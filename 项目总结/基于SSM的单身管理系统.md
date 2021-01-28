# 基于SSM的单身管理系统

## 一、配置

### 1. spring-mvc.xml

```
<!-- 1.扫描Controller（Controller层注入） -->
	<context:component-san></context:component-san>
<!-- 2.注解驱动 -->
	<mvc:annotation-driven />
<!-- 3.用location重新定位静态资源 -->
	<mvc:resourcse location="" mapping="">
<!-- 4.对视图添加前后缀 -->
	<bean id="" class="" p:prefix="/WEB-INF/jsp/" p:suffix=".jsp"
```

### 2. web.xml

```
<!-- 1.读取Spring配置文件，classpath:资源在resources下 -->
	<listener></listener>
	<context-param></context-param>
<!-- 2.读取SpringMVC配置文件，classpath:资源在resources下 -->
	<servlet></servlet>
<!-- 3.拦截设置 -->
	<servlet-mapping></servlet-mapping>
<!-- 4.过滤器 -->
	<filter></filter>
	<filter-mappeing></filter-mapping>
<!-- 5.欢迎页设置 -->
	<welcome-file-list></welcome-file-list>
```

### 3. applicationContext.xml

```
<!-- 1.配置jdbc文件 -->
	<bean></bean>
<!-- 2.扫描的包路径，这里不扫描被@Controller注解的类 -->
	<context:component-scan></context:component-scan>
<!-- 3.读取spring-mybatis文件 -->
	<import resource="classpath:spring-mybatis.xml" />
```

### 4. spring-mybatis

```
<!-- 1.配置数据源 -->
<!-- 2.结合spring和mybatis -->
<!-- 3.配置Mapper文件，自动扫描xxxMapper.xml文件，并将同名的接口一一对应 -->
<!-- 4.配置事物管理器 -->
<!-- 5.配置基于注解的声明式事务 -->
	<tx:annotation-driven transaction-manager="transactionManager" />
```

## 二、编码出现的问题及解决方法

### 1. 数据库表一对一，一对多的实现

​		首先在xxxMapper.xml文件中将数据库表中的外键属删除，然后改为外键的关联(用<association>)。

```
 <resultMap id="BaseResultMap" type="com.gdou.model.Room" >
        <id column="Room_Id" property="roomId" jdbcType="INTEGER" />
        <result column="Room_Status" property="roomStatus" jdbcType="INTEGER" />
        <association column="Room_TypeId" property="roomType" javaType="com.gdou.model.RoomType" select="com.gdou.mapper.RoomTypeMapper.selectByPrimaryKey">
            <id column="TypeId" property="typeid" jdbcType="INTEGER" />
            <result column="Room_Area" property="roomArea" jdbcType="VARCHAR" />
        </association>
 </resultMap>
```

上面代码中注意select这个属性，里面填写的内容是相应数据库表的映射文件的主键查询，即通过查询可得到相应的一行数据。

​		最后还要在对应的实体类中找到外键，将外键改为对应的实体类的实例化（注意：一定要实例化，不然会找不到数据）。

### 2. 找不到静态资源

​		在springMVC中，利用location重新定位资源。比如：

```
<mvc:resources location="/WEB-INF/assets/css/" mapping="/css/**"/>
```

### 3. 数据库DateTime类型数据的插入和前端的显示

#### 3.1 数据的插入		

```
	Date date = new Date();
	// 时间戳
    Timestamp timeStamp = new Timestamp(date.getTime());
    admin.setRegisterTime(timeStamp);
```

#### 3.2 前端的显示

```
	// 在layui中的table属性
	{field:'loginTime', width:180, title: '最近登录',templet:'<div>			   				{{layui.util.toDateString(d.loginTime, "yyyy-MM-dd HH:mm:ss") }}</div>'}        
```

### 4. 对查询结果进行分页

```
	// 使用Pagehelper传入当前页数和页面显示条数会自动为我们的select语句加上limit查询
    // 从他的下一条sql开始分页
    PageHelper.startPage(page, limit);
    //查询列表数据
    List<Administrator> adminList = adminService.selectall();
    // 使用pageInfo包装查询
    PageInfo<Administrator> rolePageInfo = new PageInfo<>(adminList);
```

### 5. 前端传入后台中文乱码问题

```
	try{
    //  解决中文乱码，adminName为字符串
        roomCheckin.setCheckinRegisterant(URLDecoder.decode(adminName,"UTF-8"));
    } catch (Exception e){
        e.printStackTrace();
    }
```

### 6. 时间格式化

```
	SimpleDateFormat sdf =   new SimpleDateFormat( "yyyyMMdd" );
    String str = sdf.format(new Date());
```

### 7. 日期的运算

```
	Calendar payedTime = Calendar.getInstance();
	// 日期加3个月，可以为负数
    payedTime.add(Calendar.MONTH,3);
	// 日期加15天，可以为负数
    payedTime.add(Calendar.DAY_OF_YEAR,15);
```

### 8. 前端获取后台传入的数组数据

​		首先后台要将数据改为字符串的形式传递

```
	// 数组转化为字符串形式，便于前端处理
    session.setAttribute("income", Arrays.toString(income));
```

​		前端需将字符串进行解析

```
	// 获取后台传入数组
	var annualData= '<%=request.getSession().getAttribute("income")%>';
	// 解析数组
	annualData=annualData.substring(1,annualData.length-1).split(", ");
```

### 9. 页面获取上一页面传入参数

```java
	//获取上一页面传入参数
    function getQueryString(name) {
        var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i');
        var r = window.location.search.substr(1).match(reg);
        if (r != null) {
            return unescape(r[2]);
        }
        return null;
    }
```

