
### SQL经典练习题

**使用方法：我用的数据库是MsSQL Server 2008，练习时应当自己建数据，自己先思考，切勿急躁翻答案！否则效果减半，做完这些题，恭喜你，你的SQL就算过关了。**

### 测试表格概述

1. 学生表：学生编号SId、学生姓名Sname、出生年月Sage、学生性别Ssex
2. 课程表：课程编号CId、课程名称Cname、教师编号TId
3. 教师表：教师编号TId、教师姓名Tname
4. 成绩表：学生编号SId、课程编号CId、分数score

### 创建上述表格并输入数据

1. 学生表Student

   ```
   create table Student(SId varchar(10),Sname varchar(10),Sage datetime,Ssex varchar(10));
   insert into Student values('01' , '赵雷' , '1990-01-01' , '男');
   insert into Student values('02' , '钱电' , '1990-12-21' , '男');
   insert into Student values('03' , '孙风' , '1990-05-20' , '男');
   insert into Student values('04' , '李云' , '1990-08-06' , '男');
   insert into Student values('05' , '周梅' , '1991-12-01' , '女');
   insert into Student values('06' , '吴兰' , '1992-03-01' , '女');
   insert into Student values('07' , '郑竹' , '1989-07-01' , '女');
   insert into Student values('09' , '张三' , '2017-12-20' , '女');
   insert into Student values('10' , '李四' , '2017-12-25' , '女');
   insert into Student values('11' , '李四' , '2017-12-30' , '女');
   insert into Student values('12' , '赵六' , '2017-01-01' , '女');
   insert into Student values('13' , '孙七' , '2018-01-01' , '女');
   ```

2. 课程表Course

   ```
   create table Course(CId varchar(10),Cname nvarchar(10),TId varchar(10));
   insert into Course values('01' , '语文' , '02');
   insert into Course values('02' , '数学' , '01');
   insert into Course values('03' , '英语' , '03');
   ```

3. 教师表Teacher

   ```
   create table Teacher(TId varchar(10),Tname varchar(10));
   insert into Teacher values('01' , '张三');
   insert into Teacher values('02' , '李四');
   insert into Teacher values('03' , '王五');
   ```

4. 成绩表SC

   ```
   create table SC(SId varchar(10),CId varchar(10),score decimal(18,1));
   insert into SC values('01' , '01' , 80);
   insert into SC values('01' , '02' , 90);
   insert into SC values('01' , '03' , 99);
   insert into SC values('02' , '01' , 70);
   insert into SC values('02' , '02' , 60);
   insert into SC values('02' , '03' , 80);
   insert into SC values('03' , '01' , 80);
   insert into SC values('03' , '02' , 80);
   insert into SC values('03' , '03' , 80);
   insert into SC values('04' , '01' , 50);
   insert into SC values('04' , '02' , 30);
   insert into SC values('04' , '03' , 20);
   insert into SC values('05' , '01' , 76);
   insert into SC values('05' , '02' , 87);
   insert into SC values('06' , '01' , 31);
   insert into SC values('06' , '03' , 34);
   insert into SC values('07' , '02' , 89);
   insert into SC values('07' , '03' , 98);
   ```

### 练习题目

1. **查询 "01" 课程比 "02" 课程成绩高的学生的信息及课程分数**

   ```
   ##01课程学生成绩
   mysql> select * from SC where SC.CId='01';
   +------+------+-------+
   | SId  | CId  | score |
   +------+------+-------+
   | 01   | 01   |  80.0 |
   | 02   | 01   |  70.0 |
   | 03   | 01   |  80.0 |
   | 04   | 01   |  50.0 |
   | 05   | 01   |  76.0 |
   | 06   | 01   |  31.0 |
   +------+------+-------+
   6 rows in set (0.02 sec)
   
   ##02课程学生成绩
   mysql> select * from SC where SC.CId='02';
   +------+------+-------+
   | SId  | CId  | score |
   +------+------+-------+
   | 01   | 02   |  90.0 |
   | 02   | 02   |  60.0 |
   | 03   | 02   |  80.0 |
   | 04   | 02   |  30.0 |
   | 05   | 02   |  87.0 |
   | 07   | 02   |  89.0 |
   +------+------+-------+
   6 rows in set (0.01 sec)
   
   ##学生信息
   mysql> select * from Student;
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   | 09   | 张三   | 2017-12-20 00:00:00 | 女   |
   | 10   | 李四   | 2017-12-25 00:00:00 | 女   |
   | 11   | 李四   | 2017-12-30 00:00:00 | 女   |
   | 12   | 赵六   | 2017-01-01 00:00:00 | 女   |
   | 13   | 孙七   | 2018-01-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   12 rows in set (0.00 sec)
   
   ##01课程比02课程成绩高的学生信息和成绩，不完全的学生信息
   mysql> SELECT A.SId,A.score as '语文',B.score as '数学' 
       -> FROM (select * from SC where SC.CId='01') as A
       -> LEFT JOIN (select * from SC where SC.CId='02') as B
       -> ON A.SId=B.SId
       -> WHERE A.score>B.score;
   +------+--------+--------+
   | SId  | 语文   | 数学   |
   +------+--------+--------+
   | 02   |   70.0 |   60.0 |
   | 04   |   50.0 |   30.0 |
   +------+--------+--------+
   2 rows in set (0.00 sec)
   
   ##完全的学生信息
   mysql> SELECT st.*,A.score as '语文',B.score as '数学' 
       -> FROM (select * from SC where SC.CId='01') as A
       -> LEFT JOIN (select * from SC where SC.CId='02') as B ON A.SId=B.SId
       -> LEFT JOIN Student as st ON st.SID=A.SId
       -> WHERE A.score>B.score;
   +------+--------+---------------------+------+--------+--------+
   | SId  | Sname  | Sage                | Ssex | 语文   | 数学   |
   +------+--------+---------------------+------+--------+--------+
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |   70.0 |   60.0 |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |   50.0 |   30.0 |
   +------+--------+---------------------+------+--------+--------+
   2 rows in set (0.00 sec)
   
   
   ```

   - **查询同时存在"01"课程和"02"课程的情况**

     ```
     mysql> SELECT S01.SId, S01.score, S02.score FROM
         -> (SELECT SId, score FROM SC WHERE CId='01') as S01 ,
         -> (SELECT SId, score FROM SC WHERE CId='02') as S02
         -> WHERE S01.SId=S02.SId;
     +------+-------+-------+
     | SId  | score | score |
     +------+-------+-------+
     | 01   |  80.0 |  90.0 |
     | 02   |  70.0 |  60.0 |
     | 03   |  80.0 |  80.0 |
     | 04   |  50.0 |  30.0 |
     | 05   |  76.0 |  87.0 |
     +------+-------+-------+
     5 rows in set (0.01 sec)
     ```

   - **查询存在"01"课程但可能不存在"02"课程的情况(不存在时显示为null)**

     ```
     mysql> SELECT S01.SId, S01.score as '01', S02.score as '02' FROM
         -> (SELECT * FROM SC WHERE CId = '02') as S02
         -> RIGHT JOIN
         -> (SELECT * FROM SC WHERE CId = '01') as S01
         -> ON S01.SId = S02.SId;
     +------+------+------+
     | SId  | 01   | 02   |
     +------+------+------+
     | 01   | 80.0 | 90.0 |
     | 02   | 70.0 | 60.0 |
     | 03   | 80.0 | 80.0 |
     | 04   | 50.0 | 30.0 |
     | 05   | 76.0 | 87.0 |
     | 06   | 31.0 | NULL |
     +------+------+------+
     6 rows in set (0.00 sec)
     ```

   - **查询不存在"01"课程但存在"02"课程的情况** 

     ```
     mysql> SELECT S01.SId, S01.CId, S01.score FROM
         -> (SELECT * FROM SC WHERE CId != '01') as S01
         -> INNER JOIN
         -> (SELECT * FROM SC WHERE CId = '02') as S02
         -> ON S01.SId = S02.SId;
     +------+------+-------+
     | SId  | CId  | score |
     +------+------+-------+
     | 01   | 02   |  90.0 |
     | 01   | 03   |  99.0 |
     | 02   | 02   |  60.0 |
     | 02   | 03   |  80.0 |
     | 03   | 02   |  80.0 |
     | 03   | 03   |  80.0 |
     | 04   | 02   |  30.0 |
     | 04   | 03   |  20.0 |
     | 05   | 02   |  87.0 |
     | 07   | 02   |  89.0 |
     | 07   | 03   |  98.0 |
     +------+------+-------+
     11 rows in set (0.00 sec)
     ```
     
     

