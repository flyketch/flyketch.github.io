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

- 修改一列数据为小写
```bash
update table_name set column=lower(column);
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

### Vue

- Vuex 详解

[VueJS中学习使用Vuex详解](https://segmentfault.com/a/1190000015782272)

- Vue 修改页面title

[VUE 单页面应用 修改页面title](https://segmentfault.com/a/1190000010139214)

- Vue 中组件传值

[Vue组件化及组件间传值](https://segmentfault.com/a/1190000011561859)


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

- linux 软链接
ln -s 源文件 目标文件

### Jekyll

- 安装Gemfile 文件依赖

```
bundle install
```

- 启动Jekyll 项目

```
jekyll serve

or

bundle exec jekyll serve
```

### wordpress

- wordpress 升级https 证书后访问

修改wp-config.php 文件，添加如下代码

```
if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
    $_SERVER['HTTPS'] = 'on';
}
```

### Idea

- Idea 常用快捷键

[IntelliJ Idea 常用快捷键列表](https://www.cnblogs.com/zhangpengshou/p/5366413.html) 
