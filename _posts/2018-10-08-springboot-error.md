### SpringBoot 项目启动时候报错

#### 1、报错信息如下

```
Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
```

#### 2、解决
这种情况，大多是没有连接上数据库导致的，重新查看数据库连接信息，修改即可。
