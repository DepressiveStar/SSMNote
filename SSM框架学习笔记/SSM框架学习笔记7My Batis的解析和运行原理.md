# My Batis 的解析和运行原理

MyBatis的运行过程分为两大步：

* 读取配置文件缓存到Configuration对象，用以创建SqlSessionFactory
* SqlSession的执行过程
  * 包含反射技术和动态代理技术（此为揭示MyBatis底层构架的基础）

### 构建SqlSessionFactory过程

MyBatis通过SqlSessionFactoryBuilder构建SqlSessionFactory分为两步

* 通过org.apache.ibatis.builder.xml.XMLConfiguration解析配置的XML文件，读出所配置的参数，将读取内容存入org.apache.ibatis.session.Configuration类对象中，Configuration采用的是单例模式
* 使用Configuration对象去创建SqlSessionFactory,此为一个接口而不是实现类，所以MyBatis提供一个默认的实现类org.apache.ibatis.session.defaults.DefaultSqlSessionFactory

#### 构建Configuration

Configuration的作用是：

* 读入配置文件，包括基础配置的XML和映射器XML
* 初始化一些基础配置
* 提供单例，为后续创建SessionFactory服务，提供配置的参数
* 执行一些重要对象的初始化方法

#### 构建映射器的内部组成

映射器的内部组成：

* MappedStatement 保存映射器节点的内容、是一个类
* SqlSource是提供BoundSql对象的地方，是MappedStatement的一个属性，是接口而不是实现类，作用是根据上下文和参数解析生成需要的SQL
* BoundSql是一个结果对象，是建立SQL和参数的地方，包含3个常用属性：sql、parameterObject、parameterMappings

**需要关注的是BoundSql对象，通过它便可拿到要执行的SQL和参数，通过SQL和参数即可增强MyBatis的功能**

BuondSql提供3个主要属性

* parameterObject 参数本身，传递简单对象、POJO或者Map、@Param注解的参数
  * 传递简单对象
  * 传递POJO或者Map
  * 传递多个参数
  * 使用@Param注解，MyBatis就会把parameterObject变成Map<String,Object>对象

* parameterMappings是一个List,每一个元素都是ParameterMapping对象，对象会描述参数，一般不去改变它，通过它即可实现参数和SQL的结合
* sql属性是书写在映射器里的一条被SqlSource解析后的SQL，大部分时候无须修改，只有在使用插件时可根据需要进行改写

### SqlSession运行过程