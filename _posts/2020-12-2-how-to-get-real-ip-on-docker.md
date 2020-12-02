## 如何在docker 环境下面获取用户真实IP

### First

> 修改Nginx配置文件，docker容器内【/etc/nginx/conf.d/default.conf】

```
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /web;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #

    location /api/ {
        proxy_pass   http://base-framework-server/;
        #下边是为获取真实IP所做的设置
        proxy_set_header    X-Real-IP        $remote_addr;
        proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header    HTTP_X_FORWARDED_FOR $remote_addr;
        proxy_set_header    X-Forwarded-Proto $scheme;
        proxy_redirect      default;
    }

}
```

### Second

> 修改Nginx配置文件，docker容器内【/etc/nginx/conf.d/default.conf】

```
location / {
    proxy_set_header            Host $host;
    proxy_set_header            X-real-ip $remote_addr;
    proxy_set_header            X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

`OR`

```
location / {
    proxy_set_header            Host $host;
    set $Real $proxy_add_x_forwarded_for;
    if ( $Real ~ (\d+)\.(\d+)\.(\d+)\.(\d+),(.*) ){
        set $Real $1.$2.$3.$4;
    }
    proxy_set_header            X-real-ip $Real;
    proxy_set_header            X-Forwarded-For $proxy_add_x_forwarded_for;
}
```
