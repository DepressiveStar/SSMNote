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