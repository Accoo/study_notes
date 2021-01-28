# RabbitMQ笔记

## 1、安装并启动RabbitMq

docker拉取镜像，选择拉取带management的（客户端网页可进行访问）

```
docker pull rabbitmq:3-management
```

运行安装好的rabbitmq

```
docker run -d -p 5672:5672 -p 15672:15672 --name myrabbitmq f65f7c36d4
1b
```

在网页上输入192.168.43.238:15672，进行访问

进入登良路界面后输入账号guest密码guest