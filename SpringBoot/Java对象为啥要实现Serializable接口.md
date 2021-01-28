## Java对象为啥要实现Serializable接口？

**Serializable接口概述**

Serializable是java.io包中定义的、用于实现Java类的序列化操作而提供的一个语义级别的接口。Serializable序列化接口没有任何方法或者字段，只是用于标识可序列化的语义。实现了Serializable接口的类可以被ObjectOutputStream转换为字节流，同时也可以通过ObjectInputStream再将其解析为对象。例如，我们可以将序列化对象写入文件后，再次从文件中读取它并反序列化成对象，也就是说，可以使用表示对象及其数据的类型信息和字节在内存中重新创建对象。

而这一点对于面向对象的编程语言来说是非常重要的，因为无论什么编程语言，其底层涉及IO操作的部分还是由操作系统其帮其完成的，而底层IO操作都是以字节流的方式进行的，所以写操作都涉及将编程语言数据类型转换为字节流，而读操作则又涉及将字节流转化为编程语言类型的特定数据类型。而Java作为一门面向对象的编程语言，对象作为其主要数据的类型载体，为了完成对象数据的读写操作，也就需要一种方式来让JVM知道在进行IO操作时如何将对象数据转换为字节流，以及如何将字节流数据转换为特定的对象，而Serializable接口就承担了这样一个角色。

下面我们可以通过例子来实现将序列化的对象存储到文件，然后再将其从文件中反序列化为对象，代码示例如下：

先定义一个序列化对象User：

```
public class User implements Serializable {     private static final long serialVersionUID = 1L;      private String userId;     private String userName;      public User(String userId, String userName) {         this.userId = userId;         this.userName = userName;     } } 
```

然后我们编写测试类，来对该对象进行读写操作，我们先测试将该对象写入一个文件：

```
public class SerializableTest {      /**      * 将User对象作为文本写入磁盘      */     public static void writeObj() {         User user = new User("1001", "Joe");         try {             ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("/Users/guanliyuan/user.txt"));             objectOutputStream.writeObject(user);             objectOutputStream.close();         } catch (IOException e) {             e.printStackTrace();         }     }      public static void main(String args[]) {         writeObj();     } } 
```

运行上述代码，我们就将User对象及其携带的数据写入了文本user.txt中，我们可以看下user.txt中存储的数据此时是个什么格式：

```
java.io.NotSerializableException: cn.wudimanong.serializable.User     at java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1184)     at java.io.ObjectOutputStream.writeObject(ObjectOutputStream.java:348)     at cn.wudimanong.serializable.SerializableTest.writeObj(SerializableTest.java:19)     at cn.wudimanong.serializable.SerializableTest.main(SerializableTest.java:27) 
```

我们看到对象数据以二进制文本的方式被持久化到了磁盘文件中。在进行反序列化测试之前，我们可以尝试下将User实现Serializable接口的代码部分去掉，看看此时写操作是否还能成功，结果如下：

结果不出所料，果然是不可以的，抛出了NotSerializableException异常，提示非可序列化异常，也就是说没有实现Serializable接口的对象是无法通过IO操作持久化的。

接下来，我们继续编写测试代码，尝试将之前持久化写入user.txt文件的对象数据再次转化为Java对象，代码如下：

```
public class SerializableTest {     /**      * 将类从文本中提取并赋值给内存中的类      */     public static void readObj() {         try {             ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("/Users/guanliyuan/user.txt"));             try {                 Object object = objectInputStream.readObject();                 User user = (User) object;                 System.out.println(user);             } catch (ClassNotFoundException e) {                 e.printStackTrace();             }         } catch (IOException e) {             e.printStackTrace();         }     }       public static void main(String args[]) {         readObj();     } } 
```

通过反序列化操作，可以再次将持久化的对象字节流数据通过IO转化为Java对象，结果如下：

```
cn.wudimanong.serializable.User@6f496d9f 
```

此时，如果我们再次尝试将User实现Serializable接口的代码部分去掉，发现也无法再文本转换为序列化对象，报错信息为：

