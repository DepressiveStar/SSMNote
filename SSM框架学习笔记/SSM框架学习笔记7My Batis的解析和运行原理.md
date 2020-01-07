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