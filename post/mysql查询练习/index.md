
### 创建查询练习数据库及表格

```
#创建一个学校数据库
mysql> create database School;
Query OK, 1 row affected (0.00 sec)
```

####学生表

- 学号
- 姓名
- 性别
- 所在班级
- 出生日期

```
mysql> create table student( number varchar(20) primary key, name varchar(20) not null, sex varchar(20) not null, birthday datetime, class varchar(20) );
Query OK, 0 rows affected (0.08 sec)
```

#### 教师表

- 教师编号
- 教师姓名
- 教师性别
- 职称
- 出生日期
- 所在部门

```
mysql> create table teacher(
    -> number varchar(20) primary key,
    -> name varchar(20) not null,
    -> sex varchar(20) not null,
    -> birthday datetime,
    -> prof varchar(20) not null,
    -> depart varchar(20) not null
    -> );
Query OK, 0 rows affected (0.04 sec)
```

#### 课程表

- 课程号
- 课程名称
- 教师编号

```
mysql> create table course(
    -> number varchar(20),
    -> name varchar(20) not null,
    -> teacher_id varchar(20) not null,
    -> primary key(number),
    -> foreign key (teacher_id) references teacher (number)
    -> );
Query OK, 0 rows affected (0.03 sec)
```

#### 成绩表

- 学号
- 课程号
- 成绩

```
mysql> create table score(
    -> student_number varchar(20) not null,
    -> course_number varchar(20) not null,
    -> degree decimal,
    -> foreign key (student_number) references student (number),
    -> foreign key (course_number) references course (number),
    -> primary key(student_number, course_number)
    -> );
Query OK, 0 rows affected (0.03 sec)
```



### 添加数据

#### 添加学生数据

```
insert into student values('108','Allon','male','1995-03-13','143');
insert into student values('101','mohan','female','1998-05-31','133');
insert into student values('104','yuhan','female','1995-08-11','123');
insert into student values('106','goudan','male','1992-06-18','144');
insert into student values('102','xiaocui','female','1990-01-14','146');
```

#### 添加教师数据

```
insert into teacher values('001','TeacherA','male','1989-08-13','P','math');
insert into teacher values('004','TeacherB','female','1978-05-21','P','chinese');
insert into teacher values('006','TeacherC','male','1977-06-18','P','math');
insert into teacher values('007','TeacherD','female','1965-03-13','P','music');
insert into teacher values('008','TeacherE','male','1989-03-17','P','physics');
```

#### 添加课程表

```
insert into course values('3-105','computer','001');
insert into course values('4-165','math','006');
insert into course values('6-005','physics','008');
insert into course values('7-007','music','007');
```

#### 添加成绩表

```
insert into score values('108','3-105','99');
insert into score values('108','4-165','90');
insert into score values('108','6-005','68');
insert into score values('108','7-007','98');
insert into score values('101','3-105','79');
insert into score values('101','4-165','80');
insert into score values('101','6-005','88');
insert into score values('101','7-007','78');
insert into score values('104','3-105','89');
insert into score values('104','4-165','80');
insert into score values('104','6-005','88');
insert into score values('104','7-007','78');
insert into score values('106','3-105','79');
insert into score values('106','4-165','70');
insert into score values('106','6-005','78');
insert into score values('106','7-007','78');
insert into score values('102','3-105','99');
insert into score values('102','4-165','80');
insert into score values('102','6-005','78');
insert into score values('102','7-007','68');
```



### 查询练习

- 查询student表所有记录

  ```
  mysql> select * from student;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.01 sec)
  ```

- 查询student表中的所有记录的 name、sex 和 calss列信息

  ```
  mysql> select name, sex, class from student;
  +---------+--------+-------+
  | name    | sex    | class |
  +---------+--------+-------+
  | mohan   | female | 133   |
  | xiaocui | female | 146   |
  | yuhan   | female | 123   |
  | goudan  | male   | 144   |
  | Allon   | male   | 143   |
  +---------+--------+-------+
  5 rows in set (0.01 sec)
  ```

