# Docker Desktop
## 1、拉取MySQL:8.0.36-oracle的镜像
### 1.命令拉取
```
docker pull mysql:8.0.36-oracle
```
### 2.Docker Desktop拉取
![image](https://github.com/OtakuBanana/docker/assets/14883112/bc59be71-89ff-40ce-aad5-fa92db065c22)
## 2、点击run生成
![image](https://github.com/OtakuBanana/docker/assets/14883112/c7c5736f-37cc-4f5a-a053-ba9d088f393b)
![image](https://github.com/OtakuBanana/docker/assets/14883112/798420d0-7221-4ecc-a779-4a5d96ae205a)
### ps：如果需要在主机上浏览容器目录，在Volume选项中，左侧是填写主机目录，右侧是填写容器目录，如果你是第一次创建 对容器路径不太了解，可以随意创建一个容器 然后进入到容器的shell中通过cd查找需要映射的目录，例如数据库是/var/lib/mysql。
## 3、启动成功
![image](https://github.com/OtakuBanana/docker/assets/14883112/645e60b4-47ea-4161-bc6a-d7c394e95ae8)
## 4、测试连接
![image](https://github.com/OtakuBanana/docker/assets/14883112/6bee9365-b790-4279-b069-6c32214708e8)
