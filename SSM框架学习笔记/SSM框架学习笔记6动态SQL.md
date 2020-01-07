# 动态SQL



### 动态SQL元素

* if 判断语句
* choose(when otherwise) 相当于java中的switch和case语句
* trim(where set) 辅助元素，用于处理特定的SQL拼装问题
* foreach 循环语句

### if元素

常与test属性联合使用

> <selec t id=” findRoles ” parameterType=” string ” resultMap= ” roleResultMap”>
> select role no , role——name , note from t_role where 1=1
> <if test=” roleName ! = null and roleName != ' ' ”>
> and role name like concat （ ’ %’， ＃｛roleName｝,’ %’ ）
> </ if>
>
> </select>

如上案例，roleName传递进映射器，参数不为空，采取构造对roleName的模糊查询，否则不去构造条件