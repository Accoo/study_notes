# Git使用教程

**网址：**https://www.cnblogs.com/mswei/p/9370238.html

## **一、创建新项目**

**1.**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090153567-957214773.png)**

**2.**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090204359-1163249557.png)**

 

**3.**

　　[![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090420794-1551885621.png)](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090420794-1551885621.png)

4.

　　[![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090449459-1085613830.png)](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726090449459-1085613830.png)

 

## **二、打开安装好的Git Bash，开始工作**

　　1.配置gitbash和github的通信协议 ，输入ssh-keygen –t rsa –C “邮箱地址” 然后一直按回车回车回车回车。。。。箭头指向的邮箱填写我当时填的是和github上写的邮箱一致。 

　　　　　[![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726091253142-1132109107.png)](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726091253142-1132109107.png)

　　2.**然后你就可以根据上图提示信息打开文件目录，找到那个文件，用文本方式打开.pub文件。直接全选复制。**

　　　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726091819545-1670738918.png)**

## **三、添加ssh密匙**

　　将本机的ssh秘钥添加到个人账户中，打开github自己的主页Settings->SSH->newSSHkey  步骤如下图：

　　**1.**

　　　　![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726093001047-165784277.png)

　　**2.**

　　　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726093056110-2094399205.png)**

　　**3.**

　　　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726093120867-1850175443.png)**

## **四、验证ssh设置！**

　　　　**输入命令：ssh –T git@github.com，会出现yes or no，就输入yes，回车。** 

**1**|**0**　　

## **五、配置gitbash的用户名和邮箱：**

　　git config --global user.name “用户名”

　　git config --global user.email “邮箱” 

　　使用github上的用户名和邮箱。 

　　[![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726093906652-510545361.png)](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726093906652-510545361.png)

## 六、更新本地仓库和远程仓库

**配置了这么多，终于可以办大事了，将你刚刚在github上创建的project和本地联系起来**

　　**大概流程，就是先在本地找个空的文件夹，然后用gitbash初始化一下这个文件夹的信息，使他变成一个类似于可以被管理的仓库，然后再从远程仓库github上pull上面的东西下来这个文件夹，然后自己修改好了，再push回去远程github，就这么简单**

### **1.创建文件夹**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726094441822-1400201723.png)**

### **2.用git bash打开并切换到此文件夹下，使用git init初始化文件夹**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726095141688-1056022171.png)**

### **3.建立与远程仓库的链接**

　　**命令：git remote add origin 你的git地址**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726095548800-893287807.png)** 

　　**git项目地址**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726095633479-101481823.png)**

### 4.拉取远程仓库文件

　　**git pull 你的git地址**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726100350010-944495064.png)**

　　**此时，文件夹中就多了个文件夹，就表示拉取成功了**

### **5.在本地仓库中添加文件，直接新建就行**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726100701064-243991784.png)**　　

### **6.将文件添加到缓冲区add，提交文件commit**

　　　**git add .     将所有改变的文件添加到缓冲区**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726101754967-1223848470.png)**　　

　　**git commit -m '提交说明'**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726102302444-941378819.png)**

　　

### **7.将本地仓库上传到github上，地址就是拉取的地址**

　　**git push '项目git地址'**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726102326530-721137049.png)**

### **8.此时，再次到github个人主页上就可以看到上传的文件了**

　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726102406796-1888416535.png)**