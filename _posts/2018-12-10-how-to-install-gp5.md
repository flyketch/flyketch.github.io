## 如何在本地部署GreenPlum 5 database

### 1、虚拟机方式

a、这里使用 vagrant,来统一管理, 下载安装vagrant, 使用vagrant add box 添加新的centos 7虚拟机。

b、通过vagrant init 生成Vagrantfile
```
Vagrant.configure("2") do |config|
  config.vm.box = "centos7"

  config.vm.define "mdw" do |mdw|
    mdw.vm.network "private_network", ip: "192.168.56.101"
  end

  config.vm.define "sdw1" do |s|
    s.vm.network "private_network", ip: "192.168.56.102"
  end

  config.vm.define "sdw2" do |s|
    s.vm.network "private_network", ip: "192.168.56.103"
  end
end
```

c、通过vagrant up启动虚拟机。

后续参考[rz1970](https://rz1970.github.io/2018/04/16/greenplum-deployment.html)


### 2、Docker方式
参考文章[rz1970](https://rz1970.github.io/2018/12/07/deploy-greenplum-with-docker.html)

需要注意的是，在
```
gpseginstall -f /home/gpadmin/gpconfig/seglist
```
完成后要添加软链接。
```
[gpadmin@4197592bf6c0 ~]$ gpssh -f gpconfig/seg-all
=> pwd
[sdw1] /home/gpadmin
[sdw2] /home/gpadmin
=> ls
[sdw1] greenplum-db-5.14.0  greenplum-db-5.14.0.tar
[sdw2] greenplum-db-5.14.0  greenplum-db-5.14.0.tar
=>
=> ln -s greenplum-db-5.14.0 greenplum-db
[sdw1]
[sdw2]
```

参考文章[静心docker安装greenplum集群](https://gitop.gitee.io/blog/post/install-greenplum-in-docker/)