- 查询教师数据表里面不重复的depart列，**distinct去重查询**。

  ```
  ###所有信息
  mysql> select * from teacher;
  +--------+----------+--------+---------------------+------+---------+
  | number | name     | sex    | birthday            | prof | depart  |
  +--------+----------+--------+---------------------+------+---------+
  | 001    | TeacherA | male   | 1989-08-13 00:00:00 | P    | math    |
  | 004    | TeacherB | female | 1978-05-21 00:00:00 | P    | chinese |
  | 006    | TeacherC | male   | 1977-06-18 00:00:00 | P    | math    |
  | 007    | TeacherD | female | 1965-03-13 00:00:00 | P    | music   |
  | 008    | TeacherE | male   | 1989-03-17 00:00:00 | P    | physics |
  +--------+----------+--------+---------------------+------+---------+
  5 rows in set (0.03 sec)
  
  ###查询depart列不重复信息
  mysql> select distinct depart from teacher;
  +---------+
  | depart  |
  +---------+
  | math    |
  | chinese |
  | music   |
  | physics |
  +---------+
  4 rows in set (0.01 sec)
  ```

- 查询score表中成绩在60-80 之间的所有记录。

  ```
  ##所有数据
  mysql> select * from score;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 6-005         |     88 |
  | 101            | 7-007         |     78 |
  | 102            | 3-105         |     99 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 3-105         |     89 |
  | 104            | 4-165         |     80 |
  | 104            | 6-005         |     88 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 3-105         |     99 |
  | 108            | 4-165         |     90 |
  | 108            | 6-005         |     68 |
  | 108            | 7-007         |     98 |
  +----------------+---------------+--------+
  20 rows in set (0.01 sec)
  
  ###60-80区间数据
  mysql> select * from score where degree between 60 and 80;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 7-007         |     78 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 4-165         |     80 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 6-005         |     68 |
  +----------------+---------------+--------+
  13 rows in set (0.00 sec)
  
  ###方法二，运算符比较
  mysql> select * from score where degree >= 60 and degree <= 80;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 7-007         |     78 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 4-165         |     80 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 6-005         |     68 |
  +----------------+---------------+--------+
  13 rows in set (0.01 sec)
  ```

  注：在 MySQL 中，BETWEEN AND 能匹配指定范围内的所有值，**包括起始值和终止值**。

- 查询score表中，成绩为78，88的成绩，**表示或者关系查询 in，同一字段的or关系**。

  ```
  mysql> select * from score where degree in (78,88);
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 6-005         |     88 |
  | 101            | 7-007         |     78 |
  | 102            | 6-005         |     78 |
  | 104            | 6-005         |     88 |
  | 104            | 7-007         |     78 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  +----------------+---------------+--------+
  7 rows in set (0.01 sec)
  ```

- 查询student表中，班级143，或者性别为male的记录，**不同字段的or关系**。

  ```
  ###所有数据
  mysql> select * from student;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.00 sec)
  
  
  ##不同字段or查询
  mysql> select * from student where class='143' or sex='male';
  +--------+--------+------+---------------------+-------+
  | number | name   | sex  | birthday            | class |
  +--------+--------+------+---------------------+-------+
  | 106    | goudan | male | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon  | male | 1995-03-13 00:00:00 | 143   |
  +--------+--------+------+---------------------+-------+
  2 rows in set (0.01 sec)
  ```

- 以class降序查询student表中所有记录 **order by，升序asc，降序desc，默认升序**。

  ```
  mysql> select * from student order by class desc;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.01 sec)
  ```

- 以course_number升序，degree降序查询score表所有记录。

  ```
  ###所有数据
  mysql> select * from score;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 6-005         |     88 |
  | 101            | 7-007         |     78 |
  | 102            | 3-105         |     99 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 3-105         |     89 |
  | 104            | 4-165         |     80 |
  | 104            | 6-005         |     88 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 3-105         |     99 |
  | 108            | 4-165         |     90 |
  | 108            | 6-005         |     68 |
  | 108            | 7-007         |     98 |
  +----------------+---------------+--------+
  20 rows in set (0.01 sec)
  
  ###course_number升序，degree降序查询
  mysql> select * from score order by course_number asc, degree desc;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 102            | 3-105         |     99 |
  | 108            | 3-105         |     99 |
  | 104            | 3-105         |     89 |
  | 101            | 3-105         |     79 |
  | 106            | 3-105         |     79 |
  | 108            | 4-165         |     90 |
  | 101            | 4-165         |     80 |
  | 102            | 4-165         |     80 |
  | 104            | 4-165         |     80 |
  | 106            | 4-165         |     70 |
  | 101            | 6-005         |     88 |
  | 104            | 6-005         |     88 |
  | 102            | 6-005         |     78 |
  | 106            | 6-005         |     78 |
  | 108            | 6-005         |     68 |
  | 108            | 7-007         |     98 |
  | 101            | 7-007         |     78 |
  | 104            | 7-007         |     78 |
  | 106            | 7-007         |     78 |
  | 102            | 7-007         |     68 |
  +----------------+---------------+--------+
  20 rows in set (0.01 sec)
  ```

  注：**条件越靠前，优先级越高。**

