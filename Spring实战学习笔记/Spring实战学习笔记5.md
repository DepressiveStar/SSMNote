## Spring实战学习笔记5

SpringMVC基于模型-视图-控制器（Model-View-Controller）模式实现

### SpringMVC起步

SpringMVC所有请求会通过一个前端控制器Servlet

DispatcherServlet是SpringMVC的核心，负责将请求路由到其他组件之中

在XML使用< mvc:annotation-driveb>启用注解驱动的SpringMVC

使用@EnableWebMvc注解标注类，从而启用SpringMVC

最小可用的SpringMVC配置需要：

* 启用SpringMVC
* 启用组件扫描
* 配置JSP视图解析器
* 配置静态资源处理

### 编写基本的控制器

在SpringMVC中，控制器只是方法上添加@RequestMapping注解的类，声明它们所要处理的请求