## 如何使用docker 搭建gitlab 服务

### 使用docker-compose 进行搭建

```
version: '3'
services:
    gitlab:
      image: 'gitlab/gitlab-ce:latest'
      restart: always
      hostname: '127.0.0.1'
      environment:
        TZ: 'Asia/Shanghai'
        GITLAB_OMNIBUS_CONFIG: |
          external_url 'http://127.0.0.1:9090'
          # gitlab_rails['time_zone'] = 'Asia/Shanghai'
          # 需要配置到 gitlab.rb 中的配置可以在这里配置，每个配置一行，注意缩进。
          # 比如下面的电子邮件的配置：
          # gitlab_rails['smtp_enable'] = true
          # gitlab_rails['smtp_address'] = "smtp.exmail.qq.com"
          # gitlab_rails['smtp_port'] = 465
          # gitlab_rails['smtp_user_name'] = "xxxx@xx.com"
          # gitlab_rails['smtp_password'] = "password"
          # gitlab_rails['smtp_authentication'] = "login"
          # gitlab_rails['smtp_enable_starttls_auto'] = true
          # gitlab_rails['smtp_tls'] = true
          # gitlab_rails['gitlab_email_from'] = 'xxxx@xx.com'
      ports:
        - '9090:9090'
        - '2422:22'
        - '8443:443'
      volumes:
        - /Users/steve/Workspaces/docker/gitlab/config:/etc/gitlab
        - /Users/steve/Workspaces/docker/gitlab/data:/var/opt/gitlab
        - /Users/steve/Workspaces/docker/gitlab/logs:/var/log/gitlab
```