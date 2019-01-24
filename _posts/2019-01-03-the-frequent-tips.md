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

- 显示查询时间
```bash
six=# \timing on 
default off
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

- gpload 使用
[gpload 简介](https://gp-docs-cn.github.io/docs/utility_guide/admin_utilities/gpload.html)
[Greenplum使用gpload通过gpfdist实现文件的高速加载](https://blog.csdn.net/jiangshouzhuang/article/details/51817520)

### Shell

- 更改文件里面空格为 |
```bash
sed -i 's/\s\+/|/g' filename
```

- linux查看文件有多少行
```bash
wc -l filename
```