2. **查询平均成绩大于等于60分的同学的学生编号和学生姓名和平均成绩**

   ```
   ##Method one
   mysql> SELECT avg_score.SId, st.Sname, avg_score.a
       -> FROM Student as st, (SELECT SId, AVG(score) as a FROM SC
       -> GROUP BY SId) as avg_score
       -> WHERE avg_score.a>60 
       -> AND avg_score.SId=st.SId;
   +------+--------+----------+
   | SId  | Sname  | a        |
   +------+--------+----------+
   | 01   | 赵雷   | 89.66667 |
   | 02   | 钱电   | 70.00000 |
   | 03   | 孙风   | 80.00000 |
   | 05   | 周梅   | 81.50000 |
   | 07   | 郑竹   | 93.50000 |
   +------+--------+----------+
   5 rows in set (0.01 sec)
   
   ##Method two
   mysql> SELECT avg_score.SId, st.Sname, avg_score.a
       -> FROM (SELECT SId, AVG(score) as a FROM SC GROUP BY SId) as avg_score
       -> LEFT JOIN Student as st
       -> ON avg_score.SId=st.SId
       -> WHERE avg_score.a>60;
   +------+--------+----------+
   | SId  | Sname  | a        |
   +------+--------+----------+
   | 01   | 赵雷   | 89.66667 |
   | 02   | 钱电   | 70.00000 |
   | 03   | 孙风   | 80.00000 |
   | 05   | 周梅   | 81.50000 |
   | 07   | 郑竹   | 93.50000 |
   +------+--------+----------+
   5 rows in set (0.01 sec)
   
   ```

   注：多个条件查询 ===> 将一些条件转化成中间表格，然后再取数据。

3. **查询在SC表存在成绩的学生信息**

   ```
   mysql> SELECT Student.* FROM Student, (SELECT DISTINCT SId FROM SC) as A
       -> WHERE Student.SId=A.SId;
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   7 rows in set (0.01 sec)
   ```

   

4. **查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩（没成绩的显示null）**

   ```
   mysql> SELECT st.SId, st.Sname, A.id, A.score FROM
       -> (SELECT SC.SId, COUNT(SC.CId) as id, SUM(SC.score) as score FROM SC
       -> GROUP BY SC.SId) as A
       -> RIGHT JOIN Student as st
       -> ON st.SId=A.SId;
   +------+--------+------+-------+
   | SId  | Sname  | id   | score |
   +------+--------+------+-------+
   | 01   | 赵雷   |    3 | 269.0 |
   | 02   | 钱电   |    3 | 210.0 |
   | 03   | 孙风   |    3 | 240.0 |
   | 04   | 李云   |    3 | 100.0 |
   | 05   | 周梅   |    2 | 163.0 |
   | 06   | 吴兰   |    2 |  65.0 |
   | 07   | 郑竹   |    2 | 187.0 |
   | 09   | 张三   | NULL |  NULL |
   | 10   | 李四   | NULL |  NULL |
   | 11   | 李四   | NULL |  NULL |
   | 12   | 赵六   | NULL |  NULL |
   | 13   | 孙七   | NULL |  NULL |
   +------+--------+------+-------+
   12 rows in set (0.00 sec)
   ```

   - **查有成绩的学生信息**

     ```
     mysql> SELECT st.*, A.id as '选课总数', A.score as '总成绩' FROM
         -> (SELECT SC.SId, COUNT(SC.CId) as id, SUM(SC.score) as score FROM SC GROUP BY SC.SId) as A
         -> LEFT JOIN Student as st
         -> ON st.SId=A.SId;
     +------+--------+---------------------+------+--------------+-----------+
     | SId  | Sname  | Sage                | Ssex | 选课总数     | 总成绩    |
     +------+--------+---------------------+------+--------------+-----------+
     | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |            3 |     269.0 |
     | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |            3 |     210.0 |
     | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |            3 |     240.0 |
     | 04   | 李云   | 1990-08-06 00:00:00 | 男   |            3 |     100.0 |
     | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |            2 |     163.0 |
     | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |            2 |      65.0 |
     | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |            2 |     187.0 |
     +------+--------+---------------------+------+--------------+-----------+
     7 rows in set (0.01 sec)
     ```
     
     

