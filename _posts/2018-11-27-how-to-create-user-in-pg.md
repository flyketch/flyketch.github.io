## 在postgres 中创建用户

- 登录postgres
```
psql -Upostgres
```
- 创建用户
```
create user ss with password '123456789'
```
- 创建数据库
```
create database test owner ss
```
- 分配权限
```
grant all privileges on database test to ss
```
- 重新登录系统
```
psql -U ss -d test
```
## 备注
`查看postgres 版本`
```
psql --version
```

参考文章：

1、[阮一峰的网络日志-PostgreSQL新手入门](http://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html)