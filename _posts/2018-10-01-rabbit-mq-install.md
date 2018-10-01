## docker 下安装rabbit mq

### 1、搜索
访问hub.docker.com 搜索rabbitmq，选择最新的版本，注意版本后面加了-management 的是带后台管理页面的。

### 2、安装
这里以3.7.8-management 版本为例
```
docker run -d --hostname my-rabbit -p 5672:5672 -p 15672:15672 rabbitmq:3.7.8-management
```