## 如何搭建Yii 2高级项目模板

### 1、下载yii2 包管理工具composer
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```
如果已经安装composer则通过
```
composer self-update
```
来进行更新composer

### 2、通过composer创建项目
```
composer create-project --prefer-dist yiisoft/yii2-app-advanced yii-application
```
创建项目完成后在项目目录下执行
```
php init
```
来初始化项目允许环境