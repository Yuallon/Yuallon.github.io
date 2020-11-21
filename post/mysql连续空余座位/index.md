
### 题目描述

几个朋友来到电影院的售票处，准备预约连续空余座位。

你能利用表 cinema ，帮他们写一个查询语句，获取所有空余座位，并将它们按照 seat_id 排序后返回吗？

```
| seat_id | free |
|---------|------|
| 1       | 1    |
| 2       | 0    |
| 3       | 1    |
| 4       | 1    |
| 5       | 1    |
```

对于如上样例，你的查询语句应该返回如下结果。

```
| seat_id |
|---------|
| 3       |
| 4       |
| 5       |
```

注意：

- seat_id 字段是一个自增的整数，free 字段是布尔类型（'1' 表示空余， '0' 表示已被占据）。
- 连续空余座位的定义是大于等于 2 个连续空余的座位。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/consecutive-available-seats

### 解题思路

- 题中只有一个表，连续空位条件需要表格的上下数据做比较。所以要用到 **self join（自连接）**来解决。两个表格的连接结果是两个表格的 **[笛卡尔乘积](https://baike.baidu.com/item/%E7%AC%9B%E5%8D%A1%E5%B0%94%E4%B9%98%E7%A7%AF/6323173?fr=aladdin)**

  ```
  SELECT a.seat_id as a_id, a.free as a_free, b.seat_id as b_id, b.free as b_free
  FROM cinema a JOIN cinema b;
  
  +------+--------+------+--------+
  | a_id | a_free | b_id | b_free |
  +------+--------+------+--------+
  | 1    | 1      | 1    | 1      |
  | 2    | 0      | 1    | 1      |
  | 3    | 1      | 1    | 1      |
  | 4    | 1      | 1    | 1      |
  | 5    | 1      | 1    | 1      |
  | 1    | 1      | 2    | 0      |
  | 2    | 0      | 2    | 0      |
  | 3    | 1      | 2    | 0      |
  | 4    | 1      | 2    | 0      |
  | 5    | 1      | 2    | 0      |
  | 1    | 1      | 3    | 1      |
  | 2    | 0      | 3    | 1      |
  | 3    | 1      | 3    | 1      |
  | 4    | 1      | 3    | 1      |
  | 5    | 1      | 3    | 1      |
  | 1    | 1      | 4    | 1      |
  | 2    | 0      | 4    | 1      |
  | 3    | 1      | 4    | 1      |
  | 4    | 1      | 4    | 1      |
  | 5    | 1      | 4    | 1      |
  | 1    | 1      | 5    | 1      |
  | 2    | 0      | 5    | 1      |
  | 3    | 1      | 5    | 1      |
  | 4    | 1      | 5    | 1      |
  | 5    | 1      | 5    | 1      |
  +------+--------+------+--------+
  25 rows in set (0.00 sec)
  ```

  

-  为了找到连续空座位，以b表来看，`b.seat_id` 与`a.seat_id` 里面的值应该相差为1，且两者都应该为空。

  ```
  SELECT a.seat_id as a_id, a.free as a_free, b.seat_id as b_id, b.free as b_free
  FROM cinema a join cinema b
    on abs(a.seat_id - b.seat_id) = 1
    and a.free = true and b.free = true;
    
  +------+--------+------+--------+
  | a_id | a_free | b_id | b_free |
  +------+--------+------+--------+
  | 4    | 1      | 3    | 1      |
  | 3    | 1      | 4    | 1      |
  | 5    | 1      | 4    | 1      |
  | 4    | 1      | 5    | 1      |
  +------+--------+------+--------+
  4 rows in set (0.00 sec)
  ```

  

- 最后，选择上表中的字段 seat_id ，并排序后返回。

  ```
  SELECT DISTINCT b.seat_id FROM 
  cinema as a 
  JOIN cinema as b 
  ON abs(a.seat_id - b.seat_id) = 1
  AND a.free = 1 AND  b.free = 1
  ORDER BY seat_id ASC
  
  +---------+
  | seat_id |
  +---------+
  | 3       |
  | 4       |
  | 5       |
  +---------+
  3 rows in set (0.01 sec)
  ```





