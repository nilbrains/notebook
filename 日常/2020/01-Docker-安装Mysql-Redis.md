# Docker 安装Mysql和Redis

## 安装 Docker

`https://www.docker.com/get-started`

此步骤省略....

## 安装 Mysql

### 拉取 Mysql 镜像

```cmd
docker pull mysql:5.7.35
```

### 运行

```cmd
sudo docker run -p 3306:3306 
--name=nil_mysql 
-v /home/nil/docker/mysql/conf:/etc/mysql 
-v /home/nil/docker/mysql/log:/var/log/mysql 
-v /home/nil/docker/mysql/db:/var/lib/mysql 
-e MYSQL_ROOT_PASSWORD=123456 
-d mysql:5.7.35
```

### OK

## 安装 Redis

### 拉取镜像

```cmd
docker pull redis
```

### 运行镜像

```cmd
docker run -d --name=nil_redis -p 6379:6379 redis --requirepass "123456"
```

### ok
