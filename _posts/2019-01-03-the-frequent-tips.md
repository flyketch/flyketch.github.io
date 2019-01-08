### 一些常用的技巧命令

### Postgres

- 查看数据库连接的用户总数
```
select count(1) from pg_stat_activity;
```

- 查看所有连接的用户信息
```
select * from pg_stat_activity;
```

### Vim

- vim 字符编码修改为utf-8

``` bash
vim ~/.vimrc

`then add `
set encoding=utf-8
set langmenu=zh_CN.UTF-8
language message zh_CN.UTF-8
```
