# Docker Compose
linux: centos

在Docker中,往往需要面临更复杂的情形,例如一个web服务往往需要同时启动nginx, mysql,等等多个相关服务. 通过docker compose管理多个服务

## Install Docker-Compose
```
# 已添加docker-ce repo可通过yum命令安装.
sudo yum install -y docker-compose
```

* [Docker Compoes安装参考](https://docs.docker.com/compose/install/)

## 编写docker-compose.yml
Docker Compose通过.yml文件管理服务,默认的文件名为docker-compose.yml. 示例:
```
version: "3.9"
services:
  web1:
    image: "demo-test:latest"
    ports:
      - "8093:8089"
  web2:
    image: "demo-test"
    ports:
      - "8094:8089"
```
1. services下定义服务名
2. 每个服务下分别定义该服务的镜像(image),端口(ports)


运行服务
```
# linux shell
sudo docker-compose up

```
异常情况:
```
ERROR: Couldn't connect to Docker daemon at http+docker://localunixsocket - is it running?

If it's at a non-standard location, specify the URL with the DOCKER_HOST environment variable.
#通过 sudo docker-compose解决
```

# 使用env file
通过env file可以在docerk-compose.yml中使用环境变量(env file提供的值).
示例:
```
version: '3'
services:
  web:
    image: "webapp:${TAG}"
```
env file示例:
```
TAG=v1.5
```
env file默认名为 .env放到docker-compose.yml同目录下, 如有多个envfile则可以通过--env-file指定路径. 命令示例:

```
sudo docker-compose --env-file ./env/dev up

# 默认情况, 将读取 .env文件
sudo docker-compose up
```
环境变量的其它配置
```
1. 直接通过environment声明
web:
  environment:
    - DEBUG=1

2. 指定env_file
env_file:
    - web-variables.env

3. 通过命令行传递
docker-compose run -e DEBUG=1 web python console.py
web:
  environment:
    - DEBUG
```

## Docker Compose extends
docker compose 允许多个compose yml相互调用.或者使用新compose file覆盖合并旧的文件.
示例:
```
docker-compose -f docker-compose.yml -f docker-compose.admin.yml
```
[Docker Compose File Extends](https://docs.docker.com/compose/extends/)