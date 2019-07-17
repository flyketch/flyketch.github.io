## 如何搭建owncloud 私有服务器

### 使用docker-compose

```
version: '3'
services:
  owncloud:
    image: owncloud
    volumes:
      - "/Users/steve/Workspaces/docker/owncloud/owndata:/var/www/html/data"
    ports:
      - 5679:80
    depends_on:
      - mysql
  mysql:
    image: mysql:5.7
    volumes:
      - "/Users/steve/Workspaces/docker/owncloud/dbdata:/var/lib/mysql"
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: "123456789"
      MYSQL_DATABASE: owncloud
```

### 如何配置

- 浏览器进入127.0.0.1:5679，用户名密码随意设置，数据库选择mysql，依次输入

```
root
123456789
owncloud
mysql
```

重新登录即可

### tips

数据库选用mysql 5.7 版本