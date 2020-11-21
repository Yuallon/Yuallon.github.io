
### MySQL表格复制4中类别

1. **仅复制表结构**

   ```
   CREATE TABLE copy1 LIKE table1
   ;
   ```

   注：从LIKE关键字就可以明白，复制表结构。

2. **复制表结构+数据**

   ```
   CREATE TABLE copy2
   SELECT * FROM table2
   ;
   ```

   注：与1相比，这里使用了SELECT语句，说明是把table2中的数据复制到copy2中。

3. **复制部分数据**

   ```
   CREATE TABLE copy3 
   SELECT id, name
   FROM table3
   WHERE id = '01'
   ;
   ```

   注：WHERE作为复制部分数据条件语句。

4. **复制部分表结构**

   ```
   CREATE TABLE copy4
   SELECT id
   FROM table4
   WHERE 0 #或者 WHERE 1=2
   ;
   ```

   注：无论是0还是1=2，它们都表示FALSE，所以没有满足条件的数据，都是空值。也就是仅仅复制了id这个列名。