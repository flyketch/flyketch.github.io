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