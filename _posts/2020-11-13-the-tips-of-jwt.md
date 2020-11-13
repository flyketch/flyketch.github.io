## JWT token的认证多台服务器部署问题

> 如果多台服务器时间不同步回存在`com.auth0.jwt.exceptions.InvalidClaimException: The Token can't be used before Thu Nov 12 16:52:52 CST 2020.` 的问题

> 解决办法：ntp 来同步时间

```
$ ntpdate -u ntp1.aliyun.com
```
