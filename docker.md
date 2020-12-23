docker常用命令

docker images 查看本地拥有的镜像
docker run -it ubuntu
docker stop containerName/containerId 停止运行指定容器
docker ps .   查看在运行的容器
docker logs  containerName/containerId 查看容器运行日志
exit
cat /proc/version
docker search httpd 查找镜像
docker  rm  containerName/containerId 删除镜像

docker pull 抽取镜像

docker run -d 
//在使用 -d 参数时，容器启动后会进入后台。不会进入容器
此时想要进入容器，可以通过以下指令进入：docker attach
docker exec：推荐大家使用 docker exec 命令，因为此退出容器终端，不会导致容器的停止。//如果从这个容器退出，不会导致容器的停止，这就是为什么推荐大家使用 docker exec 的原因。

docker export
docker import

docker network ls 查看docker 网络

Docker的CentOS镜像由于做了精简，去掉了 ping 命令， centos 使用 yum install iputils 安装包含ping的工具包
control+d 退出docker
因为control+c 是中止其他命令的执行的。
更新镜像
更新镜像之前，我们需要使用镜像来创建一个容器。
docker run -t -i ubuntu:15.10 /bin/bash
root@e218edb10161:/# 
-i: 交互式操作。
-t: 终端。
ubuntu:15.10: 这是指用 ubuntu 15.10 版本镜像为基础来启动容器。
/bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。
在运行的容器内使用 apt-get update 命令进行更新。
在完成操作之后，输入 exit 命令来退出这个容器。
此时 ID 为 e218edb10161 的容器，是按我们的需求更改的容器。我们可以通过命令 docker commit 来提交容器副本。
runoob@runoob:~$ docker commit -m="has update" -a="runoob" e218edb10161 runoob/ubuntu:v2
sha256:70bf1840fd7c0d2d8ef0a42a817eb29f854c1af8f7c59fc03ac7bdee9545aff8
各个参数说明：
-m: 提交的描述信息
-a: 指定镜像作者
e218edb10161：容器 ID
runoob/ubuntu:v2: 指定要创建的目标镜像名


###运行docker指令前要先打开docker应用！！