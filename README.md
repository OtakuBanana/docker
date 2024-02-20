# Docker
## Docker Desktop 容器位置
```
\\wsl.localhost\docker-desktop-data\mnt\wslg\distro\data\docker\containers
```
或者在以下目录搜索containers
```
\\wsl.localhost\docker-desktop-data
```
## Windows containers 卷位置
```
C:\ProgramData\Docker\volumes
```
## Linux containers 卷位置
```
/var/lib/docker/volumes/
```
## 查看&启动&停止容器
```
# 查看所有容器
docker ps -a
# 查看运行中的容器
docker ps
# 停止容器
docker stop 容器ID或容器名称
# 启动容器
docker start 容器ID或容器名称
# 启动容器挂在后台
docker start -d 容器ID或容器名称
```
## 如何在 Linux containers 下创建容器，在主机目录上浏览容器目录（以MySQL为例）
### 1.命令版
```
# docker run -d -p 主机端口:容器端口 -e 环境变量=值 -v 主机目录:容器目录 --name 容器名称 镜像名称:版本
docker run -d --name MySQL8.0.36-oracle mysql:8.0.36-oracle \
-p 33080:3306 -p 33081:3306 \
-e MYSQL_ROOT_PASSWORD=Mysql80 \
-v /d/Docker/volume/MySQL8.0.36-oracle:/var/lib/mysql
```
以上命令创建一个镜像为mysql:8.0.36-oracle的MySQL8.0.36-oracle容器，  
使用主机的33080和33081为端口映射到容器的3306端口，  
使用环境变量设置数据库的root密码为Mysql80，  
主机目录D:\Docker\volume\MySQL8.0.36-oracle映射到容器目录的/var/lib/mysql，也就是在主机的此目录下可以读写该容器目录。  
### 2.桌面版
[Docker Desktop中创建MySQL容器](MySQL/MySQL%3A8.0.36-oracle.md)
