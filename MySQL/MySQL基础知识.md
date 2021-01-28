# MySQL基础知识

## 1、SQL语句的分类

DQL（数据查询语言）：查询语句，凡是select语句都是DQL

DML（数据操作语言）：insert delete update，对表当中的数据进行增删改

DDL（数据定义语言）：create drop alter，对表结构的增删

TCL（事务控制语言）：commit提交事务，rollback回滚事务（TCL中的T是Transaction）

DCL（数据控制语言）：grant授权、revoke撤销权限等

## 2、DOS命令行导入数据

#### 2.1、进入数据库系统 

​		mysql -uroot -p密码

#### 2.2、查看已有数据库	

​		mysql>show databases; (mysql命令，不是SQL语句）

#### 2.3、创建数据库

​		mysql>create database 数据库名; (mysql命令，不是SQL语句）

#### 2.4、使用数据库

​		mysql>use database 数据库名; (mysql命令，不是SQL语句）

#### 2.5、导入表

​		mysql>sourse sql脚本路径; (mysql命令，不是SQL语句）

#### 2.6、查看数据库中的表

​		mysql>show tables; (mysql命令，不是SQL语句）

## 3、常用命令

#### 3.1、查看mysql版本

​		myql>select verion()；

#### 3.2、创建数据库

​		myql>create database 数据库名

#### 3.3、查询当前使用的数据库

​		myql>select database()；

#### 3.4、终止一条语句

​		myql>quit或exit；

#### 3.5、查看表的结构

​		mysql>desc 表名

#### 3.6、查看其他库中的表

​		mysql>show tabes from 库名

#### 3.7、查看表的创建语句

​		mysql>show create table 表名

## 4、条件查询

| 符号                | 描述                           |
| ------------------- | ------------------------------ |
| <>或!=              | 不等于                         |
| <                   | 小于                           |
| <=                  | 小于等于                       |
| >                   | 大于                           |
| >=                  | 大于等于                       |
| between ... and ... | 在...和...之间                 |
| is null             | 为null（is not null不为空）    |
| and                 | 并且                           |
| or                  | 或者                           |
| in                  | in (...,...)包含，not in不包含 |
| not                 | 否，主要用在is或in中           |
| like                | 称为模糊查询，支持正则匹配     |

## 5、排序

​		order by 默认升序排序，可以跟多个字段，用逗号隔开，字段越前，越占排序的主导作用

​		desc 降序，  asc 升序

## 6、分组函数/聚合函数/多行处理函数

| 函数名 | 描述     |
| ------ | -------- |
| count  | 计数     |
| sum    | 求和     |
| avg    | 求平均值 |
| max    | 最大值   |
| min    | 最小值   |

- 注意：分组函数不能出现在where语句中，因为where语句执行后，才会对数据进行分组

## 7、分组查询

- group by ：后面的字段必须是在表内存在的字段，最好是进行分组的字段，不然没意义

- having：能用where解决的就用where，一般涉及分组函数才会使用having，having效率低，跟group by联合使用

## 8、select语句总结

- 字符串用单引号''括起来
- SQL语言不区分大小写，但记录的数据区分大小写
- select * 一般不用于实际开发中，效率低
- distinct：去除重复的的查询结果，只能出现所有字段的前面，所有字段进行联合去重

- 一个完整的select语句格式和执行顺序

  select 字段 				⑤

  from 表名				   ①

  where ......				  ②

  group by ......			 ③

  having ......				 ④

  order by ......			  ⑥

## 9、连接查询

### 9.1、笛卡尔积现象（笛卡尔乘积现象）

- 两表无条件连接查询时，查询结果的记录条数为两表的记录条数的乘积

### 9.2、关于表的别名

- select e.ename,d.dname from emp e,dept d;

   - 使用别名的优点：

     ① 执行效率高

     ② 可读性强

### 9.3、表的连接方式

- 内连接：

  - 等值连接

    - 语法：

      ... A (inner) join B on 连接条件（等值）

  - 非等值连接:

    - 语法：

    ​        ... A (inner) join B on 连接条件（非等值）

  - 自连接：

    - 语法：

      ... emp a (inner) join emp b on 连接条件

    - 看成两个相同的表连接

- 外连接（主要特点：主表的数据无条件的全部查询出来）

  - 左外连接（左连接）：表示左边的表是主表
  - 右外连接（右连接）：表示右边的表是主表
  - 全连接（很少用）

- 内连接和外连接的区别：

  - 内连接：

    假设A和B表进行连接，使用内连接的话，凡是A表和B表能够匹配上的记录查询出来。AB两表没有主副之分，两张表是平等的。

  - 外连接：

    假设A和B表进行连接，使用外连接的话，两张表中有主副之分，主要查询主表中的数据，捎带查询副表，当副表中的数据没有和主表中的数据匹配上，副表自动模拟出Null与之匹配

## 10、子查询

- select语句中嵌套select语句，被嵌套的语句语句是子查询

- 子查询可出现的的位置：

  select 

  ​		..(select)..

  from

  ​		..(select)..

  where

  ​		..(select)..

## 11、union

- 可以将查询结果集相加

- 例如：

  ​	select ename,job from where job = 'MANAGER' 

  ​	union

  ​	select ename,job from where job = 'SLESMAN'；

- 要求：查询结果的列数相同

## 12、limit

- 重点中的重点，实现分页查询；

- mysql特有，其他数据库没有，不通用（Oracle有相通机制叫rownum）

- 通用的分页公式：

  ​	每页显示pageSize条记录：

  ​	第pageNo页：(pageNo - 1)* pageSize, pageSize

## 13、约束

### 13.1、唯一性约束(unique)

- 唯一性约束修饰的字段具有唯一性，不能重复，但可以为null

- 给某一列添加unique：username varchar(255) unique  //列级约束

- 给两个列或者多个列添加unique：

  unique(usercode,username)  //多个字段联合起来添加一个约束unique 【表级约束】

- 注意：not null约束只有列级约束，没有表级约束

### 13.2、主键约束

- id int primary key,  //列级约束
- 划分：
  - 按字段数量：单一主键（推荐）、复合主键
  - 按主键性质：自然主键（推荐）、业务主键
-  一张表的主键约束只能有1个
- mysql提供主键值自增
- Oracle当中也提供了一个自增机制，叫做：序列(sequence)对象

### 13.3、外键约束

- 关于外键约束的相关术语：
        外键约束：foreign key
        外键字段：添加有外键约束的字段
        外键值：外键字段中的每一个值

- 父子表：

  ​	  删除数据的时候，先删除子表，再删除父表。
  ​      添加数据的时候，先添加父表，再添加子表。
  ​      创建表的时候，先创建父表，再创建子表。
  ​      删除表的时候，先删除子表，再删除父表。

- 外键可以为null
- 被引用的字段不一定是主键，但至少是具有unique约束，具有唯一性，不可重复

## 14、存储引擎

### 14.1、完整的建表语句

​    CREATE TABLE `t_x` (
​      `id` int(11) DEFAULT NULL
​     ) ENGINE=InnoDB DEFAULT CHARSET=utf8; 

-  mysql默认使用的存储引擎是InnoDB方式
- 默认采用的字符集是UTF-8

### 14.2、查看当前mysql支持的存储引擎？

​       show engines \G

### 14.3、常见的存储引擎

​      Engine: MyISAM
​      Support: YES
​      Comment: MyISAM storage engine
​      Transactions: NO
​	  XA: NO
​      Savepoints: NO

   MyISAM这种存储引擎不支持事务。
   MyISAM是mysql最常用的存储引擎，但是这种存储引擎不是默认的。
   MyISAM采用三个文件组织一个表：
       xxx.frm(存储格式的文件)
	   xxx.MYD(存储表中数据的文件)
  	 xxx.MYI(存储表中索引的文件)

- 优点：可被压缩，节省存储空间。并且可以转换为只读表，提高检索效率。
- 缺点:不支持事务。

--------------------------------------------------------------------------

​       Engine: InnoDB
​       Support: DEFAULT
​       Comment: Supports transactions, row-level locking, and foreign keys
​       Transactions: YES
​	   XA: YES
​       Savepoints: YES

- 优点：支持事务、行级锁、外键等。这种存储引擎数据的安全得到保障。

   表的结构存储在xxx.frm文件中
   数据存储在tablespace这样的表空间中(逻辑概念)，无法被压缩，无法转换成只读。
   这种InnoDB存储引擎在MySQL数据库崩溃之后提供自动恢复机制。
   InoDB支持级联删除和级联更新。

----------------------------------------------------------------------------------

​      Engine: MEMORY
​      Support: YES
​      Comment: Hash based, stored in memory, useful for temporary tables
​      Transactions: NO
​	  XA: NO
​      Savepoints: NO

- 缺点：不支持事务。数据容易丢失。因为所有数据和索引都是存储在内存当中的。

- 优点：查询速度最快。
- 以前叫做HEAP引擎。

## 15、事务（Transaction）

### 15.1、什么是事务

- 一个事务是一个完整的业务逻辑单元，不可再分
- 和事务相关的语句只有DML语句（insert delete update）
  - 为什么？因为他们这三个语句都是和数据库表当中的“数据”相关的
  - 事务的存在是为了保证数据的完整性、安全性

- mysql事务默认情况下是自动提交的
- 怎么关闭默认提交？start transaction;
- rollback;（回滚）或者commit;（提交）都可结束事务

### 15.2、事务的特性

- 事务包括四大特性：ACID
  - 原子性：事务是最小的工作单元，不可再分
  - 一致性：事务必须保证多条DML语句同时成功或者同时失败
  - 隔离性：事务A与事务B之间具有隔离性
  - 持久性：最终数据必须持久化到硬盘中，事务才算成功结束

### 15.3、事务的隔离性级别

- 第一级别：读未提交（read uncommitted）

  - 对方事务还没有提交，我们当前事务可以读取到对方未提交的数据

  - 读未提交存在脏读(Dirty Read) 现象：表示读到了脏数据

- 第二级别：读已提交(read committed)

  - 对方事务提交之后的数据我方可以读取到

  - 读已提交存在的问题是：不可重复读

- 第三级别：可重复读(repeatable read)

  - 这种隔离级别解决了：不可重复读问题

  - 这种隔离级别存在的问题是：读取到的数据是幻象

- 第四级别：序列化读/串行化读（serializable）

  - 解决了所有问题
  - 效率低，需要事务排队



- Oracle数据库默认的隔离级别是：第二级别，读已提交
- mysql数据库默认的隔离级别是：第三级别，可重复读

## 16、索引

### 16.1、什么是索引？有什么用？

- 索引相当于一本书的目录，通过目录可以快速地找到对应的资源。
- 在数据库方面，查询一张表的时候有两种检索方式：
  - 全表扫描
  - 根据索引检索（效率很高）

- 索引为什么能提高检索效率？起根本原理是缩小扫描的范围

- select ename,sal from emp where ename = 'SMITH';
  	当ename字段没有添加索引的时候，以上sql语句会进行全表扫描，扫描ename字段中所有的值。
  	当ename字段添加索引的时候，以上sql语句会根据索引扫描，快速定位。

### 16.2、怎么创建索引对象？怎么删除索引对象？

- 创建索引对象：create index 索引名称 on 表名（字段名）;
- 删除索引对象：drop index 索引名称 on 表名;

### 16.3、满足什么条件才考虑添加索引

- 数据量庞大。（根据客户的需求，根据线上的环境）
- 该字段很少的DML操作。（因为字段进行修改操作，索引也需要维护）
- 该字段经常出现在where子句中。（经常根据哪个字段维护）



注意：转具有unique约束的字段会自动添加索引。根据主键查询效率较高，尽量根据主键检索。

### 16.4、索引的实现原理

- 索引底层采用的数据结构是：B+ Tree
- 原理：通过B Tree缩小稻苗范围，底层索引进行了排序、分区，索引会携带数据在表中的“物理地址。通过索引检索到数据后，获取到关联的物理地址，最终通过物理地址定位表中的数据，这样效率就会变的很高。

- select ename from emp where ename = 'SMITH';
  通过索引转换为：
  select ename from emp where  物理地址 = 0x123;

### 16.5、索引的分类

- 单一索引：给单个字段添加索引

- 复合索引：给多个字段联合起来添加一个索引

- 主键索引：主键上会自动添加索引

- 唯一索引：有unique约束的字段会自动添加索引

  ......

### 16.6、索引什么时候失效

- select ename from emp where ename like ‘%A%’;

  模糊查询的时候，第一个通配符使用的是%，不能确定检索的区域。

## 17、视图

### 17.1、什么是视图？

​       站在不同的角度去看到数据。(同一张表的数据，通过不同的角度去看待)

### 17.2、怎么创建视图？怎么删除视图？

- create view myview as select empno,ename from emp;

- drop view myview;

- 注意：

  - 只有DQL语句才能以试图对象的方式创建出来。

  - 对试图进行增删改查，会影响到原表数据。(通过视图影响原表数据，不是直接操作的原表)
    可以对视图进行CRUD操作。

### 17.3、视图的作用

- 可以隐藏表的实现细节。保密级别较高的系统，数据库只对外提供相关的视图，java程序员只对视图对象进行CRUD

## 18、DBA命令

### 18.1、在数据库当中的数据导出

- 在windows的DOS命令窗口中执行： (导出整个库)
  mysqldump bjpowernode>D:\bjpowernode.sql -uroot -p999

- 在windows的dos命令窗口中执行：(导出数据库中指定的表)
  mysqldump bjpowernode emp>D:\bjpowernode.sql -uroot -p999

### 18.2、导入数据

- create database bjpowernode;

- use bjpowernode;

- source D:\bjpowernode.sql 