- 查询student表143班学生人数，**统计count**。

  ```
  ###所有信息
  mysql> select * from student;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.00 sec)
  
  ###统计查询，count
  mysql> select count(*) from student where class='143';
  +----------+
  | count(*) |
  +----------+
  |        1 |
  +----------+
  1 row in set (0.01 sec)
  ```

- 查询score表中的最高分学生学号和课程号。**子查询or排序**。

  ```
  ####所有数据
  mysql> select * from score;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 6-005         |     88 |
  | 101            | 7-007         |     78 |
  | 102            | 3-105         |     99 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 3-105         |     89 |
  | 104            | 4-165         |     80 |
  | 104            | 6-005         |     88 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 3-105         |     99 |
  | 108            | 4-165         |     90 |
  | 108            | 6-005         |     68 |
  | 108            | 7-007         |     98 |
  +----------------+---------------+--------+
  20 rows in set (0.00 sec)
  
  ####子查询或者排序
  mysql> select student_number, course_number from score where degree=(select max(degree) from score);
  +----------------+---------------+
  | student_number | course_number |
  +----------------+---------------+
  | 102            | 3-105         |
  | 108            | 3-105         |
  +----------------+---------------+
  2 rows in set (0.03 sec)
  ```

  实际的步骤解析：

  1. 首先找到最高成绩

     ```
     select max(degree) from score;
     ```

  2. 然后找到最高成绩对应的学号，课程号

     ```
     select student_number, course_number from score where degree=(查询到的最高分);
     ```

- 查询每门课的平均成绩，**avg()，group by**。

  ```
  ###课程数据表
  mysql> select * from course;
  +--------+----------+------------+
  | number | name     | teacher_id |
  +--------+----------+------------+
  | 3-105  | computer | 001        |
  | 4-165  | math     | 006        |
  | 6-005  | physics  | 008        |
  | 7-007  | music    | 007        |
  +--------+----------+------------+
  4 rows in set (0.08 sec)
  
  ###3-105课程成绩
  mysql> select degree from score where course_number='3-105';
  +--------+
  | degree |
  +--------+
  |     79 |
  |     99 |
  |     89 |
  |     79 |
  |     99 |
  +--------+
  5 rows in set (0.00 sec)
  
  ###3-105课程平均成绩
  mysql> select avg(degree) from score where course_number='3-105';
  +-------------+
  | avg(degree) |
  +-------------+
  |     89.0000 |
  +-------------+
  1 row in set (0.01 sec)
  
  ###计算每一门课的平均成绩，group by 分组。
  mysql> select course_number, avg(degree) from score group by course_number;
  +---------------+-------------+
  | course_number | avg(degree) |
  +---------------+-------------+
  | 3-105         |     89.0000 |
  | 4-165         |     80.0000 |
  | 6-005         |     80.0000 |
  | 7-007         |     80.0000 |
  +---------------+-------------+
  4 rows in set (0.01 sec)
  ```

- 查询score表中，以3开头的课程平均成绩，且该课程最少有两名学生选修，**having count，like**。

  ```
  mysql> select course_number, avg(degree) from score group by course_number having count(course_number) >= 2 and course_number like '3%';
  +---------------+-------------+
  | course_number | avg(degree) |
  +---------------+-------------+
  | 3-105         |     89.0000 |
  +---------------+-------------+
  1 row in set (0.02 sec)
  ```

  注：like是模糊查询，可以理解为正则表达式，having count()是限制语句。

