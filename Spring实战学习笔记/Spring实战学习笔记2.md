## Spring实战学习笔记2

**依赖注入（DI）的本质是创建应用对象之间协作关系即装配（Wiring）**

### Spring配置的可选方案

Spring提供3种主要的装配机制

* 在XML中进行显式配置
* 在Java中进行显式配置
* 隐式的bean发现机制和自动装配

> 作者建议是尽可能使用自动装配机制，必须使用显式配置bean时，推荐使用类型安全且比XML更为强大的JavaConfig，最后才使用XML。

### 自动装配bean

Spring从两个角度来实现自动化装配

* 组件扫描(component scanning)：Spring会自动发现应用上下文中所创建的bean
* 自动装配(autowiring)：Spring自动满足bean之间的依赖

> 使用@Component注解，表明该类作为组件类，告知Spring为其创建bean
>
> 使用@ComponentScan注解，启用组件扫描，默认扫描与配置类相同的包
>
> 在XML中通过
>
> ```
> <context:component-scan base-package="soundsystem"/>
> ```
>
> 启用组件扫描

>测试组件扫描功能时
>
>```
>@RunWith(SpringJUnit4ClassRunner.class)
>```
>
>使用上述注解调用Spring的类自动创建Spring的应用上下文
>
>```
>@ContextConfiguration(classes=CDPlayerConfig.class)
>```
>
>使用上述注解在指定类中加载配置

将bean设置为不同ID时，修改注解为如下形式

```
@Component("lonelyHeartsClub")
```

指定扫描组件的基础包时

```
@ComponentScan(basePackages="soundsystem")
```

设置扫描多个基础包

```
@ComponentScan(basePackages={"soundsystem","video"})
```

指定扫描包中包含的类或接口

```
@ComponentScan(basePackageClasses={CDPlayer.class,DVDPlayer.class})
```

通过@Autowired注解，声明进行自动装配为当前bean注入依赖的bean(该注解为Spring特有注解)。**@Inject**注解与其作用相同，来源于Java依赖注入规范

```java
@Autowired
public CDPlayer(CompactDisc cd){
  this.cd = cd;
}
```

Spring创建CDPlayer bean的时候，通过该构造器进行实例化并传入一个CompactDisc类型的bean

### 通过Java代码装配bean

通过@Configuration注解表明该类是一个配置类

通过@Bean注解声明bean

```java
@Bean
public CompactDisc sgtPeppers(){
    return new SgtPeppers();
}
```

对于依赖于其他bean的bean装配

```java
@Bean
public CDPlayer cdPlayer(CompactDisc compactDisc){
    return newCDPlayer(compactDisc)
}
```

通过上述方式引用其他的bean

### 通过XML装配bean

创建一个XML文件，以<beans>元素为根

可借助Spring Tool Suite创建XML配置文件

声明bean

```java
<bean id="compactDisc" class="soundsystem.SgtPeppers"/>
```

构造器注入bean引用

```java
<bean id="cdPlayer" class="soundsystem.CDPlayer">
  <constructor-arg ref="compactDisc"/>
</bean>
```

将给定值以字面量形式注入到构造器中

```
<bean id="compactDisc" class="soundsystem.BlankDisc">
  <constructor-arg value="The Beatles"/>
</bean>
```

实现bean引用列表的装配

```
<bean id="compactDisc" class="soundsystem.BlankDisc">
  <constructor-arg value="The Beatles"/>
  <constructor-arg>
   <list>
    <value>aaa</value>
    <value>bbb</value>
    <value>ccc</value>
   </list>
  <constructor-arg>   
</bean>
```

实现属性注入

```
<bean id="cdPlayer" class="soundsystem.CDPlayer">
  <property name="compactDisc" ref="compactDisc"/>
</bean>
```

<property>元素为属性的Setter方法所提供功能与<constructor-arg>元素为构造器所提供的功能是相同的

将字面量注入到属性中

```
<bean id="compactDisc" class="soundsystem.BlankDisc">
  <property name="title" value="abc"/>
  <property name="tracks">
   <list>
    <value>aaa</value>
    <value>bbb</value>
    <value>ccc</value>
   </list>
  </property>   
</bean>
```

### 导入和混合配置

通过@Import注解将需要的两个类组合在一起

>@Import(CDConfig.class)

>@Import({CDPlayerConfig.class,CDConfig.class})

通过@ImportResource注解，加载XML文件

> @ImportResource("classpath:cd-config.xml")