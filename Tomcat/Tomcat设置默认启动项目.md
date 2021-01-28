# Tomcat设置默认启动项目

本机的Tomcat位置：D:\Program Files\apache-tomcat-9.0.13\conf\server.xml

顾名思义，就是让可以在浏览器的地址栏中输入ip:8080，就能访问到我们的项目。具体操作如下：

1、打开tomcat的安装根目录，找到Tomcat 6.0\conf\server.xml，打开该文件，找到<Host>节点，在该节点中添加<Context path="" docBase="../WebTest" debug="0" reloadable="true"/>。

2、再将WebTest工程放到tomcat根目录下，并将webapps文件夹中的ROOT文件夹删除或者重命名为另外一个名字

 3、启动tomcat，在浏览器中输入ip:8080，就可以访问到你的项目了。

 

 注意：<Context>节点中的docBase属性的值是指向web工程的绝对路径。

 修改tomcat访问端口号

修改端口号为80,我们就可以不用输入端口号直接访问项目了如:http://localhost/hello

在D:\Tomcat 5.5\confserver.xml 
修改port为80 ： 

```
<Connector port="80" maxHttpHeaderSize="8192" 
 maxThreads="150" minSpareThreads="25" maxSpareThreads="75" 
 enableLookups="false" redirectPort="8443" acceptCount="100" 
 connectionTimeout="20000" disableUploadTimeout="true" /> 
```

片段。 