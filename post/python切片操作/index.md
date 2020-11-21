
### 字符串（string）

在python中，我们可以通过在单引号（single quotes '...'）或 双引号（double quotes "..."）来定义一个字符串。在字符串中，如果想保留单引号或者双引号，可以使用转义符 **\\**（backslash）。

```
str1 = 'abcd'
str2 = "nihao"
str3 = 'It\'s ok!'
```



#### 字符串索引（string index）

![字符串索引](/字符串索引.jpg)

Figure1：字符串索引

- 从最左端开始，字符串索引是从0开始，往右依次递增。
- 如果从最右端开始，字符串索引是从 **-1** 开始，往左依次递减。（因为在python中，-0与0是等价的，所以从-1开始）



**切片操作（slice operation）**

**格式：string[start:end]**

在字符串后面加上中括号（bracket）并给出起始位置，就可以获取字符串string对应下标范围内的子字符串。**注意：[start : end]给出的是一个左闭右开区间**。

```
str1 = 'abcde'
str1[1:3]
#output
'bc'
```

当我们对字符串切片操作时，默认的步长是1。如果想修改默认步长，可以这样 **string[start : end: steps]**。

```
str2 = 'abcdefg'
str2[0:5:2]
#output
'ace'
```

同样，我们也可以使用index值为负数。

```
str3 = 'aabbccdd'
str3[-4:-2]
#output
'cc'
##反向步长
str3[-2:-6:-2]
#output
'dc'
```



**关于string[start : end: steps]，有点绕的解释：（能理解就行，不理解不强求）**

1. step值的的正负，表示我们是从那个端点开始计数，正数：最左端；负数：最右端
2. step值的大小，表示我们的步长是多少
3. 如果采用step为正数值，则 start值>end值。否则，返回空值。
4. 如果采用step为负数值，则 start值<end值。否则，返回空值。
5. 关于3，4的解释：离起始端点远的index值，的绝对值一定大于，离起始端点近的index值。
6. 如果，start值或end值超出字符串本身长度，返回空值。



#### 与字符串一些相关的函数

- str.find(sub, start, end)：返回子字符串 **sub** 在字符串切片 **str[start : end]** 中最小的index值，如果没有找到，返回 **-1**。

  ```
  str4 = 'nihaonihao'
  str4.find('ao')
  3
  ```

  注：find函数用于你想知道子字符串在字符串中的确切位置。如果是为了检查字符串中是否含有子字符串，可以使用 in 操作符。

  ```
  'py' in 'python'
  True
  ```

- str.index(sub, start, end)：与find函数类似，唯一的区别是：找不到会报错（raise ValueError）。

- str.replace(old, new, counts)：在字符串中用new的字符串替换掉old字符串，counts表示替换的次数

- str.count(sub, start, end)：计算子字符串在字符串切片中出现的次数（未重合的部分。）

  ```
  str5 = 'nihaoaaabbb'
  str5.count('a')
  4
  str5.count('a', 4, 7)
  2
  str5.count('aa')
  1
  ```

- str.split(sep=None, maxsplit=-1)：以sep参数方式方式对字符串进行分隔，默认不分隔。maxsplit后面跟的数值表示分隔的次数。默认是全部分隔。

  ```
  str6 = '1,2,3'
  str6.split(',')
  ['1', '2', '3']
  str6.split(',',maxsplit=1)
  ['1', '2,3']
  ```

- 其他对字符串的操作详见：[String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)



###列表（list）

列表是python中最常用的数据类型，直接在方括号（square brackets []）中添加元素即可。添加的元素类型可以是任何一种python允许的类型。

```
list1 = [1, 7.7, 'Hello World', Ture, [6,6,6]]
```

- list.append()：在列表的末尾，添加新的对象

  ```
  list1 = [1, 7.7, 'Hello World', True, [6,6,6]]
  list1.append("中国你好！")
  list1
  [1, 7.7, 'Hello World', True, [6, 6, 6], '中国你好！']
  ```

  

- list.extend()：并合两个list数据

  ```
  list1 = [1, 7.7, 'Hello World', True, [6,6,6]]
  list2 = [0, 'aa']
  list1.extend(list2)
  list1
  [1, 7.7, 'Hello World', True, [6, 6, 6], 0, 'aa']
  ```

- list.index()：根据索引值，添加对象

  ```
  list1 = [1, 7.7, 'Hello World', True, [6,6,6]]
  list1.insert(0, 'aa')
  list1
  ['aa', 1, 7.7, 'Hello World', True, [6, 6, 6]]
  ```

  

- list.remove()：移除列表中某个值的第一个匹配项

  ```
  list1 = [1, 7.7, 'Hello World', True, [6,6,6]]
  list1.remove(7.7)
  list1
  [1, 'Hello World', True, [6, 6, 6]]
  ```

  

- list.pop()：移除列表中的一个元素（默认最后一个），并且返回该元素的值。

  ```
  list1 = [1, 7.7, 'Hello World', True, [6,6,6]]
  list1.pop()
  [6, 6, 6]
  list1
  [1, 7.7, 'Hello World', True]
  ```

- list.reverse()：用于反向列表中的元素

  ```
  list1 = ['physics', 'Biology', 'chemistry', 'maths']
  list1.reverse()
  print ("list now : ", list1)
  list now :  ['maths', 'chemistry', 'Biology', 'physics']
  ```

- list.sort(cmp=None, key=None, reverse=False)：用于对列表中的元素进行排序。

  - cpm：可选参数，按照指定的参数方法进行排序

  - key：主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。

  - reverse：排序规则，**reverse = True** 降序， **reverse = False** 升序（默认）。

    ```
    a = [3,1,6,8,4,9]
    a.sort(reverse=True)
    print(a)
    [9, 8, 6, 4, 3, 1]
    ```

### 第4次作业情况

1. str.strip()函数可以去除首尾的空白
2. str.lower()函数可以把字符串中有大写字母的单词，都变成小写字母
3. str.title()函数可以把字符串中的每个单词首字母大写
4. str.startswith('s')函数判断某个字符串是否以s字母开始
5. str.endswith('e')函数判断字符串是否以e字母结尾
6. 对于作业第五题，我自己想的有些复杂化，一直纠结于字符串是不能更改的数据类型，想每次操作后都赋值一个新名字，其实每次依旧采取，words名字就行，只是虽然名字一样，但是物理地址不一样。

###Reference

- [An Informal Introduction to Python](https://docs.python.org/3/tutorial/introduction.html#strings)
- [w3schools.com](https://www.w3schools.com/python/ref_string_find.asp)

