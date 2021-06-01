# Docker
在Docker中,Docker Engine是Docker的基础. Docker Engine通过容器进行隔离不同的进程,通过image管理版本启动容器.

# Docker Install
Linux: Centos 7
## Install to Centos
docker新版本改名为docker-ce,可通过yum search docker 确认是否有docker-ce的选项,没有可以通过添加仓库安装.
```
# 旧版,可能是默认repl仓库
 sudo yum install docker


# 添加docker 官方仓库安装
sudo yum install -y yum-utils
 sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce    

```
* [Docker Install](https://docs.docker.com/engine/install/centos/)

## 作为服务启动
```
sudo systemctl start docker
sudo systemctl enable docker
```


## Dockerfile
Docker通过Dockfile文件创建镜像(image),然后再通过image启动容器.很多服务例如mysql,nginx在DockerHub中都能够找到官方image, 如需定制自己的image则可以通过Dockerfile定制化自己的image.
Dockerfile以FORM开始, 可以包含多个阶段
```
FROM python:latest
ARG APP_VERSION=1.0
RUN echo hello
WORKDIR /app
ADD . .
COPY . .
RUN echo hello2
ENV APP_DIR=/app
ENTRYPOINT ["echo"]
CMD ["echo","hello3"]

FROM python:latest
....
```
1. FROM 指令初始化一个新的构建阶段
2. RUN 构建时运行命令,可以包含多个RUN步骤
3. WORKDIR 默认的工作路径
4. COPY 从当前构建路径复制文件到image中, 默认路径为WORKDIR
5. ADD 和COPY一样
6. CMD 启动容器时运行命令
7. ARG 指定变量, 不同阶段的同一变量需要重新声明ARG
8. ENTRYPOINT 用于指定启动命令, 和CMD共存且相互关联. 

* [Dockerfile 参考](https://docs.docker.com/engine/reference/builder/)

示例创建一个Dockerfile,启动一个python http服务
```
FROM python:latest
ENV PORT=8089
WORKDIR /app
COPY . .
RUN echo hello > index.html
CMD ["sh","-c","python -m http.server $PORT"]

```
shell:
```
# 在Dockerfile所在路径运行
docker build -t python-http-demo .
docker run -d -p8080:8089 python-http-demo
# 指定自己的路径
docker run -d -v /var/www/html:/app -p8080:8089 python-http-demo
```
* 需要注意的是, 指定"sh"命令时, "python -m http.server $PORT"是作为参数传递,要写到一起.


## Docker命令
```
# 构建
docker build 
-t 指定标签


# 通过image运行容器
docker run
-d 后台运行
-v path:container_path 挂载本地文件夹到容器中
-p port:container_port 映射端口到容器
```


* [Docker Hub](https://registry.hub.docker.com/)