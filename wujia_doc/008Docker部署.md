# 总项目

[TOC]

## 1. 创建项目文件夹

- 在目录`/usr/local`下创建

```
mkdir wjproject_docker
```

![](D:\henggao2021\IMG\微信截图_20210704155555.png)

## 2. 创建Docker compose

- 在`wjproject_docker`目录下创建`compose`

  ```
  mkdir compose
  ```

  ![](D:\henggao2021\IMG\微信截图_20210704171840.png)

## 3.项目开发



## 4. 构建 Django 容器

- 在Django项目根目录下创建Dockerfile文件，**注意D大写**

  ```
  touch Dockerfile
  ```

  ![](D:\henggao2021\IMG\微信截图_20210704173022.png)

- 基础镜像

- 项目镜像



```
FROM python:3.8    # 选择基础镜像,这里的基础镜像也可以选择ubuntu,centos等，但是下面的配置就会发生变化

# 创建工作目录
RUN mkdir /blog  

#设置工作目录
WORKDIR /blog

#将当前目录加入到工作目录中
ADD . /blog
RUN pip3 install -r requirements.txt
#对外暴露端口
EXPOSE 80 8080 8000 5000
#设置环境变量
ENV SPIDER=/blog
```



## 目录参考

```
myproject_docker # 项目根目录
 ├── compose # 存放各项容器服务的Dockerfile和配置文件
 │   ├── mysql
 │   │   ├── conf
 │   │   │   └── my.cnf # MySQL配置文件
 │   │   └── init
 │   │       └── init.sql # MySQL启动脚本
 │   ├── nginx
 │   │   ├── Dockerfile # 构建Nginx镜像所的Dockerfile
 │   │   ├── log # 挂载保存nginx容器内nginx日志
 │   │   ├── nginx.conf # Nginx配置文件
 │   │   └── ssl # 如果需要配置https需要用到
 │   ├── redis
 │   │   └── redis.conf # redis配置文件
 │   └── uwsgi # 挂载保存django+uwsgi容器内uwsgi日志
 ├── docker-compose.yml # 核心编排文件
 └── myproject # 常规Django项目目录
    ├── Dockerfile # 构建Django+Uwsgi镜像的Dockerfile
    ├── apps # 存放Django项目的各个apps
    ├── manage.py
    ├── myproject # Django项目配置文件
    │   ├── asgi.py
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── pip.conf # 非必需。pypi源设置成国内，加速pip安装
    ├── requirements.txt # Django项目依赖文件
    ├── start.sh # 启动Django+Uwsgi容器后要执行的脚本
    ├── media # 用户上传的媒体资源与静态文件
    ├── static # 项目所使用到的静态文件
    └── uwsgi.ini # uwsgi配置文件
```

- 