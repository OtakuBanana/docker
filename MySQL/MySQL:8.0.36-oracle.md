# MySQL:8.0.36-oracle
## 命令版
### 1、拉取MySQL:8.0.36-oracle的镜像
```
docker pull mysql:8.0.36-oracle
```
### 2、创建容器并设置相关配置
```
# docker run -d -p 主机端口:容器端口 -e 环境变量=值 -v 主机目录:容器目录 --name 容器名称 镜像名称:版本
docker run -d --name MySQL8.0.36-oracle mysql:8.0.36-oracle \
-p 33080:3306 -p 33081:33060 \
-e MYSQL_ROOT_PASSWORD=Mysql80 \
-v /d/Docker/volume/MySQL8.0.36-oracle:/var/lib/mysql
```
以上命令创建一个镜像为mysql:8.0.36-oracle的MySQL8.0.36-oracle容器，  
使用主机的33080和33081为端口映射到容器的3306和33060端口，  
使用环境变量设置数据库的root密码为Mysql80，  
主机目录D:\Docker\volume/MySQL8.0.36-oracle映射到容器目录的/var/lib/mysql，也就是在主机的此目录下可以读写该容器目录。
### 3、停止&启动容器
```
# 停止容器
docker stop MySQL8.0.36-oracle
# 启动容器
docker start MySQL8.0.36-oracle
# 启动容器挂在后台
docker start -d MySQL8.0.36-oracle
```
### 4、测试连接
![image](https://github.com/OtakuBanana/docker/assets/14883112/6bee9365-b790-4279-b069-6c32214708e8)
## Docker Desktop/桌面版
### 1、搜索并拉取MySQL:8.0.36-oracle的镜像
![image](https://github.com/OtakuBanana/docker/assets/14883112/bc59be71-89ff-40ce-aad5-fa92db065c22)
### 2、点击run生成容器并设置相关配置
![image](https://github.com/OtakuBanana/docker/assets/14883112/c7c5736f-37cc-4f5a-a053-ba9d088f393b)
![image](https://github.com/OtakuBanana/docker/assets/14883112/798420d0-7221-4ecc-a779-4a5d96ae205a)
#### ps：在Port选项中,host port为0时随机生成映射端口，对于数据库而言我建议使用固定端口，如果不清楚应该设置什么端口，可以和我一样使用33080和33081；如果需要在主机上浏览容器目录，在Volume选项中，左侧是填写主机目录，右侧是填写容器目录，如果你是第一次创建 对容器路径不太了解，可以随意创建一个容器 然后进入到容器的shell中通过cd查找需要映射的目录，例如数据库是/var/lib/mysql。
### 3、启动容器
![image](https://github.com/OtakuBanana/docker/assets/14883112/645e60b4-47ea-4161-bc6a-d7c394e95ae8)
### 4、测试连接
![image](https://github.com/OtakuBanana/docker/assets/14883112/6bee9365-b790-4279-b069-6c32214708e8)
