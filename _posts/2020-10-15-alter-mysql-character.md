## Mysql 修改字符集和排序规则

> 改为utf8_unicode_ci
```
alter table partner_order CHANGE order_id order_id VARCHAR(100) CHARACTER SET utf8 COLLATE 'utf8_unicode_ci';
```

> 修改表的字符集
```
ALTER TABLE order DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

> 修改表的字符集和所有列的字符集
```
ALTER TABLE order CONVERT TO CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

> 修改库的排序规则

```
ALTER DATABASE db1 CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```
