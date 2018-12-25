## 物理机如何安装postgres 以及连接postgres 数据库

### 本例子安装的是postgres 10

- 1、下载postgres源码文件，[地址](https://www.postgresql.org/ftp/source/)，选择v10.1 版本

- 2、解压文件
```
gunzip postgresql-10.1.tar.gz
tar xf postgresql-10.1.tar
```
- 3、进入postgresql-10.1 文件夹进行检测安装
```
./configure
```
- 4、进行编译
```
make
```
- 5、安装文件
```
make install
```
- 6、安装完成后，设置共享库 和 环境变量
##### a、共享库

```
vi ~/.bash_profile

LD_LIBRARY_PATH=/usr/local/pgsql/lib
export LD_LIBRARY_PATH
```

##### b、环境变量

```
vi ~/.bash_profile

PATH=/usr/local/pgsql/bin:$PATH
export PATH
export PGDATA="$HOME/pgsql"
```

- 7、初始化数据库

```
initdb
```

### 连接postgres 数据库

- 1、修改PGDATA 目录下的pg_hba.conf 文件，添加

```
host    all             all             192.168.3.0/24          trust
```

上面规则可参考[文章](https://blog.csdn.net/u010936475/article/details/52729605)

- 2、修改PGDATA 目录下的postgresql.conf 文件

```
listen_addresses = '*'          # what IP address(es) to listen on;
```

- 3、重启数据库

```
pg_ctl restart
```

### tips
- 数据库只能在非root 用户下进行安装