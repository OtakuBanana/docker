# MySQL&PXC8 集群(?)部署
ps：此教程也许不准确，但是是基于个人理解在本地docker跑多个节点，实现多个数据库数据同步。（不包含swarm）

### 1、拉取percona-xtradb-cluster
![image](https://github.com/OtakuBanana/docker/assets/14883112/67af6dfe-8280-4f2c-a379-646de13bd8d7)
对应的版本则是MySQL版本。(percona-xtradb-cluster以下简称为pxc)pxc自带MySQL数据库
### 2、创建对应网段
通过命令创建网段供MySQL集群使用
```
# 创建一个mysql-net名称的网段，并设置其ip、16位
docker network create --subnet=172.18.0.0/16 mysql-net
# 查询网段
docker network inspect mysql-net
```
### 3、创建第一个数据库
在创建前可以重命名镜像，缩减长度的同时也避免粗心写错
```
# 我拉取的是latest版本
docker tag percona/percona-xtradb-cluster:latest pxc
```
然后开始创建第一个容器
```
docker run -d \
-p 33088:3306 \
-v /d/Docker/volume/MySQL-Cluster/M1:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=Mysql80 \
-e CLUSTER_NAME=pxc \
-e XTRABACKUP_PASSWORD=123456 \
--privileged \
--name=MySQL-Cluster-M1 \
--net=MySQL-Net \
pxc
```
静默创建一个容器
映射主机端口33088至容器3306
主机目录D:\Docker\volume\MySQL-Cluster\M1映射到容器目录的/var/lib/mysql
环境变量MYSQL_ROOT_PASSWORD是设置MySQL的root密码为Mysql80
环境变量CLUSTER_NAME是设置集群的名称为pxc
环境变量XTRABACKUP_PASSWORD是设置集群间同步数据的密码为123456
privileged是以root用户运行容器
name设置容器名称
net设置容器网段（如果需要指定ip则再加上 例如--ip=172.18.0.2）
最后的pxc为镜像名称
![image](https://github.com/OtakuBanana/docker/assets/14883112/f2de9808-55d8-498e-a42f-5a015adcf0b1)
这样我们就成功创建了第一个容器，接下来要创建其节点容器
```
docker run -d -p 33089:3306 -v /d/Docker/volume/MySQL-Cluster/M2:/var/lib/mysql -e CLUSTER_JOIN=MySQL-Cluster-M1 -e MYSQL_ROOT_PASSWORD=Mysql80 -e CLUSTER_NAME=pxc -e XTRABACKUP_PASSWORD=123456 --privileged --name=MySQL-Cluster-M2 --net=MySQL-Net pxc
# 如果需要再增加节点则修改名称和映射目录即可，CLUSTER_JOIN=MySQL-Cluster-M1指向的第一个容器无需修改
docker run -d -p 33089:3306 -v /d/Docker/volume/MySQL-Cluster/M3:/var/lib/mysql -e CLUSTER_JOIN=MySQL-Cluster-M1 -e MYSQL_ROOT_PASSWORD=Mysql80 -e CLUSTER_NAME=pxc -e XTRABACKUP_PASSWORD=123456 --privileged --name=MySQL-Cluster-M3 --net=MySQL-Net pxc
```
该命令增加了一个CLUSTER_JOIN=MySQL-Cluster-M1，用来指定加入到某个集群容器
#### 首次创建其节点容器的时候会出现错误，我们需要进入到第一个容器的目录里，将.pem文件拷贝覆盖到其节点容器目录，再次启动即可正常运行。
默认情况下，PXC8启用了SSL/TLS。
![image](https://github.com/OtakuBanana/docker/assets/14883112/6464f2da-eb73-46ad-a307-6a9df136bfbb)
当容器都正常运行后我们就可以测试连接了
![image](https://github.com/OtakuBanana/docker/assets/14883112/46658110-5806-4b0a-8c9d-55f3c51a3a80)
![image](https://github.com/OtakuBanana/docker/assets/14883112/37c95d92-fcef-4b92-8eec-97ae78cdd128)
修改任何一个数据库的内容会同步到其他数据库。

以上方式是在单主机docker上的部署例子，部署PXC如果出现访问相关的问题，可以参考官方文档，确认PXC需求的端口是否开放。
