# Git基本操作

- **git init**  在需要的地方建立一个版本库（也就是仓库）

- **ls -ah**    可以看默认隐藏的文件

- **git add filename** 将文件加入暂存区

- **git commit -m** “” 将暂存区的内容提交到当前分支

- **git status**  查看当前仓库状态

- **git diff** 查看修改内容

- ======================版本回退========================

- **git log** 查看历史版本记录

- **git log --pretty=oneline** 查看历史版本记录精简版

- **git reset –hard HEAD**

- - HEAD 是当前版本
  - HEAD^是上一个版本
  - HEAD^^是上上个版本
  - HEAD~100是回退100个后的版本
  - 一般是HEAD 789790890(版本号)

- 回退到某一个版本以后关电脑后想回到未来版本

-    | **git reset –hard HEAD^**--- **git relog**(记录每一次命令)找到版本号

- ==================管理和撤销修改=========================

- 1.丢弃工作区的修改 **git checkout --fileName**

- 2.丢弃暂存区的修改回到工作区  **git reset HEAD fileName**

- 删除操作--|**rm file**—然后删除暂存区 **git rm file----git commit**

- ​          |手误 **git reset –hard HEAD**

- ==================远程操作===============================

- 1.创建SSHKey 在c:adminstrater:.ssh----找到id_rsa和id_rsa.pub

- - 1.有---将自己的密钥id_rsa.pub粘贴
  - 2.没有的话—打开git bash 创建 ssh-keygen -t rsa -C“email,一路回车创建，不用设置密码

- 2.创建远程仓库和本地仓库的连接,步骤和方法：

- - 1.第一步 在网站上创建远程仓库，
  - github
  - 

　　　　**![img](https://images2018.cnblogs.com/blog/1432315/201807/1432315-20180726103245686-1003732326.png)**

- - coding.net的全是中文，大家一般都能根据提示操作进行，我就不提示了。

- 第二步，也是最重要的一步：下面分为两种情况：

- - **先创建本地仓库后连接远程仓库**                         

  - - **git remote add origin url(****托管平台地址例如Github/coding.net……  这种方法适用于)**

  - **先创建远程仓库再连接本地仓库**                                                             

  - - **git clone “url”**(仓库地址,同上)

- **git push -u origin master** 将master分支上的版本库推动到远程库

- **git pull origin master** 将本地更新成最新的代码

- ===================分支管理==============================

- **git checkout -b**  (创建并切换到dev分支)

-  |等价于**git branch dev + git checkout dev**

- **git branch** 查看当前分支

- **git merge dev** 指定合并dev分支到master分支

- 出现冲突需要手动修改冲突

- **git log --graph --pretty=oneline --abbrev-commit**

- |查看分支合并情况  

- **git merge --no-ff -m** **"merge with no-ff"dev** **（与Git Merge dev 不同之处是保留合并历史）**