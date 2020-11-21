
### MySQL中concat函数

1. **CONCAT(str1, str2, ...)**

   返回结果为连接str1，str2，···，等参数 产生的字符串。

   注：

   - 参数可以为1个或多个
   - 如果任何一个参数为NULL，则返回值为NULL。
   - 如果所有参数均为非二进制字符串，则结果为非二进制字符串
   - 如果含有任一一个二进制字符串，则结果为一个二进制字符串。

2. **CONCAT_WS(separator, str1, str2, ...)**

   - CONCAT_WS 表示 CONCAT WITH  SEPARATOR，是CONCAT()的特殊形式。
   - 第一个参数是其他参数的分隔符，分隔符可以是一个字符串，也可以是其他参数。

3. **group_concat([DISTINCT] 要连接的字段 [ORDER BY ASC/DESC 排序字段] [Separator '分隔符'])**

   

4. **REPEAT()函数**

   用来复制字符串

### 参考

[详解MySQL中concat函数的用法（连接字符串）](https://www.jb51.net/article/100886.htm)