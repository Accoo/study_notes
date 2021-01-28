# Elasticsearch笔记

## 1、安装运行

docker拉取安装后，执行下面命令

```linux
docker run -e ES_JAVA_OPTS"-Xms256m -Xmx256m" -d -p 9200:9200 -p 9300:9300 --name ES01 5acf0e8da90b
```

由于elasticsearch默认启动占用2G内存，若虚拟机内存太小会导致运行失败。

## 2、解决跨域问题

- 首先进入刚运行镜像的安装位置

```
docker exec -it ES01 bash 
```

- 使用ls查看当前文件夹下的文件
- 进入conf文件夹 cd conf
- 修改elasticsearch.yml文件

```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

但由于docker下不支持vi命令，需要先将配置文件复制到宿主机中

```
docker cp ES01:/usr/share/elasticsearch/config/elasticsearch.yml  /usr/docker/elasticsearch/conf/elasticsearch.yml
```

- 修改完成后运行挂载

```
docker run -e ES_JAVA_OPTS"-Xms256m -Xmx256m" -d --name myES -p 9200:9200 -p 9300:9300 -v /usr/docker/elasticsearch/conf/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml 5acf0e8da90b
```

