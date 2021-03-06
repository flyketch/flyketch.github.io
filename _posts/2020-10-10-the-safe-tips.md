## 网站安全方面

- 将您的服务器配置为使用“Content-Security-Policy”头

```
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;
    # add header
    add_header Content-Security-Policy "default-src 'self' g.alicdn.com login.dingtalk.com login-pro.ding.zj.gov.cn 'unsafe-inline' 'unsafe-eval' blob: data:";
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";
    include /etc/nginx/conf.d/*.conf;
}
```
- 将每个第三方脚本/链接元素支持添加到 SRI(Subresource Integrity)

```
$ curl https://example.com/static/js/other/zepto.js | openssl dgst -sha256 -binary | openssl enc -base64 -A
```

### 参考资料

- [SRI-Subresource Integrity](https://blog.csdn.net/zccccoooo/article/details/79127269)

- [nginx解决内容安全策略CSP](https://blog.csdn.net/m0_46266503/article/details/108500504)
