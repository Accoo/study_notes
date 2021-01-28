# IntelliJ IDEA(2019)创建maven项目

## 一、创建maven项目

1.配置maven仓库信息，file–>setting

![img](C:\Users\lenovo\Desktop\笔记\Maven\assets\201905022113362.png)

2.创建maven项目
  file–>new->project

![img](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502211916597.png)

## 二、配置maven项目

  创建成功的项目目录结构所有缺失，我们需要手动创建完成。

​		在main目录下分别设置java文件夹和resources文件夹，右键-->Mark directory as

![1577429055437](C:\Users\lenovo\Desktop\笔记\Maven\assets\1577429055437.png)

​		修改文件的作用，具体如下:

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502213545587.png)

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502213734783.png)

也可以右键项目-选择Open Module Settings打开项目配置页面更改

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502214050651.png)

配置依赖jar包

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502214140593.png)

## 三、tomcat插件

### 1.配置插件

```xml
<plugin>
<groupId>org.apache.tomcat.maven</groupId>
  <artifactId>tomcat7-maven-plugin</artifactId>
  <version>2.2</version>
  <configuration>
    <port>8080</port> <!-- 访问端口-->
    <path>/</path>    <!-- 访问路径-->
  </configuration>
</plugin>
```

### 2.配置tomcat启动

2.1如果在pom.xml中配置了Tomcat插件，在右边的Maven Project中会出现对应的插件

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502222204996.png)
启动成功

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502222322898.png)

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\2019050222222353.png)

访问成功

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\2019050222230838.png)

2.2也可以显示配置。点击Run–>Edit Configurations后搜索maven

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502222506183.png)

![在这里插入图片描述](C:\Users\lenovo\Desktop\笔记\Maven\assets\20190502222531670.png)

ok~项目搞定

链接：https://blog.csdn.net/qq_38526573/article/details/89765132