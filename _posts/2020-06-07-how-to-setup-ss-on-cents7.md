### centos 上面配置Shadowsocks 服务

1、安装pip
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py

2、安装配置shadowsocks
pip install --upgrade pip
pip install shadowsocks
安装完成后，创建配置文件/etc/shadowsocks.json，内容如下：
{
"server": "0.0.0.0",
"server_port": 8080,
"local_address": "127.0.0.1",
"local_port": 1080,
"password": "password",
"timeout": 600,
"method": "aes-256-cfb"
}

- method 可有多种选择

2.1
#启动
ssserver -c /etc/shadowsocks.json -d start
#停止
ssserver -c /etc/shadowsocks.json -d stop
#重启
ssserver -c /etc/shadowsocks.json -d restart

#查看是否成功启动
ps -ef | grep shad

3、配置自启动
创建配置文件/etc/systemd/system/shadowsocks.service，内容如下：
```
[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target
```

执行以下命令启动shadowsocks：
systemctl enable shadowsocks
systemctl start shadowsocks

检查服务是否启动成功：
systemctl status shadowsocks -l

启动成功

```
shadowsocks.service - Shadowsocks
   Loaded: loaded (/etc/systemd/system/shadowsocks.service; enabled; vendor preset: disabled)
   Active: active (running) since 日 2020-06-07 12:24:57 CST; 2s ago
 Main PID: 2254 (ssserver)
   CGroup: /system.slice/shadowsocks.service
           └─2254 /usr/bin/python /usr/bin/ssserver -c /etc/shadowsocks.json
```

4、centos7用的firewalld，若不进行设置，可能会导致SS无法使用，如果是阿里云服务器，则可以在阿里云管理后台设置安全组；
```
# 开放端口
$ firewall-cmd --permanent --add-port=8080/tcp 
# 修改规则后需要重启
$ firewall-cmd --reload 
```