5. **查询「李」姓老师的数量**

   ```
   ##MY answer
   mysql> SELECT COUNT(A.TId) FROM
       -> (SELECT * FROM Teacher WHERE Tname LIKE '李%') as A;
   +--------------+
   | COUNT(A.TId) |
   +--------------+
   |            1 |
   +--------------+
   1 row in set (0.01 sec)
   
   ##REFERENCE
   mysql> SELECT COUNT(*)李姓老师数量 FROM Teacher WHERE Tname LIKE '李%';
   +--------------------+
   | 李姓老师数量       |
   +--------------------+
   |                  1 |
   +--------------------+
   1 row in set (0.00 sec)
   ```

   

6. **查询学过「张三」老师授课的同学信息**

   ```
   mysql> SELECT st.* FROM 
       -> Student as st, (select * from SC where CId='01') as A
       -> WHERE st.SId=A.SId;
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   6 rows in set (0.00 sec)
   ```

   

7. **查询没有学全所有课程的同学的信息**

   ```
   ##MY answer
   mysql> SELECT st.* FROM 
       -> (SELECT * FROM
       -> (SELECT SC.SId, count(SC.CId) as '课程数' FROM SC
       -> GROUP BY SC.SId) AS A
       -> WHERE A.课程数 < (SELECT COUNT(*) FROM Course)
       -> ) AS B
       -> LEFT JOIN Student AS st
       -> ON B.SId=St.SId;
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   3 rows in set (0.01 sec)
   
   ##REFERENCE
   mysql> SELECT * FROM Student 
       -> WHERE SId IN (SELECT SId FROM SC GROUP BY SId HAVING COUNT(CId)<3);
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   3 rows in set (0.02 sec)
   ```

   

8. **查询至少有一门课程与学号为"01"的同学所学相同的同学信息**

   ```
   ###MY ANSWER
   mysql> SELECT Student.* FROM Student,
       -> (SELECT SC.SId FROM SC, (SELECT * FROM SC WHERE SC.SId='01') AS A
       -> WHERE SC.CId IN (A.CId)
       -> GROUP BY SC.SId) AS B
       -> WHERE Student.SId=B.SId; 
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   7 rows in set (0.01 sec)
   
   ###REFERENCE
   mysql> SELECT * FROM Student
       -> WHERE SId IN
       -> (SELECT DISTINCT SId FROM SC WHERE CId IN (SELECT CId FROM SC WHERE SID='01'));
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
   | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
   | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
   +------+--------+---------------------+------+
   7 rows in set (0.00 sec)
   ```

   

9. **查询和"01"号的同学学习的课程完全相同的其他同学的信息**

   ```
   ###REFERENCE
   mysql> SELECT * FROM Student
       -> WHERE SId IN
       -> (SELECT DISTINCT SId FROM SC WHERE CId IN (SELECT CId FROM SC WHERE SID='01') AND SId<>'01'
    -> GROUP BY SID
       -> HAVING 
       -> COUNT(CId) >= 3
       -> );
   +------+--------+---------------------+------+
   | SId  | Sname  | Sage                | Ssex |
   +------+--------+---------------------+------+
   | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
   | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
   | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
   +------+--------+---------------------+------+
   3 rows in set (0.01 sec)
   
   
   ###MY ANSWER
   
   ```
   
   参考答案这里给出的，只是说和"01"学生选修的课程数目相同（在本数据库中=学习课程一样），但是并没有给出学习课程一样的判断。
   
10. **查询没学过「张三」老师讲授的任一门课程的学生姓名**

   ```
   ##REFERENC
   mysql> SELECT Sname FROM Student
       -> WHERE SId NOT IN (SELECT SId FROM SC
       -> WHERE CId IN (SELECT CId FROM Course WHERE TId = (SELECT TId FROM Teacher WHERE Tname='张三'))
       -> );
   +--------+
   | Sname  |
   +--------+
   | 吴兰   |
   | 张三   |
   | 李四   |
   | 李四   |
   | 赵六   |
   | 孙七   |
   +--------+
   6 rows in set (0.00 sec)
   ```

   这里：先选出学习「张三」老师的学生ID，然后用NOT IN在学生表里面排除掉。

11. **查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩 **

    ```
    ###MY ANSWER
    mysql> SELECT A.SId, st.Sname, A.平均成绩 FROM Student as st,
        -> (SELECT SId,COUNT(CId) AS '不及格课程数', AVG(score) AS "平均成绩" FROM SC
        -> WHERE score < 60 GROUP BY SId) AS A
        -> WHERE A.SId=st.SId AND A.不及格课程数>=2
        -> ;
    +------+--------+--------------+
    | SId  | Sname  | 平均成绩     |
    +------+--------+--------------+
    | 04   | 李云   |     33.33333 |
    | 06   | 吴兰   |     32.50000 |
    +------+--------+--------------+
    2 rows in set (0.00 sec)
    
    ###REFERENCE
    mysql> SELECT A.SId, A.Sname, B.平均成绩 FROM  Student AS A 
           RIGHT JOIN 
           (SELECT SId, AVG(score)平均成绩 FROM SC WHERE score<60 GROUP BY SId HAVING COUNT(score)>=2)B 
           ON A.SId=B.SId;
    +------+--------+--------------+
    | SId  | Sname  | 平均成绩     |
    +------+--------+--------------+
    | 04   | 李云   |     33.33333 |
    | 06   | 吴兰   |     32.50000 |
    +------+--------+--------------+
    2 rows in set (0.01 sec)
    ```

    

12. **检索" 01 "课程分数小于 60，按分数降序排列的学生信息**

    ```
    mysql> SELECT SId, score FROM SC
        -> WHERE CId='01' AND score<60
        -> ORDER BY score DESC;
    +------+-------+
    | SId  | score |
    +------+-------+
    | 04   |  50.0 |
    | 06   |  31.0 |
    +------+-------+
    2 rows in set (0.00 sec)
    ```

    注意：order by 放在最后。可以理解为：先按照条件选出数据，然后再排序。

