## Spring实战学习笔记3

### 环境与profile

#### 配置profile bean

Spring引入bean profile功能，使用profile，首先要将所有不同bean

定义整理到一个或多个profile之中，将应用部署到每个环境时，确保对应的profile处于激活状态

使用profile注解注定某个bean属于哪一个profile，可在类级别或方法级别上使用该注解

在XML中通过<beans>元素的profile属性配置profile bean

亦可在<beans>元素中嵌套定义<benas>元素，将所有profile bean定义到同一个XML中

#### 激活profile

Spring依赖两个独立属性确定profile的激活状态

* spring.profiles.active
* spring.profiles.default

Spring提供@ActiveProfiles注解，指定运行测试时要激活的profile

### 条件化的bean

在Spring4.0之后可实现条件化的配置

使用@Conditional注解，给定条件结果为true时，才会创建这个bean

### 处理自动装配的歧义性

* @Primary与@Component组合用在组件扫描的bean上，将其声明为首选的bean
* @Qualifier注解是使用限定符主要方式，与@Autowired和@Inject协同使用，从而在注入时指定注入哪个bean。