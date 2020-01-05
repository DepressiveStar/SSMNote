# MyBatis配置

### 概述

* MyBatis配置项顺序不能颠倒

### properties属性

* 给系统配置运行参数，放在XML文件或properties文件中
* MyBatis提供3种方式使用properties
  * property子元素
  * properties文件（普遍，简单）
  * 程序代码传递

### settings设置

* MyBatis最复杂的配置，深刻影响MyBatis底层运行
* 大部分情况下使用默认值即可运行

### typeAliases别名

* 用别名来代替全限定名
* 分为系统定义别名和自定义别名
* 别名由类TypeAliasRegistry定义
* 使用TypeAliasRegistry 的registerAlias方法即可注册别名
* MyBatis支持扫描包中的类，并将首字母小写作为别名，若出现重名，通过MyBatis提供注解区分

### typeHandler类型转换器

* 分为两类，其作用是承担jdbcType和javaType之间的相互转换
  * jdbcType-定义数据库类型
  * javaType-定义Java类型

* 自定义typeHandler需要实现接口typeHandler，或者BaseTypeHandler

### ObjectFactory （对象工厂）