13. **按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩，CASE方法**

    ```
    mysql> SELECT SId, SUM(score)总成绩, AVG(score)平均成绩 FROM SC
        -> GROUP BY SId
        -> ORDER BY 平均成绩 DESC;
    +------+-----------+--------------+
    | SId  | 总成绩    | 平均成绩     |
    +------+-----------+--------------+
    | 07   |     187.0 |     93.50000 |
    | 01   |     269.0 |     89.66667 |
    | 05   |     163.0 |     81.50000 |
    | 03   |     240.0 |     80.00000 |
    | 02   |     210.0 |     70.00000 |
    | 04   |     100.0 |     33.33333 |
    | 06   |      65.0 |     32.50000 |
    +------+-----------+--------------+
    7 rows in set (0.00 sec)
    
    ###REFERENCE
    mysql> select SId, 
        -> max(case CId when '01' then score else 0 end)'01',
        -> max(case CId when '02' then score else 0 end)'02',
        -> max(case CId when '03' then score else 0 end)'03',
        -> AVG(score)平均分 from SC
        -> group by SId order by 平均分 desc;
    +------+------+------+------+-----------+
    | SId  | 01   | 02   | 03   | 平均分    |
    +------+------+------+------+-----------+
    | 07   |  0.0 | 89.0 | 98.0 |  93.50000 |
    | 01   | 80.0 | 90.0 | 99.0 |  89.66667 |
    | 05   | 76.0 | 87.0 |  0.0 |  81.50000 |
    | 03   | 80.0 | 80.0 | 80.0 |  80.00000 |
    | 02   | 70.0 | 60.0 | 80.0 |  70.00000 |
    | 04   | 50.0 | 30.0 | 20.0 |  33.33333 |
    | 06   | 31.0 |  0.0 | 34.0 |  32.50000 |
    +------+------+------+------+-----------+
    7 rows in set (0.00 sec)
    ```

    

14. **查询各科成绩最高分、最低分和平均分：**

     以如下形式显示：课程 ID，课程 name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率及格为>=60，中等为：70-80，优良为：80-90，优秀为：>=90要求输出课程号和选修人数，查询结果按人数降序排列，若人数相同，按课程号升序排列

    ```
    SELECT A.01 as 语文, A.02 as 数学, A.03 as 英语 FROM
    (SELECT SId AS 学号,
    MAX(CASE CID WHEN '01' THEN score ELSE 0 END) AS '01',
    MAX(CASE CID WHEN '02' THEN score ELSE 0 END) AS '02',
    MAX(CASE CID WHEN '03' THEN score ELSE 0 END) AS '03'
    FROM SC GROUP BY SId;) AS A
    
    ##某一门课程；最高分，最低分，平均分
    SELECT CId, COUNT(0)选修人数, MAX(score)最高分, MIN(score)最低分, AVG(score)平均分 FROM SC WHERE CId='01';
    
    SELECT SC.CId, A.选修人数, A.最高分, A.最低分, A.平均分 FROM SC
    LEFT JOIN (SELECT CId, COUNT(0)选修人数, MAX(score)最高分, MIN(score)最低分, AVG(score)平均分 FROM SC WHERE CId=SC.CId) AS A
    ON A.CId=SC.CId
    GROUP BY SC.CId
    ```

    

15. **按各科成绩进行排序，并显示排名， Score 重复时保留名次空缺**

    ```
    ##
    mysql> SELECT A.score, A.ranking From
        -> (SELECT
        -> @rank_counter := @rank_counter + 1 AS rank,
        -> IF(@pre_score = SC.score, @cur_rank, @cur_rank := @rank_counter) AS ranking,
        -> (@pre_score := Sc.score) AS score
        -> FROM SC, (SELECT @cur_rank := 0, @pre_score := NULL, @rank_counter := 0) AS R
        -> ORDER BY SC.score DESC) AS A;
    +-------+---------+
    | score | ranking |
    +-------+---------+
    |  99.0 |       1 |
    |  98.0 |       2 |
    |  90.0 |       3 |
    |  89.0 |       4 |
    |  87.0 |       5 |
    |  80.0 |       6 |
    |  80.0 |       6 |
    |  80.0 |       6 |
    |  80.0 |       6 |
    |  80.0 |       6 |
    |  76.0 |      11 |
    |  70.0 |      12 |
    |  60.0 |      13 |
    |  50.0 |      14 |
    |  34.0 |      15 |
    |  31.0 |      16 |
    |  30.0 |      17 |
    |  20.0 |      18 |
    +-------+---------+
    18 rows in set (0.00 sec)
    ```

    

    - **按各科成绩进行排序，并显示排名， Score 重复时合并名次**

      ```
      mysql> SELECT 
          -> IF(@pre_score = SC.score, @cur_rank, @cur_rank := @cur_rank + 1) AS ranking,
          -> (@pre_score := Sc.score) AS core
          -> FROM SC, (SELECT @cur_rank := 0, @pre_score := NULL) AS R
          -> ORDER BY SC.score DESC;
      +---------+------+
      | ranking | core |
      +---------+------+
      |       1 | 99.0 |
      |       2 | 98.0 |
      |       3 | 90.0 |
      |       4 | 89.0 |
      |       5 | 87.0 |
      |       6 | 80.0 |
      |       6 | 80.0 |
      |       6 | 80.0 |
      |       6 | 80.0 |
      |       6 | 80.0 |
      |       7 | 76.0 |
      |       8 | 70.0 |
      |       9 | 60.0 |
      |      10 | 50.0 |
      |      11 | 34.0 |
      |      12 | 31.0 |
      |      13 | 30.0 |
      |      14 | 20.0 |
      +---------+------+
      18 rows in set (0.00 sec)
      ```

      

16. **查询学生的总成绩，并进行排名，总分重复时保留名次空缺**

    ```
    ###学生总成绩按降序排列
    mysql> SELECT SId, SUM(score) AS score FROM SC GROUP BY SId ORDER BY score DESC ;
    +------+-------+
    | SId  | score |
    +------+-------+
    | 01   | 269.0 |
    | 03   | 240.0 |
    | 02   | 210.0 |
    | 07   | 187.0 |
    | 05   | 163.0 |
    | 04   | 100.0 |
    | 06   |  65.0 |
    +------+-------+
    7 rows in set (0.00 sec)
    
    ##参考15题第一题，把SC表换成上面的表（A）
    mysql> SELECT B.SId, B.score, B.ranking From
        -> (SELECT
        -> A.SId,
        -> @rank_counter := @rank_counter + 1 AS rank,
        -> IF(@pre_score = A.score, @cur_rank, @cur_rank := @rank_counter) AS ranking,
        -> (@pre_score := A.score) AS score
        -> FROM (SELECT SId, SUM(score) AS score FROM SC GROUP BY SId ORDER BY score DESC) AS A, (SELECT @cur_rank := 0, @pre_score := NULL, @rank_counter := 0) AS R
        -> ORDER BY A.score DESC) AS B;
    +------+-------+---------+
    | SId  | score | ranking |
    +------+-------+---------+
    | 01   | 269.0 |       1 |
    | 03   | 240.0 |       2 |
    | 02   | 210.0 |       3 |
    | 07   | 187.0 |       4 |
    | 05   | 163.0 |       5 |
    | 04   | 100.0 |       6 |
    | 06   |  65.0 |       7 |
    +------+-------+---------+
    7 rows in set (0.00 sec)
    ```

    

    - **查询学生的总成绩，并进行排名，总分重复时不保留名次空缺**

      ```
      ###参考16题第一题，15题第二题
      mysql> SELECT 
          -> A.SId,
          -> IF(@pre_score = A.score, @cur_rank, @cur_rank := @cur_rank + 1) AS ranking,
          -> (@pre_score := A.score) AS core
          -> FROM (SELECT SId, SUM(score) AS score FROM SC GROUP BY SId ORDER BY score DESC) AS A, (SELECT @cur_rank := 0, @pre_score := NULL) AS R
          -> ORDER BY A.score DESC;
      +------+---------+-------+
      | SId  | ranking | core  |
      +------+---------+-------+
      | 01   |       1 | 269.0 |
      | 03   |       2 | 240.0 |
      | 02   |       3 | 210.0 |
      | 07   |       4 | 187.0 |
      | 05   |       5 | 163.0 |
      | 04   |       6 | 100.0 |
      | 06   |       7 |  65.0 |
      +------+---------+-------+
      7 rows in set (0.01 sec)
      ```

      

