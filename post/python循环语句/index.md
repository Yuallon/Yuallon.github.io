
### while循环语句

**while循环基本语法**

```
while 判断语句(condition):
  	执行语句(statements)
```

跟判断语句 **if** 对比来看，**wile** 也是首先执行紧跟其后面的判断语句，如果判断语句返回的 **bool值** 为**True** 则会运行里面的执行语句，然后回到 **while语句** 再次重新判断后面的bool返回值是否为True，如果仍为True会再次运行里面的执行语句，直到 **while语句**后面的判断语句返回值为 **False** 时，终止while循环语句。

**注意⚠️：while循环里面一定要有控制循环的次数变量，如果没有：要么不执行循环，要么一直执行wile循环。**

**实例1:打印出10以内的自然数**

```
i = 1 #控制循环次数的变量
while i <= 10:
  	print(i,end='')
  	i += 1
#output
12345678910
```



### 循环嵌套

python语言是允许语句之间的嵌套。比如：if 语句可以包含另一个 if 语句。同样，while 语句也可以包含另一个 while 语句。此外，if 语句、for语句、while语句也可以互相嵌套。

**实例2:打印出9*9算法表**

```
num = 1
while num <= 9:
  	i = 1
  	while i <= num:
   		 	value = i * num
    		print("%d*%d=%d" %(i, num, value), end='\t')
        i += 1
    print()
    num += 1
#output
1*1=1	
1*2=2	2*2=4	
1*3=3	2*3=6	3*3=9	
1*4=4	2*4=8	3*4=12	4*4=16	
1*5=5	2*5=10	3*5=15	4*5=20	5*5=25	
1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36	
1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49	
1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64	
1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81	
```



### for循环语句

python中的for循环语句，用来 **遍历** 任何序列中的元素，比如一个列表or一个字符串等。

**for基本语法：**

```
for item in sequence:
  	执行语句（statements）
```

**for-else语句**

```
a = '12345678'
for i in a:
    if i == '4':
        print("找到了不吉利数字：%s" %i)
else:
    print("没有找到目标")

#output
找到了不吉利数字：4
没有找到目标
```

**else语句** 的作用当遍历完整个序列的时候，没有 **被终止** 的时候会执行else语句。

一般会使用：**if-break-else结构**

```
a = '12345678'
for i in a:
    if i == '4':
        print("找到了不吉利数字：%s" %i)
        break
else:
    print("没有找到目标")
    
#output
找到了不吉利数字：4
```



### break语句

python中的break语句是用来 **终止循环语句**，即使循环过程没有全部结束，或者序列没有完全递归完，只要break前的判断语句返回True值，就立刻终止循环过程。一般都是和 **if语句** 一起使用。

用在 while循环 和 if循环 中。

**实例3:**

```
for letter in 'python':
  	if letter == 't':
   		 	break
		print("当前字母是：%s" % letter)
#output,当遇到字母t的时候，if语句返回的值是True，break终止整个循环。
当前字母是：p
当前字母是：y
```



###continue语句

python中的continue语句，与前面的break语句不同，**continue语句是跳出本次循环，而break是跳出整个循环**。

**实例4:**

```
for letter in 'python':
  	if letter == 't':
   		 	continue
		print(letter)

#output,当遇到字母t的时候，if语句返回的值是True，continue跳过本次循环，而继续。
p	y	h	o	n
```



### pass语句

python中的pass语句是一个空语句，是为了 **保持程序结构的完整性**。pass语句不做任何事情，一般用于占位。

**实例5:**

```
for letter in 'python':
  	if letter == 't':
   		 	pass
      	print("pass占位")
		print(letter)

#output
p
y
pass占位
t
h
o
n
```

### 实例6:给出100以内的质数

```
i = 2
while(i < 100):
    j = 2
    while(j <= (i/j)):
        if not(i%j): break
        j = j + 1
    if (j > i/j) : print("%d是质数" %i)
    i = i + 1
print("end")
```





