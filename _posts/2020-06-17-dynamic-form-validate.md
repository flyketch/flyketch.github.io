### element el-form 多表单验证及动态数据项表单验证

参考官网
这里需要注意的是，:prop的写法。一定是遍历的数组’domains.’ 加上（domain，index）中 的index，再加上‘.value’。

原因是，表单验证时它需要去找到具体的某一个表单项，一旦prop写错，是无法达到验证效果的。

[vue el-form表单验证，多表单验证及动态数据项表单验证](https://blog.csdn.net/qq_27263045/article/details/82797176)

[Vue+Element动态生成新表单并添加验证](https://blog.csdn.net/weixin_41041379/article/details/81908788)
