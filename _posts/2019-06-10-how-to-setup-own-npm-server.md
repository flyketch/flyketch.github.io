### 使用verdaccio docker 搭建npm 私有仓库

参考链接：

- [npm私有仓库 配置verdaccio在docker环境](https://www.cnblogs.com/huangenai/p/10006176.html)

- [使用verdaccio的docker镜像搭建npm私服](https://blog.csdn.net/s8460049/article/details/82191702)

- [使用Verdaccio搭建npm仓库](http://ju.outofmemory.cn/entry/338244)

- [can't publish a private package to verdaccio while offline](https://github.com/verdaccio/verdaccio/issues/78)

注意点说明：

- 1、在内网中使用时候，需修改conf/config.yaml , 添加offline

```
# publish offline
publish:
  allow_offline: true
```

- 2、docker 运行时候修改verdaccio 权限

```
docker exec -it container_id /bin/sh
whoami & id
chown -R uid:gid verdaccio
```

- 3、客户端使用publish 时候记得先登录

```
npm login
username: jpicado
password: jpicado
```
### 使用nexus 搭建npm 私有服务器

- [简书](https://www.jianshu.com/p/1674a6bc1c12)

```
docker run -d --name nexus3 \
 --restart=always \
-p 8081:8081 \
-v /opt/nexus-data:/nexus-data \
sonatype/nexus3
```

### 一些问题

- [安装后出现silly decomposeActions install chalk@1.1.3](https://stackoverflow.com/questions/46043697/error-while-installing-bootstrap-4-beta-error-code-4048)
