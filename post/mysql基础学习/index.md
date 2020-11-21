
###终端命令操作数据库

####如何在终端打开Mysql？

```
mysql -uroot -p123456
```

其中，"root"是打开哪一个数据库，"123456"是密码

#### 如何查询数据库服务器中所有的数据库？

启动Mysql程序后，输入：

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.03 sec)
```

注意：一定要以英文分号（;）结尾。

#### 如何在数据库服务器中，创建数据库？

```
mysql> create database test;
Query OK, 1 row affected (0.01 sec)
```

- 如何选中某一个数据库进行操作？

  ```
  mysql> use test
  Database changed
  ```

- 如何查看某个数据库中所有的数据表？(先选中)

  ```
  mysql> show tables;
  Empty set (0.00 sec)
  ```

- 如何创建一个数据表？

  ```
  mysql> CREATE TABLE table_name (column_name column_type);
  ```

  注：创建一个新的数据表，要给定一个名字，而且数据表中的列名，要指定相应的数据类型。如，一个student数据表中，age的数据类型为：整数型。

  有关Mysql的数据介绍可以查看：[MySQL 数据类型](https://www.runoob.com/mysql/mysql-data-types.html)

  ```
  mysql> CREATE TABLE student (
      -> name VARCHAR(20),
      -> sex CHAR(1),
      -> birth DATE);
  Query OK, 0 rows affected (0.10 sec)
  ```

- 如何查看一个数据表结构？

  ```
  mysql> describe student;
  +-------+-------------+------+-----+---------+-------+
  | Field | Type        | Null | Key | Default | Extra |
  +-------+-------------+------+-----+---------+-------+
  | name  | varchar(20) | YES  |     | NULL    |       |
  | sex   | char(1)     | YES  |     | NULL    |       |
  | birth | date        | YES  |     | NULL    |       |
  +-------+-------------+------+-----+---------+-------+
  3 rows in set (0.03 sec)
  ```

- 如何查看一个数据表中的数据记录呢？

  ```
  mysql> select * from student;
  Empty set (0.00 sec)
  ```

  注：因为刚刚创建，所以为Empty。

- 如何往数据表中添加数据记录？

  MySQL 表中使用 **INSERT INTO** SQL语句来插入数据。

  ```
  INSERT INTO table_name ( field1, field2,...fieldN )
                         VALUES
                         ( value1, value2,...valueN );
  ```

  例子：

  ```
  mysql> INSERT INTO student
      -> VALUES ("Allon","F","1995-03-13");
  Query OK, 1 row affected (0.01 sec)
  ```

  再次读取：

  ```
  mysql> select * from student;
  +-------+------+------------+
  | name  | sex  | birth      |
  +-------+------+------------+
  | Allon | f    | 1995-03-13 |
  +-------+------+------------+
  1 row in set (0.01 sec)
  ```

  注意：插入的数据一定要满足前面设置的数据类型极其长度。

- 如何删除数据表中的数据？

  语法：

  ```
  delete from table_name where name='field_name';
  ```

  例子：

  ```
  mysql> select * from student;
  +-------+------+------------+
  | name  | sex  | birth      |
  +-------+------+------------+
  | Allon | f    | 1995-03-13 |
  | yuhan | m    | 1995-08-13 |
  | mohan | m    | 1995-05-31 |
  +-------+------+------------+
  3 rows in set (0.00 sec)
  
  #删除操作
  mysql> delete from student where name='mohan';
  Query OK, 1 row affected (0.02 sec)
  
  ##
  mysql> select * from student
      -> ;
  +-------+------+------------+
  | name  | sex  | birth      |
  +-------+------+------------+
  | Allon | f    | 1995-03-13 |
  | yuhan | m    | 1995-08-13 |
  +-------+------+------------+
  2 rows in set (0.00 sec)
  ```

- 如何修改数据？

  语法：

  ```
  update table_name set name='field_name' where name='field_name';
  ```

  例子：

  ```
  ###原始数据
  mysql> select * from student
      -> ;
  +-------+------+------------+
  | name  | sex  | birth      |
  +-------+------+------------+
  | Allon | f    | 1995-03-13 |
  | yuhan | m    | 1995-08-13 |
  +-------+------+------------+
  2 rows in set (0.00 sec)
  
  #修改数据
  mysql> update student set name='Yuallon' where name='Allon';
  
  ##修改结果
  mysql> select * from student;
  +---------+------+------------+
  | name    | sex  | birth      |
  +---------+------+------------+
  | Yuallon | f    | 1995-03-13 |
  | yuhan   | m    | 1995-08-13 |
  +---------+------+------------+
  2 rows in set (0.00 sec)
  ```

- 总结

  - 增：INSERT
  - 删：DELETE
  - 改：UPDATE
  - 查：SELECT

### Mysql建表约束类型及其含义

通过前面的学习，我们已经可以对Mysql数据进行 **增删改查** 的操作。但是，在数据的记录中，如何保证某一条记录的唯一性呢，即：如何区分A班的张三与D班的张三 or A班的李四与A班的张三呢？

#### 主键约束

通过添加主键约束（primary key），它能够唯一确定一张表中的一条记录，可以使得该字段**不重复且不为空（NULL）**。

例子：

```
###创建一个primary key约束的数据表
mysql> create table user ( id int primary key, name varchar(20));
Query OK, 0 rows affected (0.05 sec)

###查看，在数据表ID的KEY下有PRI
mysql> describe user;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

###添加数据
mysql> insert into user values (1,'Zhang3');
Query OK, 1 row affected (0.01 sec)

####重复添加则报错
mysql> insert into user values (1,'Zhang3');
ERROR 1062 (23000): Duplicate entry '1' for key 'PRIMARY'

