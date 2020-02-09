## Spring实战学习笔记3

### 环境与profile

Spring引入bean profile功能，使用profile，首先要将所有不同bean

定义整理到一个或多个profile之中，将应用部署到每个环境时，确保对应的profile处于激活状态

使用profile注解注定某个bean属于哪一个profile，可在类级别或方法级别上使用该注解

在XML中通过<beans>元素的profile属性配置profile bean

亦可在<beans>元素中嵌套定义<benas>元素，将所有profile bean定义到同一个XML中