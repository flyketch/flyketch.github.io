## 安装cent os 7.3

1、访问cent os 官网下载[下载地址](https://www.centos.org/download/)

2、用UltraISO 制作启动盘进行安装

3、安装时候，我们选择最小化安装。

## 配置OS 环境

1、java 环境

a. 在oracle 官网下载jdk1.8.1.rpm 

b. 安装rpm文件
```
rpm -ivh jdk-8u181-linux-x64.rpm
```
c. 配置Java 环境变量

```
vim /etc/profile 

export JAVA_HOME=/usr/java/jdk1.8.0_102/
export PATH=$PATH:$JAVA_HOME
```

## 安装docker

参考runoob.com的教程[地址](http://www.runoob.com/docker/centos-docker-install.html)

补充docker 自动启动
```
systemctl enable docker
```

补充创建mysql 数据库时候指定Database-Encoding 为
utf8mb4

## 配置centos7对外开放端口

参考CSDN 的一篇文章[地址](https://blog.csdn.net/xingyue425/article/details/53911479)

## 启动项目
```
java -jar app.jar
```