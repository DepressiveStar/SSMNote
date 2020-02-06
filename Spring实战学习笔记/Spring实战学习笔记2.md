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

通过@Autowired注解，声明进行自动装配为当前bean注入依赖的bean