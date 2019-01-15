### 一些常用的技巧命令

### Postgres

- 查看数据库连接的用户总数
```bash
select count(1) from pg_stat_activity;
```

- 查看所有连接的用户信息
```bash
select * from pg_stat_activity;
```

- 切换数据库
```bash
one=# \c two
```

### Vim

- vim 字符编码修改为utf-8

``` bash
vim ~/.vimrc

`then add`
set encoding=utf-8
set langmenu=zh_CN.UTF-8
language message zh_CN.UTF-8
```

### GreenPlum

- gpfdist 使用

[GreenPlum 集群 gpfdist 实战](https://blog.csdn.net/mchdba/article/details/72540806)
