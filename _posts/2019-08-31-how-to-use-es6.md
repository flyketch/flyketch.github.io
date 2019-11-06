### ES6

- [ES6这些就够了](https://www.jianshu.com/p/287e0bb867ae)

- js 替换'/' 为 '-'

```
var a = '2019/11/6'
var ss = a.replace(/\//g, '-') // 转换ok

var cc = a.replace('/', '-') // 不能转换所有的
```