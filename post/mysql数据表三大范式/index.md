
### 前言

当我们利用Mysql来管理数据库的时候，是绕不开对数据表的操作的。在对数据表的创建过程中，如何使得后续的操作更有效率？这便是Mysql数据表建表范式内容。这部分内容，其实不算是Mysql独有内容，它是数据管理过程中，对于如何建表方便后续高效率操作数据的讨论。

### 第一范式

根据自己对数据的需求，尽可能的细化数据字段，即确保每列数据的原子性（不可再细分）。

例子1：

| 名字 | 性别 | 住址             |
| ---- | ---- | ---------------- |
| 张三 | 男   | 中国河南省开封市 |

例子2:

| 名字 | 性别 | 国籍 | 省份   | 城市   |
| ---- | ---- | ---- | ------ | ------ |
| 张三 | 男   | 中国 | 河南省 | 开封市 |

通过对比上面两个例子，在人员信息统计过程中，明显例子2是更好的。因为例子2的数据统计更详细（细分），方便后面对不同国家、省份、城市等人员信息的统计。

### 第二范式

在第一范式的基础上，确保数据表中每一列都和主键相关，而不能和主键某一部分相关。

例子：设计一个订单表。

```
mysql> create table myorder(
	product_id int,
	customer_id int,
	product_name varchar(20),
	customer_name varchar(20),
	primary key (product_id, customer_id)
);
```

在上面的订单表里面包含：产品ID、顾客ID、产品名字、顾客名字；其中主键为：产品ID、顾客ID。

我们发现，产品的名字只和产品ID有关；顾客的名字也只和顾客ID有关。这不满足第二范式。这个时候就需要把表格拆分：

```
###订单表
mysql> create table myorder(
	order_id int,
	product_id int,
	customer_id int,
	primary key (order_id)
);

###产品表
mysql> create table product(
	id int primary key,
	name varchar(20),
	product_id int,
	foreign key(product_id) references myorder(product_id)
);

###
mysql> create table customer(
	id int primary key,
	name varchar(20),
	customer_id int,
	foreign key(customer_id) references myorder(customer_id)
);

```

通过上面对表格的拆分：订单表、产品表、顾客表。我们发现，对于任何一个表格里面的数据而言，其每一列数据都只与该表的主键有关。再通过外键约束可以使得订单表包含产品表和顾客表。满足了第二范式。

第二范式的意义在于：对于任意一个数据表，其主键约束统领该表格所有列。方便后续根据约束的信息来处理数据。即，**主表统领所有副表**。

### 第三范式

在满足第二范式的前提下，除开主键列以外，其他列不能有传递依赖。

```
###订单表
mysql> create table myorder(
	order_id int,
	product_id int,
	customer_id int,
	customer_phone varchar(20),
	primary key (order_id)
);
```

在上面的表格中，虽然订单ID统领：产品ID、顾客ID、顾客电话。但是顾客ID和顾客电话之间有传递关系，则不满足第三范式。要想满足第三范式，可以把顾客电话放在顾客表里面。

### 参考

- [数据表设计--第一范式](https://www.bilibili.com/video/BV1Vt411z7wy?p=16)
- [数据表设计--第二范式](https://www.bilibili.com/video/BV1Vt411z7wy?p=17)
- [数据表设计--第三范式](https://www.bilibili.com/video/BV1Vt411z7wy?p=18)