```
ava.io.InvalidClassException: cn.wudimanong.serializable.User; class invalid for deserialization     at java.io.ObjectStreamClass$ExceptionInfo.newInvalidClassException(ObjectStreamClass.java:157)     at java.io.ObjectStreamClass.checkDeserialize(ObjectStreamClass.java:862)     at java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2038)     at java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1568)     at java.io.ObjectInputStream.readObject(ObjectInputStream.java:428)     at cn.wudimanong.serializable.SerializableTest.readObj(SerializableTest.java:31)     at cn.wudimanong.serializable.SerializableTest.main(SerializableTest.java:44) 
```

提示非法类型转换异常，说明在Java中如何要实现对象的IO读写操作，都必须实现Serializable接口，否则代码就会报错!

**序列化&反序列化**

通过上面的阐述和示例，相信大家对Serializable接口的作用是有了比较具体的体会了，接下来我们上层到理论层面，看下到底什么是序列化/反序列化。序列化是指把对象转换为字节序列的过程，我们称之为对象的序列化，就是把内存中的这些对象变成一连串的字节(bytes)描述的过程。

而反序列化则相反，就是把持久化的字节文件数据恢复为对象的过程。那么什么情况下需要序列化呢?大概有这样两类比较常见的场景：1)、需要把内存中的对象状态数据保存到一个文件或者数据库中的时候，这个场景是比较常见的，例如我们利用mybatis框架编写持久层insert对象数据到数据库中时;2)、网络通信时需要用套接字在网络中传送对象时，如我们使用RPC协议进行网络通信时;

**关于serialVersionUID**

对于JVM来说，要进行持久化的类必须要有一个标记，只有持有这个标记JVM才允许类创建的对象可以通过其IO系统转换为字节数据，从而实现持久化，而这个标记就是Serializable接口。而在反序列化的过程中则需要使用serialVersionUID来确定由那个类来加载这个对象，所以我们在实现Serializable接口的时候，一般还会要去尽量显示地定义serialVersionUID，如：

```
private static final long serialVersionUID = 1L; 
```

在反序列化的过程中，如果接收方为对象加载了一个类，如果该对象的serialVersionUID与对应持久化时的类不同，那么反序列化的过程中将会导致InvalidClassException异常。例如，在之前反序列化的例子中，我们故意将User类的serialVersionUID改为2L，如：

```
private static final long serialVersionUID = 2L; 
```

那么此时，在反序例化时就会导致异常，如下：

```
java.io.InvalidClassException: cn.wudimanong.serializable.User; local class incompatible: stream classdesc serialVersionUID = 1, local class serialVersionUID = 2     at java.io.ObjectStreamClass.initNonProxy(ObjectStreamClass.java:687)     at java.io.ObjectInputStream.readNonProxyDesc(ObjectInputStream.java:1880)     at java.io.ObjectInputStream.readClassDesc(ObjectInputStream.java:1746)     at java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2037)     at java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1568)     at java.io.ObjectInputStream.readObject(ObjectInputStream.java:428)     at cn.wudimanong.serializable.SerializableTest.readObj(SerializableTest.java:31)     at cn.wudimanong.serializable.SerializableTest.main(SerializableTest.java:44) 
```

如果我们在序列化中没有显示地声明serialVersionUID，则序列化运行时将会根据该类的各个方面计算该类默认的serialVersionUID值。但是，Java官方强烈建议所有要序列化的类都显示地声明serialVersionUID字段，因为如果高度依赖于JVM默认生成serialVersionUID，可能会导致其与编译器的实现细节耦合，这样可能会导致在反序列化的过程中发生意外的InvalidClassException异常。因此，为了保证跨不同Java编译器实现的serialVersionUID值的一致，实现Serializable接口的必须显示地声明serialVersionUID字段。

此外serialVersionUID字段地声明要尽可能使用private关键字修饰，这是因为该字段的声明只适用于声明的类，该字段作为成员变量被子类继承是没有用处的!有个特殊的地方需要注意的是，数组类是不能显示地声明serialVersionUID的，因为它们始终具有默认计算的值，不过数组类反序列化过程中也是放弃了匹配serialVersionUID值的要求。