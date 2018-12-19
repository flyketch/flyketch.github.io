## vagrant 和 gp5的一些基本命令

### vagrant 常用命令
![vagrant](/assets/images/vagrant.png)

### gp5 常用命令
```
gpstart     # 启动
gpstop     # 停止
gpstop -u     # 修改参数后，不用重启gp
gpstate     # 查看GP运行状态
gprecoverseg     # 恢复挂掉的节点
gprecoverseg -r     # 恢复节点的角色
```

### what's more

- 通过tpc-ds 可以生成gp测试数据，参考文章[TPC_DS](https://github.com/pivotalguru/TPC-DS)

- 通过gpcopy 来进行数据迁移

### gpcopy 使用时候注意点

- gpcopy 是在新的机器(需要迁移到的机器)上面进行操作的。

- gpcopy 需要在原来的机器(需要迁移的机器)上面修改`/data/master/gpseg-1/pg_hba.conf` 文件，添加下面一行，有访问权限
```
host  all   gpadmin   172.16.1.201/32    trust
```