
#### 题目

编写一个 SQL 查询，获取 `Employee` 表中第 *n* 高的薪水（Salary）。

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

例如上述 `Employee` 表，*n = 2* 时，应返回第二高的薪水 `200`。如果不存在第 *n* 高的薪水，那么查询应返回 `null`。

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

#### SQL 语句

#####使用 IFNULL

题目要求：如果没有第二高的成绩，返回空值，所以这里用判断空值的函数（IFNULL）函数来处理特殊情况。

IFNULL() 函数用于判断第一个表达式是否为 NULL，如果为 NULL 则返回第二个参数的值，如果不为 NULL 则返回第一个参数的值。

IFNULL() 函数语法格式为：

**IFNULL(expression, alt_value)**

如果第一个参数的表达式 expression 为 NULL，则返回第二个参数的备用值。两个参数可以是文字值或表达式。

##### 使用 LIMIT 和 OFFSET

在`SELECT`语句中使用`LIMIT`子句来约束结果集中的行数。`LIMIT`子句接受一个或两个参数。**两个参数的值必须为零或正整数**。

两个参数的`LIMIT`子句语法：

```
SELECT 
    column1,column2,...
FROM
    table
LIMIT offset , count;
```

我们来查看`LIMIT`子句参数：

- `offset`参数指定要返回的第一行的偏移量。第一行的偏移量为`0`，而不是`1`。
- `count`指定要返回的最大行数。

##### 本题SQL代码

```

select ifNull(
(select distinct salary
from Employee 
order by Salary Desc
limit 1,1),null
) as SecondHighestSalary;
```

#### 注：

使用MySQL LIMIT获得第n个最高值，第三个链接里面有详细的介绍。

### 参考资料

- [MySQL IFNULL() 函数](https://www.runoob.com/mysql/mysql-func-ifnull.html)

- [MySQL IFNULL函数简介](https://www.yiibai.com/mysql/ifnull.html)

- [MySQL LIMIT子句简介](https://www.yiibai.com/mysql/limit.html)

- #### [177. 第N高的薪水](https://leetcode-cn.com/problems/nth-highest-salary/)

- [图解SQL面试题：如何查找第N高的数据？](https://leetcode-cn.com/problems/nth-highest-salary/solution/tu-jie-sqlmian-shi-ti-ru-he-cha-zhao-di-ngao-de-2/)

