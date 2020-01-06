# 映射器

* MyBatis的映射器主要是通过XML方式实现
* 自动映射和驼峰映射，能有效减少大量的映射配置，减少工作量
* 配置自动映射的autoMappingBehavior 选项的取值范围是：（通常使用默认即可）
  * NONE 不进行自动映射
  * PARTIAL 默认值，只对没有嵌套结果集进行自动映射
  * FULL 对所有结果集进行自动映射，包括嵌套结果集

* 驼峰命名（mapUnderscoreToCamelCase）设置为true即可
* 自动映射和驼峰映射建立在SQL列名和POJO属性名的映射关系上
* 对于传递多个参数，使用注解传递，提高代码可读性

>public List<Role > findRolesByAnnotation (@Param (” roleName ” ) String rolename ,
>@Param (” note ” ) String note) ;

* 4种传递多个参数的方法
  * 使用m叩传递参数导致了业务可读性的丧失，导致后续扩展和维护的困难，在实际
    的应用中要果断废弃这种方式。
  * 使用＠ Param 注解传递多个参数，受到参数个数C n ）的影响。当n 三三5 时， 这是最
    佳的传参方式，它比用Java Bean 更好，因为它更加直观； 当n> 5 时， 多个参数将
    给调用带来困难，此时不推荐使用它。
  * 当参数个数多于5 个时，建议使用Java Bean 方式
  * 对于使用混合参数的，要明确参数的合理性

* 使用resultMap映射结果集
* MyBatis内置专门处理分页的类--RowBounds,其原理是执行SQL的查询后，按照偏移量和限制条数返回查询结果，对于大量的数据查询，性能并不佳

### sql元素

sql元素可定义SQL的一部分，方便后面的SQL引用