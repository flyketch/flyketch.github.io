## 如何搭建rancher server 服务

### rancher 是什么

参考网站

[中文网站](https://www.cnrancher.com/docs/rancher/v2.x/cn/overview/)

### 搭建rancher server 服务

```
docker run -d --restart=unless-stopped -p 8080:8080 rancher/server
```