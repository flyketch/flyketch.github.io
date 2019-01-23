## GreenPlum 如何导入S3的数据

### S3是什么
Amazon简单存储服务（Amazon S3）提供了安全、持久、高可扩展的对象存储，参考链接[Amazon S3](https://aws.amazon.com/cn/s3/)

### 如何使用

#### 1、创建S3 server
通过docker 创建server，并暴露端口8888
``` bash
docker run -d -p 8888:80 --restart always  andrewgaul/s3proxy

docker exec -it 4dbdbbfeaeb8 /bin/sh

cd /data
```
server 的bucket 存放在/data 目录下，每一个bucket 就是一个文件夹，prefix 指文件名前缀


### 2、使用S3 服务
以下操作都在master 上面进行
- 生成s3 配置文件
``` bash
gpcheckcloud -t > /home/gpadmin/s3.conf
```

修改配置文件

``` bash
secret = "local-credential"
accessid = "local-identity"

version = 2
encryption = false
```

- 检查配置文件

``` bash
gpcheckcloud -c "s3://192.168.1.15:8888/testbucket config=s3.conf"
```

正确则会返回

```
Your configuration works well.
```

- 上传文件到S3 server
``` bash
gpcheckcloud -u gpdextdata/two.txt "s3://192.168.1.15:8888/two/one config=s3.conf"
```

- Master 节点复制s3.conf 到segment
``` bash
gpscp  -f hostfile  /home/gpadmin/s3.conf =:/home/gpadmin/
```

- 创建S3外部表

加载S3外部表的依赖库:
``` bash
CREATE OR REPLACE FUNCTION write_to_s3() RETURNS integer AS
   '$libdir/gps3ext.so', 's3_export' LANGUAGE C STABLE;
CREATE OR REPLACE FUNCTION read_from_s3() RETURNS integer AS
   '$libdir/gps3ext.so', 's3_import' LANGUAGE C STABLE;
CREATE PROTOCOL s3 (writefunc = write_to_s3, readfunc = read_from_s3);
```

分别创建只写和只读的S3外部表
``` bash
CREATE EXTERNAL TABLE r_two (like two) location
('s3://192.168.1.15:8888/two/one config=/home/gpadmin/s3.conf') format
'text' (delimiter as '|');


CREATE WRITABLE EXTERNAL TABLE w_two (like two) location
('s3://192.168.1.15:8888/two/one config=/home/gpadmin/s3.conf') format
'text' (delimiter as '|');
```

### two.txt
like this 
``` bash
9397688616950152282|1529454007|order|浏览商品|{"name":"watch","city":"长沙"}|2018-06-20
9397688616950152281|1529454007|collectionGoods|登陆|{"name":"watch","city":"上海"}|2018-06-20
9397688616950152284|1529454007|searchGoods|搜索商品|{"name":"watch","city":"深圳","brand":"Hair","price":6034.851}|2018-06-20
9397688616950152283|1529454007|browseGoods|订单付款|{"name":"watch","city":"深圳","brand":"Apple","price":8510.112}|2018-06-20
```
