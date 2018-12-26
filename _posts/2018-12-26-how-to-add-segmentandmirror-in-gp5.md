## gp5 如何拓展segment 和 mirror 节点

## 增加segement 节点

- 1、通过vagrant 新增一台虚拟机sdw3

- 2、配置虚拟机环境，包括如下环境
`ntp` `sestatus` `firewalld` `estab` 等等
具体参考 安装greenplum 时候环境配置

- 3、修改集群 hosts 文件，添加新增的hosts

- 4、创建文件newseg，添加内容
```
sdw3
```

- 5、打通节点之间SSH
```
gpssh-exkeys -f /home/gpadmin/gpconfig/hostlist
```

- 6、安装greenplum
```
gpseginstall -f /home/gpadmin/gpconfig/newseg
```

- 7、在master 通过gpexpend 生成配置文件，指定数据库
```
gpexpand -f newseg -D one
```

- 8、通过生成的配置文件初始化segment
```
gpexpand -i gpexpand_inputfile_20181226_074521 -D one
```

### tips
- 1、 gpexpend失败了则回滚
```
gpexpand --rollback -D one
```

### 创建mirror 节点

- 1、删除hosts 文件中对应的 127.0.0.1， such as
```
127.0.0.1	sdw1	sdw1
```

- 2、通过gpaddmirrors 来生成mirror 节点文件
```
gpaddmirrors -o filename
```

- 3、添加mirror 节点
```
gpaddmirrors -i mirror_config_file
```

### 参考文章
- 1、英文文档

[gpexpend](https://gpdb.docs.pivotal.io/43270/admin_guide/expand/expand-initialize.html)
[gpaddmirrors](https://gpdb.docs.pivotal.io/43270/admin_guide/highavail/topics/g-enabling-segment-mirroring.html)

- 2、中文文档

[gpexpend](https://gp.stage.vonbros.com/docs/admin_guide/expand/expand-initialize.html)
[gpaddmirrors](https://gp.stage.vonbros.com/docs/admin_guide/highavail/topics/g-enabling-segment-mirroring.html)

[csdn add segement](https://blog.csdn.net/dazuiba008/article/details/65440748)

[扩展计算节点时偶遇 gpexpand 出错](https://blog.csdn.net/wxc20062006/article/details/53126076)

