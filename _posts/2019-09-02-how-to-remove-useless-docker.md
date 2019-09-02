## 如何删除无用的docker 容器以及镜像

```bash
#!/bin/bash

# reomve containers

docker rm `docker ps -a | grep Created | awk '{print $1}'`

# remove docker images

docker rmi -f `docker images | grep '<none>' | awk '{print $3}'`

```