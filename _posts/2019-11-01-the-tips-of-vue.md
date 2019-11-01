## Vue 使用技巧

1、el-switch 开关
默认写法
```
<el-switch v-model="state"
   	 active-value="1"
     inactive-value="2">
</el-switch>
```

active-value和inactive-value的值分别是字符串的1和2,如果你赋值为数字类型的 1 或 2是无法正常工作的，若赋值为数值类型，需这样写：

```
<el-switch v-model="state"
     :active-value="1"
     :inactive-value="2"
     @change=chang($event,state)>
</el-switch>
```

2、vue 传值

- 传值

```
this.$router.push({
    path: '/path',
    query: Object
})
```

- 取值

```
this.$route.query.title
```