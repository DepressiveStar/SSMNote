# 映射器

* MyBatis的映射器主要是通过XML方式实现
* 自动映射和驼峰映射，能有效减少大量的映射配置，减少工作量
* 配置自动映射的autoMappingBehavior 选项的取值范围是：（通常使用默认即可）
  * NONE 不进行自动映射
  * PARTIAL 默认值，只对没有嵌套结果集进行自动映射
  * FULL 对所有结果集进行自动映射，包括嵌套结果集

* 驼峰命名（mapUnderscoreToCamelCase）设置为true即可
* 自动映射和驼峰映射建立在SQL列名和POJO属性名的映射关系上