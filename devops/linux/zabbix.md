# Zabbix

## Install
### 1. install docker
### 2. use quick start shell run zabbix-mysql-server. verify your server ip and start containter.
```
#!/bin/bash
pwd=`pwd`

DB_SERVER_HOST=192.168.0.141
MYSQL_DATABASE=zabbix
MYSQL_USER=root
MYSQL_PASSWORD=root
MYSQL_ROOT_PASSWORD=root
PHP_TZ=Asia/Shanghai

docker run --rm --name zabbix-server-mysql -t \
      -e DB_SERVER_HOST=$DB_SERVER_HOST \
      -e MYSQL_DATABASE=$MYSQL_DATABASE \
      -e MYSQL_USER=$MYSQL_USER \
      -e MYSQL_PASSWORD=$MYSQL_PASSWORD \
      -e MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD \
      -p 10051:10051 \
      -v $pwd/zabbix:/zabbix \
      -d zabbix/zabbix-server-mysql:latest > console-server.log &2>&1 &

```

### 3. use shell run zabbix-web-nginx.
```
DB_SERVER_HOST=192.168.0.141
MYSQL_DATABASE=zabbix
MYSQL_USER=root
MYSQL_PASSWORD=root
MYSQL_ROOT_PASSWORD=root

ZBX_SERVER_HOST=192.168.0.141
ZBX_SERVER_PORT=10051

PHP_TZ=Asia/Shanghai
docker run --rm -d --name zabbix-web-nginx-mysql -t \
      -e DB_SERVER_HOST=$DB_SERVER_HOST \
      -e MYSQL_DATABASE=$MYSQL_DATABASE \
      -e MYSQL_USER=$MYSQL_USER \
      -e MYSQL_PASSWORD=$MYSQL_PASSWORD \
      -e MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD \
      -e ZBX_SERVER_HOST=$ZBX_SERVER_HOST \
      -e ZBX_SERVER_PORT=$ZBX_SERVER_PORT \
      -e PHP_TZ=$PHP_TZ \
      --link zabbix-server-mysql \
      -p 8080:8080 \
      -d zabbix/zabbix-web-nginx-mysql:latest >console-web.log &2>&1 &

```
### 4. Install Zabbix Agent. 
```
# example centos 7
rpm -Uvh https://repo.zabbix.com/zabbix/5.2/rhel/7/x86_64/zabbix-release-5.2-1.el7.noarch.rpm
yum install zabbix-agent

```
### 5. Run Zabbix Agent.
```
systemctl restart zabbix-agent
```


* [Zabbix Agent Package download](https://www.zabbix.com/download?zabbix=5.2&os_distribution=red_hat_enterprise_linux&os_version=8&db=mysql)

### 5. Other manual
* [Zabbix中文文档](https://www.zabbix.com/documentation/3.4/zh/manual/config/triggers/trigger)
* [Zabbix Install for docker](https://www.zabbix.com/documentation/current/manual/installation/containers)


## Use
在确保已经启动了服务端(Zabbix-server 和 zabbix-web)后, 可以通过访问浏览器访问ip:8080 (脚本里映射的端口) 进入到web管理界面.然后你可以通过以下流程学习使用zabbix.
1. 修改语言, 左下角User Settings, 修改Language为Chinese(zh_CN).
2. 添加一台主机,并正确设置主机IP和端口
```
- 设置主机名称
- 设置群组,选择一个默认的
- 在Intefaces,中选择客户端(agent), 并设置主机ip和端口(agent端口,默认10050)
- 确认添加
```
3. 添加一个监控项,并测试可达. 监控项是通过命令获取数据,例如: 内存占用,CPU占用等各自有命令(键值keyword)可以获取
```
- 进入到添加的主机,选择监控项(item),点击右上角-创建监控项.
- 输入名称
- 选择类型为Zabbix 客户端,也就是Zabbix agent.
- 选择一个键值, 这里的键值就是一个内置的命令, 这里我们选择agent.version 用于查看主机安装的 agent的版本.
- 信息类型选文本
- 选择最下方的-测试按钮,然后单击测试. 如果已经正确的设置了目标主机,这里可以看到值为agent的版本号.

```
4.  配置触发器(Trigger), 触发器可以通过监控项获取的值判断状态.在触发器配置表达式,从而判断状态是否正常.

5. 动作(Action), 通过Action可以再触发器获取到异常状态时,发送邮件或信息给运维人员.需要注意的事,运维人员需要有对应主机的访问权限,才能收到邮件.主机权限在用户组中配置.