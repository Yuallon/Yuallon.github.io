
IN运算符允许您确定指定的值是否与列表中的值或子查询中的任何值匹配。 下面说明了`IN`操作符的语法

```
SELECT 
    column1,column2,...
FROM
    table_name
WHERE 
 (expr|column_1) IN ('value1','value2',...);
```

下面我们更详细的来看看上面的查询：

- 可以在 WHERE 子句中与`IN`运算符一起使用，可使用列或表达式(`expr`)。
- 列表中的值必须用逗号(`，`)分隔。
- `IN`操作符也可以用在其他语句(如 INSERT，UPDATE，DELETE等)的 WHERE子 句中。

如果`column_1`的值或`expr`表达式的结果等于列表中的任何值，则`IN`运算符返回`1`，否则返回`0`。

当列表中的值都是常量时：

- 首先，MySQL根据`column_1`的类型或`expr`表达式的结果来计算值。
- 第二步，MySQL排序值。
- 第三步，MySQL使用二进制搜索算法搜索值。因此，使用具有常量列表的`IN`运算符的查询将执行得非常快。

> 请注意，如果列表中的`expr`或任何值为`NULL`，则`IN`运算符计算结果返回`NULL`。

可以将`IN`运算符与`NOT`运算符组合，以确定值是否与列表或子查询中的任何值不匹配。

### 参考资料

- [MySQL IN操作符介绍](https://www.yiibai.com/mysql/sql-in.html)