- 查询所有学生的name、course_number 和 degree列，**来自于不同的数据表**。

  ```
  ##
  mysql> select * from student;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.01 sec)
  
  ##
  mysql> select * from score;
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 101            | 4-165         |     80 |
  | 101            | 6-005         |     88 |
  | 101            | 7-007         |     78 |
  | 102            | 3-105         |     99 |
  | 102            | 4-165         |     80 |
  | 102            | 6-005         |     78 |
  | 102            | 7-007         |     68 |
  | 104            | 3-105         |     89 |
  | 104            | 4-165         |     80 |
  | 104            | 6-005         |     88 |
  | 104            | 7-007         |     78 |
  | 106            | 3-105         |     79 |
  | 106            | 4-165         |     70 |
  | 106            | 6-005         |     78 |
  | 106            | 7-007         |     78 |
  | 108            | 3-105         |     99 |
  | 108            | 4-165         |     90 |
  | 108            | 6-005         |     68 |
  | 108            | 7-007         |     98 |
  +----------------+---------------+--------+
  20 rows in set (0.00 sec)
  
  ###
  mysql> select name,course_number,degree from student,score where student.number=score.student_number;
  +---------+---------------+--------+
  | name    | course_number | degree |
  +---------+---------------+--------+
  | mohan   | 3-105         |     79 |
  | mohan   | 4-165         |     80 |
  | mohan   | 6-005         |     88 |
  | mohan   | 7-007         |     78 |
  | xiaocui | 3-105         |     99 |
  | xiaocui | 4-165         |     80 |
  | xiaocui | 6-005         |     78 |
  | xiaocui | 7-007         |     68 |
  | yuhan   | 3-105         |     89 |
  | yuhan   | 4-165         |     80 |
  | yuhan   | 6-005         |     88 |
  | yuhan   | 7-007         |     78 |
  | goudan  | 3-105         |     79 |
  | goudan  | 4-165         |     70 |
  | goudan  | 6-005         |     78 |
  | goudan  | 7-007         |     78 |
  | Allon   | 3-105         |     99 |
  | Allon   | 4-165         |     90 |
  | Allon   | 6-005         |     68 |
  | Allon   | 7-007         |     98 |
  +---------+---------------+--------+
  20 rows in set (0.01 sec)
  ```

  注：**多表查询，其实就是通过一个对应的参数，将两个数据表唯一的联系起来。这时候就体现出范式的重要性了。**所以，进行多表联合查询前， 先查看两个数据表是否有那些属性是相关的，比如这里是学生的编号。

- 查询所有学生的编号（number in student table），课程名字（name in course table） 分数（degree in score table）列。

  ```
  mysql> select student.number, course.name, score.degree from student, course, score
      -> where student.number = score.student_number
      -> and course.number = score.course_number;
  +--------+----------+--------+
  | number | name     | degree |
  +--------+----------+--------+
  | 101    | computer |     79 |
  | 102    | computer |     99 |
  | 104    | computer |     89 |
  | 106    | computer |     79 |
  | 108    | computer |     99 |
  | 101    | math     |     80 |
  | 102    | math     |     80 |
  | 104    | math     |     80 |
  | 106    | math     |     70 |
  | 108    | math     |     90 |
  | 101    | physics  |     88 |
  | 102    | physics  |     78 |
  | 104    | physics  |     88 |
  | 106    | physics  |     78 |
  | 108    | physics  |     68 |
  | 101    | music    |     78 |
  | 102    | music    |     68 |
  | 104    | music    |     78 |
  | 106    | music    |     78 |
  | 108    | music    |     98 |
  +--------+----------+--------+
  20 rows in set (0.01 sec)
  ```

  注：仍旧是注意表格间的相互关系。

