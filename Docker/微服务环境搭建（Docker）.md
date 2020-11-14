# 微服务环境搭建（Docker）

# MySql

https://hub.docker.com/_/mysql

拉取镜像

```
$ docker pull mysql:8.0.19
```

运行

```
$ docker run --name mysql-server -p 3306:3306 -e MYSQL_ROOT_PASSWORD=147258369 -d mysql:8.0.19
```

# Redis

https://hub.docker.com/_/redis

拉取镜像

```
$ docker pull redis
```

运行容器

```
docker run -p 6379:6379 --name redis-server -v /docker/redis/data:/data -d redis redis-server --appendonly yes
```

持久化容器

```
$ docker run -p 6379:6379 --name redis-server -d redis  -v $PWD/data:/data --appendonly yes
```

命令说明：

-p 6379:6379 : 将容器的6379端口映射到主机的6379端口

-v $PWD/data:/data : 将主机中当前目录下的data挂载到容器的/data

redis-server --appendonly yes : 在容器执行redis-server启动命令，并打开redis持久化配置

使用客户端连接容器

```
$ docker exec -it redis-server redis-cli
```

其中 redis-server 为容器名称，也可直接使用容器ID



# Consul

https://hub.docker.com/_/consul

拉取镜像

```
$ docker pull consul
```

运行容器

```
$ docker run -d -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8500:8500 -p 8600:8600 --name=consul-server -e CONSUL_BIND_INTERFACE=eth0 consul
```



访问WEB http://127.0.0.1:8500/