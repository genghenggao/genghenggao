# Docker 修改使用国内镜像源

[TOC]

- 为加快拉取镜像速度，建议设置docker国内镜像源



## 1、国内镜像仓库

| 国内Docker镜像仓库名称 | 链接                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Docker 官方中国区      | [https://registry.docker-cn.com](https://registry.docker-cn.com/) |
| 网易                   | [http://hub-mirror.c.163.com](http://hub-mirror.c.163.com/)  |
| 中国科学技术大学       | [https://docker.mirrors.ustc.edu.cn](https://docker.mirrors.ustc.edu.cn/) |
| 阿里云                 | https://<你的ID>.mirror.aliyuncs.com                         |



## 2、修改docker镜像仓库配置

修改/etc/docker/daemon.json文件，如果没有先建一个即可

```shell
sudo vim /etc/docker/daemon.json
```



## 3、修改配置文件

```shell
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
```



## 4、使配置文件生效

```shell
sudo systemctl daemon-reload
```



## 5、重启Docker

```shell
sudo service docker restart
```



## 6、测试配置是否成功

```shell
docker search nginx
```