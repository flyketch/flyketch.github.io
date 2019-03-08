## 如何配置CI流程

- [官网地址](https://concoursetutorial.com/)

- CI 需要先登录

```
fly -t ci login
fly -t ci set-pipeline -p flyketch -c flyketch_pipeline.yml
```

- tips
内网访问一般先把github 代码down 到A服务器，然后部署的B服务器从A服务器拷贝代码