17. **统计各科成绩各分数段人数：课程编号，课程名称，[100-85]，[85-70]，[70-60]，[60-0] 及所占百分比**

    ```
    SELECT CId, SUM(CId) FROM SC GROUP BY CId;
    
    (CASE WHEN 85<score<=100 THEN )
    
    ###
    mysql> select * from SC where CId='01'
        -> ;
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 01   | 01   |  80.0 |
    | 02   | 01   |  70.0 |
    | 03   | 01   |  80.0 |
    | 04   | 01   |  50.0 |
    | 05   | 01   |  76.0 |
    | 06   | 01   |  31.0 |
    +------+------+-------+
    6 rows in set (0.00 sec)
    
    ##
    SELECT 
    A.SId
    FROM (select * from SC where CId='01') AS A
    WHERE A.score>=85 AND A.score<=100;
    
    ###
    SELECT 
    ```

    

18. **查询各科成绩前三名的记录**

    ```
    ###指定某门课程的前三名
    mysql> SELECT * FROM SC WHERE CId='01' ORDER BY score DESC LIMIT 3;
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 01   | 01   |  80.0 |
    | 03   | 01   |  80.0 |
    | 05   | 01   |  76.0 |
    +------+------+-------+
    3 rows in set (0.00 sec)
    
    ###如何全部课程一起查询前三名呢,使用UNION ALL
    mysql> (SELECT * FROM SC WHERE CId='01' ORDER BY score DESC LIMIT 3)
        -> UNION ALL
        -> (SELECT * FROM SC WHERE CId='02' ORDER BY score DESC LIMIT 3)
        -> UNION ALL
        -> (SELECT * FROM SC WHERE CId='03' ORDER BY score DESC LIMIT 3);
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 01   | 01   |  80.0 |
    | 03   | 01   |  80.0 |
    | 05   | 01   |  76.0 |
    | 01   | 02   |  90.0 |
    | 07   | 02   |  89.0 |
    | 05   | 02   |  87.0 |
    | 01   | 03   |  99.0 |
    | 07   | 03   |  98.0 |
    | 02   | 03   |  80.0 |
    +------+------+-------+
    9 rows in set (0.00 sec)
    ```

    

19. **查询每门课程被选修的学生数 **

    ```
    mysql> SELECT CId, COUNT(SId) AS 人数 FROM SC
        -> GROUP BY CId;
    +------+--------+
    | CId  | 人数   |
    +------+--------+
    | 01   |      6 |
    | 02   |      6 |
    | 03   |      6 |
    +------+--------+
    3 rows in set (0.00 sec)
    ```

    

20. **查询出只选修两门课程的学生学号和姓名 **

    ```
    mysql> SELECT Student.SId, Student.Sname FROM Student
        -> WHERE SId IN
        -> (SELECT SId FROM SC GROUP BY SId HAVING COUNT(CId)=2);
    +------+--------+
    | SId  | Sname  |
    +------+--------+
    | 05   | 周梅   |
    | 06   | 吴兰   |
    | 07   | 郑竹   |
    +------+--------+
    3 rows in set (0.00 sec)
    ```

21. **查询男生、女生人数**

    ```
    mysql> SELECT
        -> (SELECT COUNT(*) FROM Student WHERE Ssex='男')男生人数,
        -> (SELECT COUNT(*) FROM Student WHERE Ssex='女')女生人数;
    +--------------+--------------+
    | 男生人数     | 女生人数     |
    +--------------+--------------+
    |            4 |            8 |
    +--------------+--------------+
    1 row in set (0.00 sec)
    
    ###REFERENCE
    mysql> SELECT Student.Ssex, COUNT(*) AS 人数
        -> FROM Student
        -> GROUP BY Student.Ssex;
    +------+--------+
    | Ssex | 人数   |
    +------+--------+
    | 女   |      8 |
    | 男   |      4 |
    +------+--------+
    2 rows in set (0.00 sec)
    ```

    

22. **查询名字中含有「风」字的学生信息**

    ```
    mysql> SELECT * FROM Student
        -> WHERE Sname LIKE '%风%';
    +------+--------+---------------------+------+
    | SId  | Sname  | Sage                | Ssex |
    +------+--------+---------------------+------+
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
    +------+--------+---------------------+------+
    1 row in set (0.00 sec)
    ```

    

23. **查询同名同性学生名单，并统计同名人数**

    ```
    mysql> SELECT Sname, COUNT(Sname) AS 同名人数 FROM Student
        -> GROUP BY Sname
        -> HAVING COUNT(Sname)>=2;
    +--------+--------------+
    | Sname  | 同名人数     |
    +--------+--------------+
    | 李四   |            2 |
    +--------+--------------+
    1 row in set (0.01 sec)
    ```

    

24. **查询 1990 年出生的学生名单**

    ```
    mysql> SELECT * FROM Student
        -> WHERE YEAR(Sage)='1990';
    +------+--------+---------------------+------+
    | SId  | Sname  | Sage                | Ssex |
    +------+--------+---------------------+------+
    | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
    | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
    | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
    +------+--------+---------------------+------+
    4 rows in set (0.00 sec)
    
    ###REFERENCE
    mysql> SELECT * FROM Student
        -> WHERE Sage LIKE '1990%';
    +------+--------+---------------------+------+
    | SId  | Sname  | Sage                | Ssex |
    +------+--------+---------------------+------+
    | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
    | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
    | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
    +------+--------+---------------------+------+
    4 rows in set, 1 warning (0.01 sec)
    ```

    

