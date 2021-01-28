# IDEA搭建ssm框架

## 一、创建项目

先附上测试的数据库

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` int(5) NOT NULL AUTO_INCREMENT,
  `name` varchar(10) COLLATE utf8_bin DEFAULT NULL,
  `password` varchar(10) COLLATE utf8_bin DEFAULT NULL,
  `remark` varchar(50) COLLATE utf8_bin DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8 COLLATE=utf8_bin;

-- ----------------------------
-- Records of user
-- ----------------------------
INSERT INTO `user` VALUES ('1', 'zhangsan', '123456', null);
INSERT INTO `user` VALUES ('2', 'lisi', '123', null);
INSERT INTO `user` VALUES ('3', 'wangan', '456', null);
INSERT INTO `user` VALUES ('4', 'xinxi', '000', null);
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

1.new->project出现如下

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190522183038072-534550036.png)

点击next后出现如下填写GroupId和ArtifactId在点击next直至finish

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190524234826599-471945998.png)

2.构建目录结构

在main下新建java和resources目录如下并将java目录标记为Sources Root，resources标记为Resources Root

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190522184449475-1947943982.png)

 

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190522184608164-900872960.png)

在java下新建如下包package

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190524235311868-1976705195.png)

## 二、Spring MVC

1.首先引入Spring MVC依赖

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<!-- Spring相关包 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

并添加<properties><spring.version>4.3.8.RELEASE</spring.version></properties>

2.在controller新建TestController类，在WEB-INF下新建static目录，还在WEB-INF下新建jsp目录并新建test.jsp页面

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190525000930854-990238857.png)

 

3.在web.xml添加dispatcherServlet

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="WebApp_ID" version="3.0">

  <display-name>SSM2</display-name>
  

  <!-- 设计路径变量值
  <context-param>
      <param-name>webAppRootKey</param-name>
      <param-value>springmvc.root</param-value>
  </context-param>
  -->

  <!-- Spring字符集过滤器 -->
  <filter>
    <filter-name>SpringEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
      <param-name>forceEncoding</param-name>
      <param-value>true</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>SpringEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>



  <!-- springMVC核心配置 -->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <!--spingMVC的配置路径   如果是classspath：资源是在resources下面-->
      <param-value>/WEB-INF/spring-mvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <!-- 拦截设置 -->
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>


  <welcome-file-list>
    <welcome-file>index.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

4.在WEB-INF下新建spring-mvc.xml

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="
    http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.2.xsd
    http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd">

    <!-- 扫描controller（controller层注入） -->
    <context:component-scan base-package="com.exp.controller" use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>

    </context:component-scan>

    <mvc:annotation-driven />

    <!-- 内容协商管理器  -->
    <!--1、首先检查路径扩展名（如my.pdf）；2、其次检查Parameter（如my?format=pdf）；3、检查Accept Header-->
    <bean id="contentNegotiationManager" class="org.springframework.web.accept.ContentNegotiationManagerFactoryBean">
        <!-- 扩展名至mimeType的映射,即 /user.json => application/json -->
        <property name="favorPathExtension" value="true"/>
        <!-- 用于开启 /userinfo/123?format=json 的支持 -->
        <property name="favorParameter" value="true"/>
        <property name="parameterName" value="format"/>
        <!-- 是否忽略Accept Header -->
        <property name="ignoreAcceptHeader" value="false"/>

        <property name="mediaTypes"> <!--扩展名到MIME的映射；favorPathExtension, favorParameter是true时起作用  -->
            <value>
                json=application/json
                xml=application/xml
                html=text/html
            </value>
        </property>
        <!-- 默认的content type -->
        <property name="defaultContentType" value="text/html"/>
    </bean>


    <!-- 当在web.xml 中   DispatcherServlet使用 <url-pattern>/</url-pattern> 映射时，能映射静态资源 -->
    <mvc:default-servlet-handler />
    <!-- 静态资源映射 -->
    <mvc:resources mapping="/static/**" location="/WEB-INF/static/"/>


    <!-- 对模型视图添加前后缀 -->
    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          p:prefix="/WEB-INF/jsp/" p:suffix=".jsp"/>


</beans>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

5.部署

点击如下图

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190523194813901-493739287.png)

点击+号找到Local

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190523194926122-864287233.png)

接下来修改名字，选择Deployment点击+号，选择ssm2:war exploded,另外Application context填写的如果是ssm2，那么访问的时候就是localhost:8080/ssm2,部署结束。

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190523195203266-1695981955.png)

6.启动测试

启动后默认访问的是index.jsp页面，可以访问http://localhost:8080/ssm2/test

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190525001906526-1302472584.png)

如果页面乱码在头部加上<%@ page language="java" contentType="text/html; charset=UTF-8"  pageEncoding="UTF-8"%>

## 三、Spring与Mybatis

1.引入相关依赖

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<!-- MyBatis相关包 -->
      <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
          <version>3.3.0</version>
      </dependency>
      <!-- MySQL相关包 -->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>5.1.26</version>
      </dependency>
      <!-- 数据库连接池 -->
      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
          <version>1.0.20</version>
      </dependency>
      <!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>fastjson</artifactId>
          <version>1.2.31</version>
      </dependency>

      <!-- Spring集成MyBatis -->
      <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis-spring</artifactId>
          <version>1.2.3</version>
      </dependency>

      <!-- JSP标准标签库 -->
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>jstl</artifactId>
          <version>1.2</version>
      </dependency>

      <!-- 日志相关包 -->
      <dependency>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
          <version>1.2.17</version>
      </dependency>
      <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-api</artifactId>
          <version>1.7.21</version>
      </dependency>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

2.生成实体与mybatis配置文件

在resources下新建generator目录并新建generatorConfig.xml文件

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--本地的数据库连接驱动地址-->
    <classPathEntry
            location="D:\OfficeWave\configdata\repository\mysql\mysql-connector-java\5.1.26\mysql-connector-java-5.1.26.jar"/>
    <context id="Mysql" targetRuntime="MyBatis3Simple" defaultModelType="flat">
        <property name="beginningDelimiter" value="`"/>
        <property name="endingDelimiter" value="`"/>
        <property name="mergeable" value="false"></property>
        <!--数据库连接地址-->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/user"
                        userId="root"
                        password="root">
        </jdbcConnection>
        <!--生成实体类（注意修改包路径）-->
        <javaModelGenerator targetPackage="com.exp.model" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!--生成mapper.xml-->
        <sqlMapGenerator targetPackage="mapper" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>

        <!--生成mapper.java（注意修改包路径）-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.exp.mapper"
                             targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>

            <!--数据库中的表名称和对应的实体类名称-->
        </javaClientGenerator>
        <table tableName="user" domainObjectName="User"></table>

    </context>
