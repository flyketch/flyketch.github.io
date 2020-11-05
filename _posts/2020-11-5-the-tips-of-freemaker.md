## FreeMarker 模板文件语法

> FTL 指令 ${user} ${being.name}

#### list 指令

```
<#list nameList as name>
 ${name}
</#list>
```

#### if 指令

```
<#if name == 'freemarker'>
    freemarker 模板引擎
</if>
```

### Note

> 注释 即<#-- .. --> 格式不会输出
