### 如何部署Vue 项目

1、build 目录下 webpack.prod.conf.js 里面的 output 新增

```
output: {
    publicPath: './'
}
```

2、build 目录下webpack.base.conf.js里的 output 修改成

```
publicPath: process.env.NODE_ENV === 'production'
  ? './' +config.build.assetsPublicPath
  : './' + config.dev.assetsPublicPath
```

3、在build文件夹里面的utils.js文件 下面的 generateLoaders 方法里面新增

```
if (options.extract) {
    return ExtractTextPlugin.extract({
      use: loaders,
      publicPath: '../../',  // 加入这行代码就可以
      fallback: 'vue-style-loader'
   })
} else {
   return ['vue-style-loader'].concat(loaders)
}
```

4、执行build 命令

```
npm run build
```

项目路径下的dist 目录即为打包后的文件

5、设置引用前缀，修改config 下的 index.js文件

```
build: {
    assetsPublicPath: './',
    assetsPublicPath: '/product',
}
```
