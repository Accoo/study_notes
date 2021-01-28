## SSM与SpringBoot的区别：

可以从SSM框架和SpringBoot的搭建步骤进行分析

#### SSM框架的搭建步骤

1. 利用Maven加相关的依赖包（jar包）

2. 配置web.xml，加载Spring，SpringMVC

3. 配置数据库连接，Spring事务
4. 配置加载配置文件的读取，开启注解
5. 配置日志文件
6. 配置完成，部署Tomcat调试

#### 新建SpringBoot项目的步骤

1. 创建Maven工程
2. 添加SpringBoot的起步依赖；
3. 配置SpringBoot引导类
4. 配置controller

SpringBoot框架使用starter依赖主要是为了引入相关的jar和自动完成bean配置

对比两者以上搭建框架的步骤可分析两者的主要区别为：

1. SpringBoot将原来的xml配置，简化为java注解
2. SpringBoot可简化Spring应用的初始搭建以及开发过程
3. SpringBoot内置的Tomcat服务器，可以jar形式启动一个服务，可以快速部署发布web服务
4. SpringBoot使用starter依赖自动完成bean配置，解决bean之间的冲突，并引入相关的jar包（这一点最重要）