25. **查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按课程编号升序排列**

    ```
    mysql> SELECT CId, AVG(score) AS 平均成绩 FROM SC
        -> GROUP BY CID
        -> ORDER BY 平均成绩 DESC, CId ASC;
    +------+--------------+
    | CId  | 平均成绩     |
    +------+--------------+
    | 02   |     72.66667 |
    | 03   |     68.50000 |
    | 01   |     64.50000 |
    +------+--------------+
    3 rows in set (0.00 sec)
    ```

    

26. **查询平均成绩大于等于 85 的所有学生的学号、姓名和平均成绩 **

    ```
    mysql> SELECT A.SId, Student.Sname, A.平均成绩 FROM
        -> (SELECT SId, AVG(score) AS 平均成绩 FROM SC GROUP BY SID HAVING 平均成绩>=85) AS A
        -> LEFT JOIN Student ON Student.SId=A.SId;
    +------+--------+--------------+
    | SId  | Sname  | 平均成绩     |
    +------+--------+--------------+
    | 01   | 赵雷   |     89.66667 |
    | 07   | 郑竹   |     93.50000 |
    +------+--------+--------------+
    2 rows in set (0.00 sec)
    ```

    

27. **查询课程名称为「数学」，且分数低于 60 的学生姓名和分数 **

    ```
    mysql> SELECT Student.Sname, A.score AS 数学成绩 FROM
        -> (SELECT SId,score FROM SC
        -> WHERE CId=(SELECT CId FROM Course WHERE Cname='数学') AND score<60) AS A
        -> LEFT JOIN Student
        -> ON Student.SId=A.SId
        -> ;
    +--------+--------------+
    | Sname  | 数学成绩     |
    +--------+--------------+
    | 李云   |         30.0 |
    +--------+--------------+
    1 row in set (0.00 sec)
    ```

    

28. **查询所有学生的课程及分数情况（存在学生没成绩，没选课的情况）**

    ```
    mysql> SELECT Student.Sname, Student.SId, SC.CId, score FROM
        -> Student
        -> LEFT JOIN
        -> SC
        -> ON Student.SId=SC.SId;
    +--------+------+------+-------+
    | Sname  | SId  | CId  | score |
    +--------+------+------+-------+
    | 赵雷   | 01   | 01   |  80.0 |
    | 赵雷   | 01   | 02   |  90.0 |
    | 赵雷   | 01   | 03   |  99.0 |
    | 钱电   | 02   | 01   |  70.0 |
    | 钱电   | 02   | 02   |  60.0 |
    | 钱电   | 02   | 03   |  80.0 |
    | 孙风   | 03   | 01   |  80.0 |
    | 孙风   | 03   | 02   |  80.0 |
    | 孙风   | 03   | 03   |  80.0 |
    | 李云   | 04   | 01   |  50.0 |
    | 李云   | 04   | 02   |  30.0 |
    | 李云   | 04   | 03   |  20.0 |
    | 周梅   | 05   | 01   |  76.0 |
    | 周梅   | 05   | 02   |  87.0 |
    | 吴兰   | 06   | 01   |  31.0 |
    | 吴兰   | 06   | 03   |  34.0 |
    | 郑竹   | 07   | 02   |  89.0 |
    | 郑竹   | 07   | 03   |  98.0 |
    | 张三   | 09   | NULL |  NULL |
    | 李四   | 10   | NULL |  NULL |
    | 李四   | 11   | NULL |  NULL |
    | 赵六   | 12   | NULL |  NULL |
    | 孙七   | 13   | NULL |  NULL |
    +--------+------+------+-------+
    23 rows in set (0.00 sec)
    ```

    

29. **查询任何一门课程成绩在 70 分以上的姓名、课程名称和分数**

    ```
    ###MY ANSWER，改动课程ID就可以查询该课程高于70分的同学信息
    mysql> SELECT Student.Sname, A.CId, score FROM
        -> Student,
        -> (SELECT * FROM SC WHERE CId='01' HAVING score>70) AS A
        -> WHERE Student.SId=A.SId
        -> ;
    +--------+------+-------+
    | Sname  | CId  | score |
    +--------+------+-------+
    | 赵雷   | 01   |  80.0 |
    | 孙风   | 01   |  80.0 |
    | 周梅   | 01   |  76.0 |
    +--------+------+-------+
    3 rows in set (0.01 sec)
    
    ##是我理解有问题吗？其他答案是：在所有课程里面选出70分以上的信息？？？
    
    ```

    

30. **查询不及格的课程**

    ```
    mysql> select * from SC
        -> where score<60;
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 04   | 01   |  50.0 |
    | 04   | 02   |  30.0 |
    | 04   | 03   |  20.0 |
    | 06   | 01   |  31.0 |
    | 06   | 03   |  34.0 |
    +------+------+-------+
    5 rows in set (0.01 sec)
    ```

    

31. **查询课程编号为 01 且课程成绩在 80 分及以上的学生的学号和姓名**

    ```
    mysql> SELECT Student.SID, Student.Sname, A.score FROM
        -> Student,
        -> (SELECT * FROM SC 
        -> WHERE CId='01' AND score>=80) AS A
        -> WHERE Student.SId=A.SId;
    +------+--------+-------+
    | SID  | Sname  | score |
    +------+--------+-------+
    | 01   | 赵雷   |  80.0 |
    | 03   | 孙风   |  80.0 |
    +------+--------+-------+
    2 rows in set (0.01 sec)
    ```

    

32. **求每门课程的学生人数 **

    ```
    mysql> SELECT CId, COUNT(SId) AS 人数 FROM SC
        -> GROUP BY CId;
    +------+--------+
    | CId  | 人数   |
    +------+--------+
    | 01   |      6 |
    | 02   |      6 |
    | 03   |      6 |
    +------+--------+
    3 rows in set (0.00 sec)
    ```

    

