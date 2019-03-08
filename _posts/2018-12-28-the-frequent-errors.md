### 常见的错误结合

## 1、yum 安装软件时候报错

### *<font color='#e4e'>问题描述</font>*

```bash
[root@gpstage1 ~]# yum install -y perl
ImportError: No module named site
```

### *<font color='green'>解决方案</font>*

```bash
unset PYTHONPATH

## to use the system default ##
unset PYTHONHOME  
```

### 参考文章

- 1、[yum error](https://unix.stackexchange.com/questions/295116/yum-error-no-module-named-site)

## 2、防火墙开启后，docker 间不能通信

- [答案](https://unix.stackexchange.com/questions/199966/how-to-configure-centos-7-firewalld-to-allow-docker-containers-free-access-to-th)

- [答案](https://www.google.com.hk/search?q=firewalld+start+docker-compose&oq=firewalld+start+docker-compose&aqs=chrome..69i57.19951j0j1&sourceid=chrome&ie=UTF-8)