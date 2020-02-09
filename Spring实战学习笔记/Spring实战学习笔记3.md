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

* @Primary与@Component组合用在组件扫描的bean上，将其声明为首选的bean（设置多个首选bean时无法处理歧义）
* @Qualifier注解是使用限定符主要方式，与@Autowired和@Inject协同使用，从而在注入时指定注入哪个bean。（只针对基于默认beanID作为限定符）。
* 可在bean声明中添加@Qualifier注解创建自定义限定符。
* 使用自定义限定符注解，该注解本身使用@Qualifier注解来标注。

### bean的作用域

默认情况下，Spring应用上下文中所有bean是以单例形式创建的

**使用@Scope注解选择其他的作用域**

* 在Web应用中，使用会话和请求作用域需要用到@Scope及其proxyMode属性。
* 在XML中，通过<bean>元素的scope属性设置bean的作用域，通过Spring aop命名空间设置代理模式

> <aop:scoped-proxy/>

### 运行时值注入

为了避免值注入时的硬编码值情况，使这些值在运行时确定，Spring提供两种运行时求值的方式

* 属性占位符（Property placeholder）
* Spring表达式语言(SpEL)

处理外部值最简单方式是声明属性源并通过Spring的Environment来检索属性

**Environment**

Environment提供getProperty()方法来获取属性值

getActiveProfiles()获取激活profile名称

getDefaultProfiles()获取默认profile名称

**在Spring装配中，占位符形式为使用${...}包装的属性名称**