</generatorConfiguration>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190527195031776-2134620049.png)

在pom.xml中的<pluginManagement>标签下添加如下

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<plugins>
          <plugin>
              <groupId>org.mybatis.generator</groupId>
              <artifactId>mybatis-generator-maven-plugin</artifactId>
              <version>1.3.2</version>
              <configuration>
                  <configurationFile>${basedir}/src/main/resources/generator/generatorConfig.xml</configurationFile>
                  <overwrite>true</overwrite>
                  <verbose>true</verbose>
              </configuration>
          </plugin>
      </plugins>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

双击运行即可

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190527200016539-1627569217.png)

3.web.xml中引入spring相关配置

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<!-- 读取spring配置文件 -->
   <listener>
           <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
      </listener>
   <context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:applicationContext.xml</param-value>
</context-param>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

4.在resources下新建applicationContext.xml

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd
http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
">
    <!-- 1.配置jdbc文件 -->
    <bean id="propertyConfigurer" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
        <property name="locations" value="classpath:jdbc.properties"/>
    </bean>

    <!-- 2.扫描的包路径，这里不扫描被@Controller注解的类 --><!--使用<context:component-scan/> 可以不在配置<context:annotation-config/> -->
    <context:component-scan base-package="com.exp">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <import resource="classpath:spring-mybatis.xml" />

</beans>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

