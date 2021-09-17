# Docker



- 容器

- 镜像



## 命令

```shell
# 查看所有镜像
docker images -a

# 删除镜像
docker rm 容器id

# 运行的容器
docker ps

# 重启Docker
 systemctl restart  docker
 
 # 关闭Docker，但docker.socket仍在运行
 systemctl stop docker
```



## 项目目录结构参考

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