33. **成绩不重复，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩**

    ```
    ##成绩不重复：首先找出「张三」老师所授课程的成绩表A，然后以降序排列，取第一个就是成绩最高的。
    mysql> SELECT A.SId, A.score FROM
        -> (SELECT * FROM SC
        -> WHERE CId=(SELECT CID FROM Course WHERE TId=(SELECT TId FROM Teacher WHERE Tname='张三'))) AS A
        -> ORDER BY A.score DESC LIMIT 1;
    +------+-------+
    | SId  | score |
    +------+-------+
    | 01   |  90.0 |
    +------+-------+
    1 row in set (0.00 sec)
    ```

    

34. **成绩有重复的情况下，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩**

    ```
    ###成绩重复：首先找出「张三」老师所授课程的成绩表A,选取成绩=最高分B.MAXscore的学生记录
    mysql> SELECT A.SId, A.score FROM 
        -> (SELECT * FROM SC
        -> WHERE CId=(SELECT CID FROM Course WHERE TId=(SELECT TId FROM Teacher WHERE
        -> Tname='张三'))) AS A,
        -> (SELECT MAX(score) AS MAXscore FROM SC
        -> WHERE CId=(SELECT CID FROM Course WHERE TId=(SELECT TId FROM Teacher WHERE
        -> Tname='张三'))) AS B
        -> WHERE A.score=B.MAXscore;
    +------+-------+
    | SId  | score |
    +------+-------+
    | 01   |  90.0 |
    +------+-------+
    1 row in set (0.01 sec)
    ```

    

35. **查询不同课程成绩相同的学生的学生编号、课程编号、学生成绩**

    ```
    ###REFERENCE
    mysql> SELECT C.SId, MAX(C.CId) AS CId, MAX(C.score) AS score FROM SC AS C          
    		-> LEFT JOIN (SELECT SId, AVG(score) AS score FROM SC GROUP BY SId) AS B
        -> ON C.SId=B.SId
        -> WHERE C.score=B.score
        -> GROUP BY C.SId
        -> HAVING COUNT(0)=(SELECT COUNT(0) FROM SC WHERE SId=C.SId);
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 03   | 03   |  80.0 |
    +------+------+-------+
    1 row in set (0.01 sec)
    ```

    参考答案的解题思路：一个学生的各科成绩一样 <=> 最高成绩C表与平均成绩B表一样。

    如何理解having后面的条件呢？

    - 首先我有总的成绩表C，和一个平均成绩表B。
    - 根据B中的SId，和 平均成绩成绩去匹配C中的信息（这个时候，单科成绩=平均成绩的信息也会被选择出来，如学号为'02'的同学成绩：70，60，80；平均成绩：70），这个时候（02+70这条记录也会被选出来）
    - 最后要求某一个SId选出来的成绩记录条数=总成绩表SC中该SId的成绩记录条数（having后面的条件）

    **认真品读，WHERE、ON、GROUP BY、HAVING的位置。**

36. **查询每门课程中成绩最好的前两名**

    ```
    mysql> (SELECT * FROM SC WHERE CId='01' ORDER BY score DESC LIMIT 2)
        -> UNION ALL
        -> (SELECT * FROM SC WHERE CId='02' ORDER BY score DESC LIMIT 2)
        -> UNION ALL
        -> (SELECT * FROM SC WHERE CId='03' ORDER BY score DESC LIMIT 2)
        -> ;
    +------+------+-------+
    | SId  | CId  | score |
    +------+------+-------+
    | 01   | 01   |  80.0 |
    | 03   | 01   |  80.0 |
    | 01   | 02   |  90.0 |
    | 07   | 02   |  89.0 |
    | 01   | 03   |  99.0 |
    | 07   | 03   |  98.0 |
    +------+------+-------+
    6 rows in set (0.00 sec)
    ```

    

37. **统计每门课程的学生选修人数（超过 5 人的课程才统计）。**

    ```
    mysql> SELECT CId, COUNT(CId) AS 人数 FROM SC
        -> GROUP BY CId
        -> HAVING 人数>5;
    +------+--------+
    | CId  | 人数   |
    +------+--------+
    | 01   |      6 |
    | 02   |      6 |
    | 03   |      6 |
    +------+--------+
    3 rows in set (0.01 sec)
    ```

    

38. **检索至少选修两门课程的学生学号 **

    ```
    mysql> SELECT SId FROM SC
        -> GROUP BY SId
        -> HAVING COUNT(CID)>=2;
    +------+
    | SId  |
    +------+
    | 01   |
    | 02   |
    | 03   |
    | 04   |
    | 05   |
    | 06   |
    | 07   |
    +------+
    7 rows in set (0.00 sec)
    ```

    

39. **查询选修了全部课程的学生信息**

    ```
    mysql> SELECT * FROM Student
        -> WHERE SId IN
        -> (SELECT SC.SId FROM SC
        -> GROUP BY SC.SId
        -> HAVING COUNT(CId)=(SELECT COUNT(*) FROM Course));
    +------+--------+---------------------+------+
    | SId  | Sname  | Sage                | Ssex |
    +------+--------+---------------------+------+
    | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
    | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
    | 04   | 李云   | 1990-08-06 00:00:00 | 男   |
    +------+--------+---------------------+------+
    4 rows in set (0.01 sec)
    ```

    

40. **查询各学生的年龄，只按年份来算 **

    ```
    mysql> SELECT Student.*, (YEAR(NOW())-YEAR(Student.Sage)) AS 年龄
        -> FROM Student;
    +------+--------+---------------------+------+--------+
    | SId  | Sname  | Sage                | Ssex | 年龄   |
    +------+--------+---------------------+------+--------+
    | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |     30 |
    | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |     30 |
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |     30 |
    | 04   | 李云   | 1990-08-06 00:00:00 | 男   |     30 |
    | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |     29 |
    | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |     28 |
    | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |     31 |
    | 09   | 张三   | 2017-12-20 00:00:00 | 女   |      3 |
    | 10   | 李四   | 2017-12-25 00:00:00 | 女   |      3 |
    | 11   | 李四   | 2017-12-30 00:00:00 | 女   |      3 |
    | 12   | 赵六   | 2017-01-01 00:00:00 | 女   |      3 |
    | 13   | 孙七   | 2018-01-01 00:00:00 | 女   |      2 |
    +------+--------+---------------------+------+--------+
    12 rows in set (0.00 sec)
    ```

    