####不给定id值也报错
mysql> insert into user values (NULL,'Li4');
ERROR 1048 (23000): Column 'id' cannot be null
```

**联合主键约束**：只要是多个主键约束的参数，不完全一样，就不冲突。

例子：

```
##创建联合主键约束
mysql> create table user2 ( id int, name varchar(20), sex varchar(20), primary key (id,name));
Query OK, 0 rows affected (0.05 sec)

##添加
mysql> insert into user2 values(1,'Zhang3','femal');
Query OK, 1 row affected (0.01 sec)

mysql> insert into user2 values(2,'Zhang3','femal');
Query OK, 1 row affected (0.01 sec)

mysql> insert into user2 values(1,'Li3','femal');                            
Query OK, 1 row affected (0.00 sec)

##查询
mysql> select * from user2;
+----+--------+-------+
| id | name   | sex   |
+----+--------+-------+
|  1 | Li3    | femal |
|  1 | Zhang3 | femal |
|  2 | Zhang3 | femal |
+----+--------+-------+
3 rows in set (0.00 sec)
```

注：联合主键任何一个参数都不能为空（NULL）。

**自增约束**：auto_increment，自动增加某个参数的数值。

```
###创建自增约束数据表
mysql> create table user3(
    -> id int primary key auto_increment,
    -> name varchar(20)
    -> );
Query OK, 0 rows affected (0.03 sec)

###添加数据,没有对ID进行操作
mysql> insert into user3 (name) values ('Zhang3');
Query OK, 1 row affected (0.01 sec)

##查看数据，ID会自动添加数值
mysql> select * from user3
    -> ;
+----+--------+
| id | name   |
+----+--------+
|  1 | Zhang3 |
+----+--------+
1 row in set (0.00 sec)
```

**如果创建数据表的时候，忘记添加主键约束了，怎么办？**

```
alter table table_name add primary key(field_name)
```

**如何删除主键约束呢？**

```
alter table table_name drop primary key
```

**如何修改？**

```
alter table table_name modify field_name field_type primary key
```



#### 唯一约束

约束修饰字段的值，不能重复。

例子：

```
###创建数据表
mysql> create table user5 (
    -> id int,
    -> name varchar(20)
    -> );
Query OK, 0 rows affected (0.05 sec)

###数据表
mysql> describe user5
    -> ;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.02 sec)

###创建唯一约束
mysql> alter table user5 add unique(name);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

####再次查看
mysql> desc user5
    -> ;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

注：唯一约束，即，name后面的（UNI）表示，name属性不可以重复。

```
##添加数据
mysql> insert into user5 values(1,"Zhang3");
Query OK, 1 row affected (0.00 sec)

##重复添加报错
mysql> insert into user5 values(1,"Zhang3");
ERROR 1062 (23000): Duplicate entry 'Zhang3' for key 'name'
```

也可以创建数据列表的时候添加约束，跟前面的主键约束一样。

**如何删除唯一约束？**

```
alter table table_name drop index field_name;

##Example
alter table user5 drop index name;
```

**modify方式添加唯一约束**

```
alter table user5 modify name varchar(20) unique;
```



#### 非空约束

修饰的字段不能为空（NULL）

例子：

```
###创建非空约束数据表
mysql> create table user6 (
    -> id int,
    -> name varchar(20) not null
    -> );
Query OK, 0 rows affected (0.05 sec)

###查看
mysql> desc user6;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

注：name属性的NULL一栏中，null=NO，表示name的数据不能为空。



#### 默认约束

当我们插入字段值的时候，如果没有传值，使用默认约束。

例子：

```
###创建默认约束数据表
mysql>  create table user7 (
    -> id int,
    -> name varchar(20),
    -> age int default 10);
Query OK, 0 rows affected (0.04 sec)

###查看表格特征
mysql> desc user7
    -> ;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | 10      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

###添加数据
mysql> insert into user7 (id,name) values (1,"zhang3");
Query OK, 1 row affected (0.00 sec)

###提取表格数据
mysql> select * from user7;
+------+--------+------+
| id   | name   | age  |
+------+--------+------+
|    1 | zhang3 |   10 |
+------+--------+------+
1 row in set (0.01 sec)
```

注：上面添加数据的时候没有给age传值，则默认为10。



#### 外键约束

涉及到两个表格：父表，子表。

例子：

```
##创建一个班级表
mysql> create table classes(
    -> id int primary key,
    -> name varchar(20)
    -> );
Query OK, 0 rows affected (0.04 sec)

##查看classes表格属性
mysql> desc classes;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

##创建一个学生表
mysql> create table students(
    -> id int primary key,
    -> name varchar(20),
    -> class_id int,
    -> foreign key(class_id) references classes(id)
    -> );
Query OK, 0 rows affected (0.04 sec)

##查看students表格属性,Key值有MUL
mysql> desc students;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int(11)     | NO   | PRI | NULL    |       |
| name     | varchar(20) | YES  |     | NULL    |       |
| class_id | int(11)     | YES  | MUL | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

```

注：这就像是文件夹跟文件的关系一样，在班级的文件夹中，有各个班级的文件，每个班级里面又有相应该班级的学生信息。数据的增删改查跟前面一样，只是连个表格有了class_id联系起来了。

- 主表 classes 中没有的数据值，在副表里面不能被引用。
- 主表里面的信息被副表引用，则不可以被直接删除。
- 

###如何退出数据库服务器？

```
mysql> exit;
Bye
```



### 参考

[一天学会 MySQL 数据库](https://www.bilibili.com/video/BV1Vt411z7wy?p=1)