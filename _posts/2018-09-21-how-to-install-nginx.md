## 安装nginx

1、安装make
```
yum -y install gcc automake autoconf libtool make
```
2、安装gcc
```
yum install gcc gcc-c++
```
3、安装PCRE库
```
yum install pcre pcre-devel
```
4、安装zlib库
```
yum install zlib zlib-devel
```
5、安装openssl
```
openssl openssl-devel
```
6、安装nginx
```
wget http://nginx.org/download/nginx-1.6.2.tar.gz
tar zxvf nginx-1.6.2.tar.gz
cd nginx-1.6.2
./configure
make
make install
```
