### 如何部署eureka 集群

1、部署好eureka 服务

2、添加Docker 文件 

- build.sh

```
#!/usr/bin/env bash

mvn clean package -Dmaven.test.skip=true -U

docker build -t springeureka .
```

- Dockerfile

```
FROM java:8-alpine

ADD target/*.jar app.jar

EXPOSE 8761

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

3、执行命令

```bash
bash build.sh
```

4、配置docker-compose.yml

```
version: '3.1'
services:
  eureka-1:
    restart: always
    image: springeureka
    container_name: eureka-1
    ports:
      - 8761:8761

  eureka-2:
    restart: always
    image: springeureka
    container_name: eureka-2
    ports:
      - 8762:8761
```

5、启动docker-compose