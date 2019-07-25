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


### 附录

- conf/config.yaml

```
#
# This is the config file used for the docker images.
# It allows all users to do anything, so don't use it on production systems.
#
# Do not configure host and port under `listen` in this file
# as it will be ignored when using docker.
# see https://github.com/verdaccio/verdaccio/blob/master/wiki/docker.md#docker-and-custom-port-configuration
#
# Look here for more config file examples:
# https://github.com/verdaccio/verdaccio/tree/master/conf
#

# path to a directory with all packages
storage: /verdaccio/storage

auth:
  htpasswd:
    file: /verdaccio/conf/htpasswd
    # Maximum amount of users allowed to register, defaults to "+inf".
    # You can set this to -1 to disable registration.
    #max_users: 1000
security:
  api:
    jwt:
      sign:
        expiresIn: 60d
        notBefore: 1
  web:
    sign:
      expiresIn: 7d

# a list of other known repositories we can talk to
uplinks:
  npmjs:
    url: https://registry.npm.taobao.org/

packages:
  '@jota/*':
      access: $all
      publish: $all

  '@*/*':
    # scoped packages
    access: $all
    publish: $all
    proxy: npmjs

  '**':
    # allow all users (including non-authenticated users) to read and
    # publish all packages
    #
    # you can specify usernames/groupnames (depending on your auth plugin)
    # and three keywords: "$all", "$anonymous", "$authenticated"
    access: $all

    # allow all known users to publish packages
    # (anyone can register by default, remember?)
    publish: $all

    # if package is not available locally, proxy requests to 'npmjs' registry
    proxy: npmjs

# To use `npm audit` uncomment the following section
middlewares:
  audit:
    enabled: true

# log settings
logs:
  - {type: stdout, format: pretty, level: trace}
  #- {type: file, path: verdaccio.log, level: info}

# publish offline
publish:
  allow_offline: true
```

- conf/htpasswd

```
jpicado:$6vkdNgRX2npc:autocreated 2017-07-11T18:48:38.003Z
```

- docker-compose.yml

```
version: '3.0'
services:
  verdaccio:
    image: verdaccio/verdaccio
    restart: always
    container_name: verdaccio
    ports:
      - "4873:4873"
    volumes:
        - "./storage:/verdaccio/storage"
        - "./conf:/verdaccio/conf"
volumes:
  verdaccio:
    driver: local
```
