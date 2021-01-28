# 数据库SQL语句

数据库中存在三张表部门表（dept）、员工表（emp）、薪资表（salgrade）

dept(deptno, dname)

emp(empno, ename, deptn, sal)

salgrade(salno, lasal, hisal, grade)

### 1、取得每个部门最高薪水的人员名称？

第一步：取得每个部门的最高薪水

​	select deptno,max(sal) as maxsal from emp group by deptno;

第二步：查询对应部门和最高薪水的人员名称

​	select e.ename, t.*

​	from emp e 

​	join (select deptno,max(sal) as maxsal from emp group by deptno) as t

​	on e.deptno = t.deptno and e.sal = t.maxsal;

### 2、哪些人的薪资在部门的平均薪资之上？

第一步：每个部门的平均薪资

​	select deptno,avg(sal) as avgsal from emp group by deptno;

第二步：查询在部门的平均薪资之上的人员

​	select t.deptno, t.avgsal, e.ename, e.sal

​	from emp as e 

​	join  (select deptno,avg(sal) as avgsal from emp group by deptno) as t

​	on e.deptno = t.deptno and e.sal > t.avgsal ;

### 3、取得部门中（所有人的）平均的薪资等级

第一步：取得所有人的薪资等级

​	select e.name, e.sal, e.deptno, s.grade

​	from emp e

​	join salgrade

​	where e.sal > s.losal and e.sal<hisal;

第二步：取得部门的平均薪资等级

​	select e.deptno, avg(s.grade)

​	from emp e

​	join salgrade

​	where e.sal > s.losal and e.sal<hisal

​	group by e.deptno;

### 4、不准用聚合函数（Max），取得最高薪资（给出两种解决方案）

方案一：select sal from emp order by sal desc limit 1;

方案二（自连接）：

​				select sal from emp 

​				where sal not in 

​					(select distinct a.sal from emp a join emp b on a.sal < b.sal);

### 5、取得平均薪资最高的部门的部门编号（两种方案）



### 6、取得平均薪资最高的部门的部门名称



### 7、求平均薪资的等级最低的部门名称



### 8、取得比普通员工的最高薪资还要高的领导人姓名



### 9、取得薪资最高的前五名员工



### 10、取得薪水最高的第六到第十名员工



### 11、取得最后入职的5名员工



### 12、取得每个薪资等级有多少



### 13、面试题



### 14、列出所有员工及领导的姓名



### 15、列出受雇日期早于其直接



### 16、列出部门名称和这些部门的



### 17、列出至少有5名员工的所有



### 18、列出薪资比‘SMITH’多的



### 19、列出所有‘CLERK’（办事员



### 20、列出最低薪资大于1500的



### 21、列出在部门‘SALES’（销售



### 22、列出薪资高于公司平均薪资



### 23、列出与‘SCOTT’从事相同



### 24、列出薪资等于部门编号为30中员工



### 25、列出薪资高于在部门编号为30