## 如何搭建Jenkins 服务器


### 使用docker-compose 进行搭建

```
version: "3"
services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    restart: always
    user: root
    hostname: '127.0.0.1'
    ports:
      - '8090:8080'
      - '50000:50000'
      - '9000:9000'
    privileged: true
    volumes:
      - '/home/docker/jenkins:/var/jenkins_home'
      - '/home/docker/apache-maven-3.6.1:/var/maven_home'
    environment:
      - TZ=Asia/Shanghai
```