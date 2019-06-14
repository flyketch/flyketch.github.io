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

### JavaScript

- js 循环遍历树行数据

[js实现无限层级树形数据结构](https://blog.csdn.net/Mr_JavaScript/article/details/82817177)

```js
function treeData(source, id, parentId, children){   
    let cloneData = JSON.parse(JSON.stringify(source))
    return cloneData.filter(father=>{
        let branchArr = cloneData.filter(child => father[id] == child[parentId]);
        branchArr.length>0 ? father[children] = branchArr : ''
        return father[parentId] == 0        // 如果第一层不是parentId=0，请自行修改
    })
}
```

- js 无限递归

[javascript当中的无限分类递归树,今天来重写一下](https://blog.csdn.net/jayhkw/article/details/68945087)

- es6 怎么优雅的实现从数组中的对象取值并返回新的数组

[ES6 怎么优雅的实现从数组中的对象取值并返回新的数组](https://segmentfault.com/q/1010000012302145/a-1020000012302361)

### Element UI

1、element ui 中tree 获取父节点信息

- [官方指南](https://element.eleme.cn/#/zh-CN/component/tree)

- [element tree根据子节点添加父级节点](http://www.imooc.com/wenda/detail/454697)

- [element-ui Tree控件, 如何获取父节点的ID](https://segmentfault.com/q/1010000015922387)

点击事件中添加信息

```
handleGroupClick(data, node) {
    console.log(data)
    console.log(node.parent.data.name)
}
```

2、element ui 中tree 自定义节点图标

- [elementui tree自定义节点图标](https://segmentfault.com/q/1010000015215077)

3、element ui 中tree 设置默认选中点

- [后台管理系统遇到的问题](https://www.jianshu.com/p/230c88a2c523)

```
menuIds.data.forEach(item => {
    this.$refs.tree.setChecked(item,true);
});
```

4、 ElementUI tree控件如何取得被选中的节点，以及父节点（即使没被全选）

[ElementUI tree控件如何取得被选中的节点](https://segmentfault.com/q/1010000012309004)


### Vue

- Vuex 详解

[VueJS中学习使用Vuex详解](https://segmentfault.com/a/1190000015782272)

- Vue 修改页面title

[VUE 单页面应用 修改页面title](https://segmentfault.com/a/1190000010139214)

- Vue 中组件传值

[Vue组件化及组件间传值](https://segmentfault.com/a/1190000011561859)

- Vue input 赋值后无法修改

原因： 没有赋初始值，赋初始值即可。


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
