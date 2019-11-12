## 如何使用ntp 服务

1、下载ntp

```
yum install -y ntp
```

2、修改ntp配置

```
vi /etc/ntp.conf

server ip_addr
fudge ip_addr stratum 10

systemctl enable ntpd
systemctl start ntpd

ntpdate -u ip_addr
ntpstat
timedatectl
```