5.在resources下新建jdbc.properties文件和spring-mybatis.xml

jdbc.properties

```
jdbc_driverClassName =com.mysql.jdbc.Driver
jdbc_url=jdbc:mysql://localhost:3306/user?useUnicode=true&characterEncoding=utf8
jdbc_username=root
jdbc_password=root
```

spring-mybatis.xml

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
   http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
   http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd
   http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd">

    <!-- 3.配置数据源 ，使用的alibba的数据库-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close">
        <!-- 基本属性 url、user、password -->
        <property name="driverClassName" value="${jdbc_driverClassName}"/>
        <property name="url" value="${jdbc_url}"/>
        <property name="username" value="${jdbc_username}"/>
        <property name="password" value="${jdbc_password}"/>

        <!-- 配置初始化大小、最小、最大 -->
        <property name="initialSize" value="10"/>
        <property name="minIdle" value="10"/>
        <property name="maxActive" value="50"/>

        <!-- 配置获取连接等待超时的时间 -->
        <property name="maxWait" value="60000"/>
        <!-- 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒 -->
        <property name="timeBetweenEvictionRunsMillis" value="60000" />

        <!-- 配置一个连接在池中最小生存的时间，单位是毫秒 -->
        <property name="minEvictableIdleTimeMillis" value="300000" />

        <property name="validationQuery" value="SELECT 'x'" />
        <property name="testWhileIdle" value="true" />
        <property name="testOnBorrow" value="false" />
        <property name="testOnReturn" value="false" />

        <!-- 打开PSCache，并且指定每个连接上PSCache的大小  如果用Oracle，则把poolPreparedStatements配置为true，mysql可以配置为false。-->
        <property name="poolPreparedStatements" value="false" />
        <property name="maxPoolPreparedStatementPerConnectionSize" value="20" />

        <!-- 配置监控统计拦截的filters -->
        <property name="filters" value="wall,stat" />
    </bean>

    <!-- spring和MyBatis完美整合，不需要mybatis的配置映射文件 -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <!-- 自动扫描mapping.xml文件 -->
        <property name="mapperLocations" value="classpath:/mapper/*.xml"></property>
    </bean>


    <!-- DAO接口所在包名，Spring会自动查找其下的类 ,自动扫描了所有的XxxxMapper.xml对应的mapper接口文件,只要Mapper接口类和Mapper映射文件对应起来就可以了-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.exp.mapper" />
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"></property>
    </bean>

    <!-- (事务管理)transaction manager, use JtaTransactionManager for global tx -->
    <!-- 配置事务管理器 -->
    <bean id="transactionManager"
          class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <!--======= 事务配置 End =================== -->
    <!-- 配置基于注解的声明式事务 -->
    <!-- enables scanning for @Transactional annotations -->
    <tx:annotation-driven transaction-manager="transactionManager" />


</beans>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

6.编写代码

在service下新建接口UserService

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
package com.exp.service;

import com.exp.model.User;

import java.util.List;

public interface UserService {

    List<User> selectAll();
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 在UserServiceImpl下新建类UserServiceImpl

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```

package com.exp.service.impl;import com.exp.mapper.UserMapper;import com.exp.model.User;import com.exp.service.UserService;import org.springframework.beans.factory.annotation.Autowired;import org.springframework.stereotype.Service;import java.util.List;@Servicepublic class UserServiceImpl implements UserService {    @Autowired    private UserMapper userMapper;    @Override    public List<User> selectAll() {        List<User> userList = userMapper.selectAll();        return userList;    }}
 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
类TestController
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
package com.exp.controller;

import com.exp.model.User;
import com.exp.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import java.util.List;

@Controller
@RequestMapping("/")
public class TestController {

    @Autowired
    private UserService userService;

    @RequestMapping("/test")
    public String test(){
        List<User> userList = userService.selectAll();
        for (User user:userList){
            System.out.println(user);        }
        return "test";
    }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

7.测试

访问http://localhost:8080/ssm2/test

在server打印如下即搭建成功

![img](https://img2018.cnblogs.com/blog/1681041/201905/1681041-20190527202635404-1871660016.png)