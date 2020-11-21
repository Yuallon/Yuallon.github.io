
- 查看数据库编码格式

  ```
  show create database <数据库名字>;
  ```

- 查看数据表编码格式

  ```
  show create table <数据表名字>;
  ```

- 创建数据库时指定数据库的编码格式

  ```
  create  database  <数据库名>  character  set  utf8;
  ```

- 创建数据表时指定数据表的编码格式

  ```
  create table tb_books(
      name  varchar(45) not  null,
      price  double  not  null,
      bookCount  int  not  null,
      author  varchar(45)  not  null) 
      default  charset = utf8;
  ```

- 修改数据库的编码格式

  ```
  alter  database  <数据库> character  set  utf8;
  ```

- 修改数据表的编码格式

  ```
  alter  table  <表名> character  set  utf8;
  ```

- 修改字段编码格式

  ```
  alter  table <表名>  change  <字段名>  <字段名>  <类型>  charset  set  utf8;
  alter table tb_books change name name varchar(20) character  set  utf8 not null;
  ```

  

### 参考

[查看mysql数据库及编码方式](https://www.jianshu.com/p/57ebcb855e0c)