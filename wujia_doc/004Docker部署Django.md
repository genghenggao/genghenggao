# Docker部署Django



## 前言

1. 在Docker与virtualenv或pipenv的区别
   - virtualenv或pipenv创建的虚拟环境只是隔离了一个python运行的虚拟环境，允许不同的项目使用不同版本的程序包，从而解决依赖性问题。Docker的每个容器更像一个小型的linux系统，可以有自己的IP地址，容器相互之前环境隔离地更彻底。我们不仅可以把python的第三方依赖包放在一个容器里，我们还可以把数据库比如MySQL或Redis也放在容器里，这是python虚拟环境做不到的。因此生产环境使用Docker部署Django时，你不再需要使用virtualenv或pipenv创建python虚拟环境。
2. 在Docker镜像与容器之前的关系
   - Docker容器是由docker镜像创建的运行实例。简单来说，镜像是文件，容器是进程。它们之前的关系如同Python的类与实例化对象之前的关系，一个镜像可以对应多个容器。
3. 使用Docker技术的基本流程
   - 我们首先要使用`docker pull`命令或Dockerfile文件构建docker镜像，再使用`docker run`命令创建容器，最后使用`docker exec -it`命令进入容器执行其它命令。
4. 宿主机和容器间的通信
   - 安装Docker的服务器就是宿主机，宿主机有固定的IP地址和完整的操作系统比如Centos或Ubuntu。前面已经提到过每个容器像一个极简的Linux系统，还可以有自己的IP地址(Docker分配的)。宿主机和容器之间是可以通过`docker cp`或目录挂载的方式通信的。





## Django常见的两种部署方式：

1. Django + Nginx + uWSGI
2. Django+ Nginx + Gunicorn



