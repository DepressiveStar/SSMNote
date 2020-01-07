# 动态SQL



### 动态SQL元素

* if 判断语句
* choose(when otherwise) 相当于java中的switch和case语句
* trim(where set) 辅助元素，用于处理特定的SQL拼装问题
* foreach 循环语句

### if元素

常与test属性联合使用

> ```java
> <selec t id=” findRoles ” parameterType=” string ” resultMap= ” roleResultMap”>
> select role no , role——name , note from t_role where 1=1
> <if test=” roleName ! = null and roleName != ' ' ”>
> and role name like concat （ ’ %’， ＃｛roleName｝,’ %’ ）
> </if>
> </select>
> ```

如上案例，roleName传递进映射器，参数不为空，采取构造对roleName的模糊查询，否则不去构造条件

### choose when otherwise元素

> ```java
> <select id= ” findRoles" parameterType=” r ole ” resultMap= ” roleResultMap”>
> select role_no , role_name, note from t_role
> where 1=1
> <choose>
> <when test=” roleNo != null and roleNo !=' ' ”>
> AND role_no = #{roleNo}
> </when>
> <when test = ” roleName != null and roleName !=' ' ”>
> AND role_name like concat （’%’ ,#{roleName}, ’ %’）
> </when>
> <otherwise>
> AND note is not null
> </otherwise>
> </choose>
> </select>
> ```

类似于switch case default功能的语句

### trim where set 元素

```java
<select id=” findRoles ” parameterType=” s tring ” resultMap=” roleResultMap” >
select role no , role name , note from t role
<trim prefix=” where" prefixOverrides="and">
<if test =” roleName ! = null and roleName !=””>
and role name like concat （ ’%’， #{roleName} ，’%’）
</if>
</trim>
</select>
```

更新字段,用where替换and