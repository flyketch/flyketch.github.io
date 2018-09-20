## 编译jar 包

a、 编译时候没有跑测试
```
mvn clean package -Dmaven.test.skip=true
```
## 发布App

a、 指定端口
```
java -jar -Dserver.port=8090 app.jar
```
b、 指定配置环境
```
java -jar -Dspring.profiles.active=prod app.jar
```
c、 程序在后台运行
```
nohup java -jar app.jar > /dev/null 2>&1 &
```
d、 查看进程
```
ps -ef | grep app.jar
```
## 在cent os中创建service
a、 创建
```
cd /etc/systemd/system
vim app.service

[Unit]
Desciption=app
After=syslog.target.network.target

[Service]
Type=simple

ExecStart=/usr/bin/java -jar /opt/javaapps/app.jar
ExecStop=/bin/kill -15 $MAINPID

User=root
Group=root

[Install]
WantedBy=mutli-user.target
```
b、 使用
```
systemctl start app
```
c、 重新加载
```
systemctl daemon-reload
```
d、 停止
```
systemctl stop app
```
e、 开机启动
```
systemctl enable app
```
f、 取消开机启动
```
systemctl disable app
```


