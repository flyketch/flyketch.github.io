## Curl 使用的小技巧

```
linux 下使用curl访问带多参数，get未获取到参数的解决方案
1，由于url中&后面的其他参数获取不到，在linux系统中，&会使进程系统后台运行 必须对&进行转义才能获得所有参数
示列：http://localhost:8080findById?a=1&b=2&c=3
2.使用双引号方式最方便 这样在系统后台运行时就直接当成字符串 不会进行转义

```

参考 [linux使用curl命令 为什么要加双引号](https://blog.csdn.net/liulu164212/article/details/90644410)