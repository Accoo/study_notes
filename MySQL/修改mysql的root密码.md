# 修改mysql的root密码

## 方法一：用set password命令

首先登陆MySQL；

格式：mysql>set password for <u>用户名@localhos</u>t = password（‘新密码’）；

例子：mysql>set password for root@localhost = password（‘123’）；

（注意加分号）



## 方法二：用mysqladmin

格式：mysqladmin -u用户名 -p旧密码 password 新密码

例子：mysqladmin -uroot -p123456 password 123



## 方法三：用update直接编辑user表

首先登陆MySQL。

mysql> use mysql ；

mysql> update user set password=password('123') where user='root' and host='localhost'；

mysql> flush privileges；

（注意分号要加上，表示一个语句结束）



## 方法四：在忘记root密码的时候

1. 关闭正在运行的mysql服务；
2. 打开DOS窗口，转到mysql\bin目录；
3. 输入mysqld --skip-grant-tables 回车；（--skip-grant-tables的意思是启动MySQL服务的时候跳过权限表的认证）
4. 再开一个DOS窗口（因为刚才那个DOS窗口已经不能动了），转到mysql\bin目录；
5. 输入mysql回车，如果成功，将出现MySQL提示符>；
6. 连接权限数据库：use mysql；
7. 改密码：update user set password=password('123') where user='root'；（注意加分号）
8. 刷新权限（必须步骤）：flush privileges；
9. 退出 quit；
10. 注销系统，再进入，使用用户名和刚才设置的新密码123登录。