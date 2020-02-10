## Spring实战学习笔记4

散布于应用中多处的功能称为**横切关注点**，这些横切关注点是从概念上与应用的业务逻辑相分离。

**将横切关注点与业务逻辑相分离**是面向切面编程(AOP)所要解决的问题

AOP可以实现横切关注点与其所影响的对象之间的解耦

### 面向切面编程

横切关注点可被模块化为特殊的类，称之为**切面(aspect)**

其优点有两处：

* 每个关注点都集中于一个地方，而不是分散到多处代码中
* 服务模块更简洁

####  AOP术语

* 通知（Advice） 切面的工作：定义切面是什么及何时使用
  * 前置通知（Before）：目标方法被调用之前调用通知
  * 后置通知（After）：目标方法完成之后调用通知
  * 返回通知（After-returning）：目标方法成功执行后调用通知
  * 异常通知（After-throwing）：目标方法抛出异常后调用通知
  * 环绕通知（Around）：通知包裹被通知方法，在被通知方法调用前和调用后执行自定义行为

* 连接点（Join Point）在应用执行过程中能够插入切面的点。它可以是调用方法时，抛出异常时等等。切面代码利用这些点插入到应用正常流程中，并添加新的行为。
* 切点（Poincut）缩小切面所通知的连接点的范围，每个切点定义会匹配通知所要织入的一个或多个连接点
* 切面（Aspect）是通知和切点的结合，通知和切点共同定义切面的全部内容，是什么，在何时和何处完成其功能
* 引入（Introduction）允许向现有类添加新方法或属性
* 织入（Weaving）把切面应用到目标对象并创建新的代理对象过程。在目标对象的生命周期中有多个点可以进行织入
  * 编译期
  * 类加载期
  * 运行期

Spring提供4种类型的AOP支持：

* 基于代理的经典SpringAOP
* 纯POJO切面
* @AspectJ注解驱动的切面
* 注入式AspectJ切面（适用于Spring各版本）

**Spring通知是Java编写的**

**Spring只支持方法级别的连接点**

### 通过切点来选择连接点

execution指示器是编写切点定义时最主要使用的指示器

切点表达式设置当perform()方法执行时触发通知的调用

![](C:\Users\DepressiveStar\Desktop\切点定义.png)

亦可在切点表达式中限制切点匹配特定的bean

```
execution(* concert.Perform.perform())and bean('woodstock')
```

### 使用注解创建切面

使用@Aspect注解标注，表明其不仅是POJO，还是切面

使用@PointCut注解，定义可重用的切点

使用@EnableAspectJ-AutoProxy注解启用自动代理功能

在XML中使用< aop:aspectj-autoproxy/ >元素启用自动代理

环绕通知能够将被通知的目标方法完全包装起来，在一个通知方法中同时编写前置通知和后置通知。

其接受ProceedingJoinPoint作为参数，需要调用proceed()方法

使用@DeclareParents注解将新功能或接口引入到已有bean中

@DeclareParents注解由三部分组成：

* value属性指定哪种类型bean引入该接口
* defaultImpl属性指定为引入功能提供实现的类
* @DeclareParents注解标注的静态属性指明要引入的接口

### 在XML中声明切面

大多数AOP配置元素必须在< aop:config >元素的上下文内使用

> < aop:before>元素定义前置通知
>
> < aop:after-returning>元素定义返回通知
>
> < aop:after-throwing>元素定义异常通知

使用< aop:around>元素声明环绕通知

使用< aop:declare-parents>元素引入新方法

Spring通过aspectOf()方法获得切面的引用，使用Spring的依赖注入为AspectJ切面注入协作者