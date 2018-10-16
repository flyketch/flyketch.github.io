## 如何搭建本地docker 镜像仓库

[参看地址](https://www.linuxidc.com/Linux/2018-03/151308.htm)

```
docker run -itd -v /data/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry --privileged=true registry:latest
```
Nice Man