- 查询所有学生的名字，课程名字，成绩列。**多表查询练习**。

  ```
  mysql> select student.name, course.name, score.degree from student, course, score
      -> where student.number = score.student_number
      -> and course.number = score.course_number;
  +---------+----------+--------+
  | name    | name     | degree |
  +---------+----------+--------+
  | mohan   | computer |     79 |
  | xiaocui | computer |     99 |
  | yuhan   | computer |     89 |
  | goudan  | computer |     79 |
  | Allon   | computer |     99 |
  | mohan   | math     |     80 |
  | xiaocui | math     |     80 |
  | yuhan   | math     |     80 |
  | goudan  | math     |     70 |
  | Allon   | math     |     90 |
  | mohan   | physics  |     88 |
  | xiaocui | physics  |     78 |
  | yuhan   | physics  |     88 |
  | goudan  | physics  |     78 |
  | Allon   | physics  |     68 |
  | mohan   | music    |     78 |
  | xiaocui | music    |     68 |
  | yuhan   | music    |     78 |
  | goudan  | music    |     78 |
  | Allon   | music    |     98 |
  +---------+----------+--------+
  20 rows in set (0.01 sec)
  ```

  注：仍是多表查询练习。

  tip：可以用as方法，给选择出来的数据列重新命名。

  ```
  select student.number as student_number from student;
  ```

- 查询某一个班级，每门课的平均分。

  ```
  mysql> select score.course_number, avg(score.degree) from score
      -> where score.student_number in (select student.number from student where student.class='143') 
      -> group by score.course_number;
  +---------------+-------------------+
  | course_number | avg(score.degree) |
  +---------------+-------------------+
  | 3-105         |           99.0000 |
  | 4-165         |           90.0000 |
  | 6-005         |           68.0000 |
  | 7-007         |           98.0000 |
  +---------------+-------------------+
  4 rows in set (0.01 sec)
  ```

  注意：体会查询过程中，不同条件的制约关系，品读在代码写法过程中的体现。就是所有的逻辑关系弄明白。

- 查询选修3-105课程的成绩高于109号同学3-105课程成绩，所有学生的成绩。

  ```
  select degree from score
  where degree > (select degree from score where student_number='108' and course_number='3-105') 
  and course_number='3-105';
  ```

  

- 函数 **year(), month(), day()** 对时间的操作。

  ```
  #数据表
  mysql> select * from student;
  +--------+---------+--------+---------------------+-------+
  | number | name    | sex    | birthday            | class |
  +--------+---------+--------+---------------------+-------+
  | 101    | mohan   | female | 1998-05-31 00:00:00 | 133   |
  | 102    | xiaocui | female | 1990-01-14 00:00:00 | 146   |
  | 104    | yuhan   | female | 1995-08-11 00:00:00 | 123   |
  | 106    | goudan  | male   | 1992-06-18 00:00:00 | 144   |
  | 108    | Allon   | male   | 1995-03-13 00:00:00 | 143   |
  +--------+---------+--------+---------------------+-------+
  5 rows in set (0.04 sec)
  
  #year()
  mysql> select year(birthday) from student;
  +----------------+
  | year(birthday) |
  +----------------+
  |           1998 |
  |           1990 |
  |           1995 |
  |           1992 |
  |           1995 |
  +----------------+
  5 rows in set (0.00 sec)
  
  #month()
  mysql> select month(birthday) from student;
  +-----------------+
  | month(birthday) |
  +-----------------+
  |               5 |
  |               1 |
  |               8 |
  |               6 |
  |               3 |
  +-----------------+
  5 rows in set (0.01 sec)
  
  #day()
  mysql> select day(birthday) from student;
  +---------------+
  | day(birthday) |
  +---------------+
  |            31 |
  |            14 |
  |            11 |
  |            18 |
  |            13 |
  +---------------+
  5 rows in set (0.00 sec)
  ```

- 查询某一教师的课程的学生成绩，多层嵌套子查询。

  ```
  mysql> select * from score
      -> where score.course_number = (select number from course where teacher_id = (select number from teacher where teacher.name='TeacherA'));
  +----------------+---------------+--------+
  | student_number | course_number | degree |
  +----------------+---------------+--------+
  | 101            | 3-105         |     79 |
  | 102            | 3-105         |     99 |
  | 104            | 3-105         |     89 |
  | 106            | 3-105         |     79 |
  | 108            | 3-105         |     99 |
  +----------------+---------------+--------+
  5 rows in set (0.02 sec)
  ```

  

### 参考

[一天学会MySQL](https://www.bilibili.com/video/BV1Vt411z7wy?p=19)

