#  **使用IDEA集成Maven环境**

## 1. IDEA 中配置Maven环境 如图:

 

点击 File-Settings-Maven

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps1.jpg) 

 

## 2. 使用Maven的骨架创建java项目

第一步:

 

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps2.jpg) 

第二步:  选择使用的骨架

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps3.jpg) 

第三步: 输入项目 的 组织  项目名  版本  创建项目

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps4.jpg) 

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps5.jpg) 

## 3. 不使用Maven的骨架创建java项目(实际开发推荐)

创建好的项目:  过程和使用骨架就是在选择骨架的使用不选择骨架即可

 

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps6.jpg) 

 

## 4. 使用maven创建javaWeb项目

第一步:

 

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps7.jpg) 

 

第二步: 创建好项目

![img](file:///C:\Users\lenovo\AppData\Local\Temp\ksohtml13628\wps8.jpg) 

第三步: 配置maven 的依赖和maven插件(运行插件  编译插件)

Maven 运行插件:

```
<**plugin**>         <**groupId**>org.apache.tomcat.maven</**groupId**>         <**artifactId**>tomcat7-maven-plugin</**artifactId**>         <**version**>2.2</**version**>         <**configuration**>           <**port**>8081</**port**>         </**configuration**>   </**plugin**>
```

Maven编译插件:

```xml
<plugin**>         <groupId**>org.apache.maven.plugins</**groupId**>         <artifactId**>maven-compiler-plugin</**artifactId**>         <**version**>2.3.2</**version**>         <configuration**>           <**source**>1.8</**source**>           <**target**>1.8</**target**>           <**encoding**>UTF-8</**encoding**>         </**configuration**> </**plugin**> 
```

Jsp和servlet依赖包的配置:

```xml
<**dependencies**>     <**dependency**>         <**groupId**>javax.servlet</**groupId**>         <**artifactId**>servlet-api</**artifactId**>         <**version**>2.5</**version**>         <**scope**>provided</**scope**>     </**dependency**>     <**dependency**>         <**groupId**>javax.servlet</**groupId**>         <**artifactId**>jsp-api</**artifactId**>         <**version**>2.0</**version****>**<**scope**>provided</**scope**>     </**dependency**> </**dependencies**>
```

