### 安装运行Redis

#### 拉取镜像

在国内的镜像市场找到redis, 选好版本,pull下来,[传送门](https://links.jianshu.com/go?to=https%3A%2F%2Fhub.daocloud.io%2Frepos%2Fbeb958f9-ffb6-4f68-817b-c17e1ff476c3)

选一个新的,并且稳定的版本,我这里选择的3.2.9版本

执行以下命令,pull镜像



```dart
docker pull daocloud.io/library/redis:3.2.9
```

#### 创建文件夹

创建两个文件夹,一个用来放持久化的数据,一个用来放配置文件,如果不把持久化的数据放在服务器本地的话,重启容器,数据就没了.



```kotlin
mkdir /usr/docker/redis/data
mkdir /usr/docker/redis/conf
```

data文件夹用来存放数据,conf文件夹用来存放redis的配置文件

#### 配置文件修改

在[github](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2F)中搜索redis,找到对应的版本,我在上面是下载的3.2.9版本,所以我在release中找到[3.2.9版本](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fantirez%2Fredis%2Freleases%2Ftag%2F3.2.9),然后下载源码

下载完成之后找到`redis.conf`这个文件

-  `bind 127.0.0.1`,在配置文件中找到这个配置,注释掉(注释掉才可以远程连接redis)
-  `protected-mode yes`,找到这个配置改为`protected-mode no` 
-  `daemonize yes`找到这个配置,注释掉

最后保存修改,文件上传到服务器刚刚创建好的`/usr/docker/redis/conf`目录下面

#### 启动容器

命令:



```kotlin
docker run -p 6379:6379 --name redis01 -v /usr/docker/redis/conf/redis.conf:/etc/redis/redis.conf -v /usr/docker/redis/data:/data --privileged=true -d 3459037fcc3a redis-server /etc/redis/redis.conf --appendonly yes --requirepass 666666
```

参数解析:

-  `-p` 端口映射
-  `--name` 指定容器的名称是`redis-6379` 
-  `-v` 映射容器外部的配置文件和目录
-  `--privileged=true`  使容器内的root用户具有真正的root用户的权限,不设置可能会启动失败,提示没有权限
-  `-d 3459037fcc3a` -d是以后台的方式启动,`3459037fcc3a`是最开始拉下来的镜像的id
-  `redis-server /etc/redis/redis.conf`  指定配置文件启动redis-server进程
-  `--appendonly yes` 开启数据持久化

#### 启动完成查看状态

可以通过以下命令,查看正在运行的容器



```undefined
docker ps
```

#### 完成

上面的操作全部搞定之后,就可以通过远程去连接了