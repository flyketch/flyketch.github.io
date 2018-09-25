# 新建一个eureka client端报错

## 1、版本信息

a、Spring Boot: 2.0.5.RELEASE

b、Spring Cloud: Finchley.SR1

## 2、报错信息
Invocation of destroy method failed on bean with name 'scopedTarget.eurekaClient': org.springframework.beans.factory.BeanCreationNotAllowedException: Error creating bean with name 'eurekaInstanceConfigBean': Singleton bean creation not allowed while singletons of this factory are in destruction (Do not request a bean from a BeanFactory in a destroy method implementation!)

## 3、解决方法
这是因为client里不包含Tomcat启动的web依赖，所以项目无法实例化，在pom 文件中加入web依赖即可。
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

