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

- 3、vue excel 文件导入导出

参考vue-element-admin 中的导入导出进行使用

- 4、vue 打包后可以看到源代码

在 config/index.js 页面找到productionSourceMap:ture 改为 productionSourceMap:false
