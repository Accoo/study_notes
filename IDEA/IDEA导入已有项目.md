# IDEA导入已有项目

先关闭原有项目File-->close Project，然后选择Import Project

或者File-->Project From Existing Sources

1. 1. 选择Create project from existing sources

![img](https://img-blog.csdnimg.cn/20190129110549735.png)

1. 1. 设置项目SDK, 点击 + 号添加本地的JDK

![img](https://img-blog.csdnimg.cn/20190129110835670.png)

1. 配置tomcat
   1. 等待idea初始化项目后，点击右下角event log

![img](https://img-blog.csdnimg.cn/20190129110847719.png)

1. 1. 点击红框中的Create Default Context 和 Configure 配置项目



![img](https://img-blog.csdnimg.cn/20190129110859523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190129110917731.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

1. 1. 点击File,打开Project Structure

![img](https://img-blog.csdnimg.cn/20190129110924387.png)

1. 1. 在Project Structure 中选择Artifacts-Web Application:Exploded-From Modules

![img](https://img-blog.csdnimg.cn/2019012911095414.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190129111002763.png)

1. 1. 双击红框中lib,点击apply保存配置

![img](https://img-blog.csdnimg.cn/20190129111020770.png)

![img](https://img-blog.csdnimg.cn/20190129111028812.png)

1. 1. 点击右上角的Add Configuration，配置tomcat

![img](https://img-blog.csdnimg.cn/20190129111035232.png)

1. 1. 点击 + 号，找到Tomcat server选择loca

l![img](https://img-blog.csdnimg.cn/20190129112500595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

1. 1. 在Configure中添加本地Tomcat，点击Deployment

![img](https://img-blog.csdnimg.cn/20190129112508404.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

1. 1. 
   2. 1. 在Deployment中点击 + 号，选择Artifact...，并修改Application context为eginpms

   ![img](https://img-blog.csdnimg.cn/2019012911251548.png)

   ![img](https://img-blog.csdnimg.cn/20190129112522797.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

1. 1. 设置虚拟内存和资源热部署

![img](https://img-blog.csdnimg.cn/20190129112529930.png)



![img](https://img-blog.csdnimg.cn/2019012911253673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vbnN0YXJfaHU=,size_16,color_FFFFFF,t_70)

 

1. 1. 点击右上角run 或者debug即可启动项目

 

![img](https://img-blog.csdnimg.cn/20190129112544942.png)