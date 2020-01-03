## Ubuntu 下面安装shadowsockets


### 安装shadowsockets

```
sudo apt install python-pip
sudo apt install python-setuptools m2crypto -y
sudo pip install shadowsocks
```

### 安装最新包

```
sudo pip install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U
```
### 编辑配置文件
```
vi /etc/shadowsockets.json

{
  "server":"11.22.33.44",
  "server_port":50003,
  "local_port":1080,
  "password":"123456",
  "timeout":600,
  "method":"aes-256-cfb"
}
```

### 启动服务

```
sslocal -c /etc/shadowsockets.json
```

### 最后在浏览器上面配置信息即可使用了