41. **按照出生日期来算，当前月日 < 出生年月的月日则，年龄减一。TIMESTAMPDIFF方法**

    ```
    mysql> SELECT Student.*, TIMESTAMPDIFF(YEAR, Sage, NOW()) as 年龄
        -> FROM Student;
    +------+--------+---------------------+------+--------+
    | SId  | Sname  | Sage                | Ssex | 年龄   |
    +------+--------+---------------------+------+--------+
    | 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |     30 |
    | 02   | 钱电   | 1990-12-21 00:00:00 | 男   |     29 |
    | 03   | 孙风   | 1990-05-20 00:00:00 | 男   |     30 |
    | 04   | 李云   | 1990-08-06 00:00:00 | 男   |     30 |
    | 05   | 周梅   | 1991-12-01 00:00:00 | 女   |     28 |
    | 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |     28 |
    | 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |     31 |
    | 09   | 张三   | 2017-12-20 00:00:00 | 女   |      2 |
    | 10   | 李四   | 2017-12-25 00:00:00 | 女   |      2 |
    | 11   | 李四   | 2017-12-30 00:00:00 | 女   |      2 |
    | 12   | 赵六   | 2017-01-01 00:00:00 | 女   |      3 |
    | 13   | 孙七   | 2018-01-01 00:00:00 | 女   |      2 |
    +------+--------+---------------------+------+--------+
    12 rows in set (0.00 sec)
    ```

    

42. **查询本周过生日的学生**

    ```
    ###第一步选出学生的生日：月份+号数
    mysql> SELECT SId, Sname, MONTH(Sage) as month, DAY(Sage) as day FROM Student;
    +------+--------+-------+------+
    | SId  | Sname  | month | day  |
    +------+--------+-------+------+
    | 01   | 赵雷   |     1 |    1 |
    | 02   | 钱电   |    12 |   21 |
    | 03   | 孙风   |     5 |   20 |
    | 04   | 李云   |     8 |    6 |
    | 05   | 周梅   |    12 |    1 |
    | 06   | 吴兰   |     3 |    1 |
    | 07   | 郑竹   |     7 |    1 |
    | 09   | 张三   |    12 |   20 |
    | 10   | 李四   |    12 |   25 |
    | 11   | 李四   |    12 |   30 |
    | 12   | 赵六   |     1 |    1 |
    | 13   | 孙七   |     1 |    1 |
    +------+--------+-------+------+
    12 rows in set (0.00 sec)
    
    ###当前月份
    mysql> SELECT MONTH(NOW()) AS 当前月份;
    +--------------+
    | 当前月份     |
    +--------------+
    |            9 |
    +--------------+
    1 row in set (0.00 sec)
    
    ###本周周一和周末号数
    mysql> SELECT DAY(DATE_SUB(NOW(), INTERVAL WEEKDAY(NOW()) DAY)) AS 本周周一;
    +--------------+
    | 本周周一     |
    +--------------+
    |            7 |
    +--------------+
    1 row in set (0.00 sec)
    
    mysql> SELECT DAY(DATE_ADD(NOW(), INTERVAL (6-WEEKDAY(NOW())) DAY)) AS 本周周日; 
    +--------------+
    | 本周周日     |
    +--------------+
    |           13 |
    +--------------+
    1 row in set (0.00 sec)
    
    ###本周过生日的学生：月份=本月 AND 本周一号数<=学生生日号数<=下周日号数
    mysql> SELECT A.* FROM
        -> (SELECT SId, Sname, MONTH(Sage) as month, DAY(Sage) as day FROM Student) AS A
        -> WHERE A.month = (SELECT MONTH(NOW()))
        -> AND (DAY(DATE_SUB(NOW(), INTERVAL WEEKDAY(NOW()) DAY))) <= A.day <=
        -> (DAY(DATE_ADD(NOW(), INTERVAL (6-WEEKDAY(NOW())) DAY)))
        -> ;
    Empty set (0.01 sec)
    ```

    

43. **查询下周过生日的学生**

    ```
    ##下周一号数
    mysql> SELECT DAY(DATE_ADD(DATE_SUB(NOW(), INTERVAL WEEKDAY(NOW()) DAY), INTERVAL 1 WEEK)) AS A;
    +------+
    | A    |
    +------+
    |   14 |
    +------+
    1 row in set (0.00 sec)
    
    ##下周日号数
    mysql> SELECT DAY(DATE_ADD(DATE_ADD(NOW(), INTERVAL (6-WEEKDAY(NOW())) DAY), INTERVAL 1 WEEK)) AS B;
    +------+
    | B    |
    +------+
    |   20 |
    +------+
    1 row in set (0.00 sec)
    
    ###下周过生日的学生：月份=本月 AND 下周一号数<=学生生日号数<=下周日号数
    mysql> SELECT A.* FROM
        -> (SELECT SId, Sname, MONTH(Sage) as month, DAY(Sage) as day FROM Student) AS A
        -> WHERE A.month = (SELECT MONTH(NOW()))
        -> AND (DAY(DATE_ADD(DATE_SUB(NOW(), INTERVAL WEEKDAY(NOW()) DAY), INTERVAL 1 WEEK))) <= A.day <=
        -> (DAY(DATE_ADD(DATE_ADD(NOW(), INTERVAL (6-WEEKDAY(NOW())) DAY), INTERVAL 1 WEEK)))
        -> ;
    Empty set (0.00 sec)
    ```

    

44. **查询本月过生日的学生**

    ```
    ##本月，月份查询
    SELECT MONTH(NOW());
    
    ##本月过生日学生：月份=本月
    mysql> SELECT A.* FROM
        -> (SELECT SId, Sname, MONTH(Sage) as month, DAY(Sage) as day FROM Student) AS A
        -> WHERE A.month = MONTH(NOW());
    Empty set (0.00 sec)
    ```

    

45. **查询下月过生日的学生**

    ```
    ##下个月，月份查询
    SELECT MONTH(NOW())+1;
    
    ##下个月过生日学生：月份=下个月
    mysql> SELECT A.* FROM
        -> (SELECT SId, Sname, MONTH(Sage) as month, DAY(Sage) as day FROM Student) AS A
        -> WHERE A.month = (MONTH(NOW()) + 1);
    Empty set (0.00 sec)
    
    ```

### 参考

- [超经典SQL练习题，做完这些你的ＳＱＬ就过关了](https://blog.csdn.net/flycat296/article/details/63681089?spm=a2c4e.10696291.0.0.630e19a4acZJf7)
- [Mysql练习题-50](https://www.jianshu.com/p/2d1276d056b8)
- [MySQL经典练习题及答案，常用SQL语句练习50题](https://blog.csdn.net/qq_41936662/article/details/80393172)
- 15题，16题参考：[MYSQL实现排名函数RANK，DENSE_RANK和ROW_NUMBER](https://blog.csdn.net/u011726005/article/details/94592866)
- 