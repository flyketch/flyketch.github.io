## 如何搭建Yii 2高级项目模板

### 1、下载yii2 包管理工具composer
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```
如果已经安装composer则通过
```
composer self-update
```
来进行更新composer

### 2、通过composer创建项目
```
composer create-project --prefer-dist yiisoft/yii2-app-advanced yii-application
```
创建项目完成后在项目目录下执行
```
php init
```
来初始化项目允许环境。
初始化完成后创建pg数据库

### 3、创建postgres 数据库
```
docker run --name yii2pg -e POSTGRES_PASSWORD=123456789 -p 54321:5432 -d postgres
```
此时用户名为postgres, 数据库为postgres。
在common/config/main-local.php中
配置数据库信息
```
'db' => [
    'class' => 'yii\db\Connection',
    'dsn' => 'pgsql:host=localhost;port=54321;dbname=postgres',
    'username' => 'postgres',
    'password' => '123456789',
    'charset' => 'utf8',
],
```
数据库信息配置完成后，通过
```
php yii migrate
```
来创建数据库信息。

### 4、创建nginx 服务器以及php允许环境
创建nginx服务器, 我们使用docker-compose的方式来进行创建
```
yii2-service:
    image: nginx
    ports: ["80:80"]
    volumes: ["../yii-application:/var/yii2/","./nginx-yii.conf:/etc/nginx/conf.d/default.conf"]
    command: /bin/bash -c "nginx -g 'daemon off;'"
```
以及nginx-yii.conf
```
server {
    listen 80;
    server_name localhost;

    set $base_root /var/yii2;
    root $base_root;

    #error_log /var/log/nginx/advanced.local.error.log warn;
    #access_log /var/log/nginx/advanced.local.access.log main;
    charset UTF-8;
    index index.php index.html;

    location / {
        root $base_root/frontend/web;
        try_files $uri $uri/ /frontend/web/index.php$is_args$args;

        # omit static files logging, and if they don't exist, avoid processing by Yii (uncomment if necessary)
        #location ~ ^/.+\.(css|js|ico|png|jpe?g|gif|svg|ttf|mp4|mov|swf|pdf|zip|rar)$ {
        #    log_not_found off;
        #    access_log off;
        #    try_files $uri =404;
        #}

        location ~ ^/assets/.+\.php(/|$) {
            deny all;
        }
    }

    location /admin {
        alias $base_root/backend/web/;

        # redirect to the URL without a trailing slash (uncomment if necessary)
        #location = /admin/ {
        #    return 301 /admin;
        #}

        # prevent the directory redirect to the URL with a trailing slash
        location = /admin {
            # if your location is "/backend", try use "/backend/backend/web/index.php$is_args$args"
            # bug ticket: https://trac.nginx.org/nginx/ticket/97
            try_files $uri /backend/web/index.php$is_args$args;
        }

        # if your location is "/backend", try use "/backend/backend/web/index.php$is_args$args"
        # bug ticket: https://trac.nginx.org/nginx/ticket/97
        try_files $uri $uri/ /backend/web/index.php$is_args$args;

        # omit static files logging, and if they don't exist, avoid processing by Yii (uncomment if necessary)
        #location ~ ^/admin/.+\.(css|js|ico|png|jpe?g|gif|svg|ttf|mp4|mov|swf|pdf|zip|rar)$ {
        #    log_not_found off;
        #    access_log off;
        #    try_files $uri =404;
        #}

        location ~ ^/admin/assets/.+\.php(/|$) {
            deny all;
        }
    }

    location ~ ^/.+\.php(/|$) {
        rewrite (?!^/((frontend|backend)/web|admin))^ /frontend/web$uri break;
        rewrite (?!^/backend/web)^/admin(/.+)$ /backend/web$1 break;

        fastcgi_pass 127.0.0.1:9000; # proxy requests to a TCP socket
        #fastcgi_pass unix:/var/run/php/php7.0-fpm.sock; # proxy requests to a UNIX domain socket (check your www.conf file)
        fastcgi_split_path_info ^(.+\.php)(.*)$;
        include /etc/nginx/fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        try_files $fastcgi_script_name =404;
    }

    location ~ /\. {
        deny all;
    }
}
```
将项目目录和nginx文件分别挂在/var/yii2/ 以及/etc/nginx/conf.d/default.conf下
docker-compose 起来后，进入nginx容器内，安装php环境
```
apt-get update
apt-get install php
apt-get install php7.0-fpm
```
安装完成后，访问localhost 会出现502错误
解决方法参照stackoverflow[nginx: connect() failed (111: Connection refused) while connecting to upstream
](https://stackoverflow.com/questions/21524373/nginx-connect-failed-111-connection-refused-while-connecting-to-upstream)

### 参考文章
1、[github](https://github.com/mickgeek/yii2-advanced-one-domain-config)

2、[yii2](https://www.yiiframework.com/wiki/799/yii2-app-advanced-on-single-domain-apache-nginx)