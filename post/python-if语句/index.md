
### python条件语句

**语法格式：**

```
#if语句
if 判断条件1:
  	执行语句1
elif 判断条件2:
  	执行语句2
else:
 		执行语句3  
```

注：其中 **elif** 语句可以有多个，对于 **if** 和 **elif** 中的判断条件，运行第一个给出True值后面的执行语句，且运行后不再判断后面 **elif**语句。如果最后一个 **elif** 语句返回的仍是False，则执行 **else** 中的语句。

**语法解读：**

python中的 if 条件语句 通过依次执行语句中的判断条件，如果判断结果返回的是True，则运行紧跟后面的执行语句。如果判断条件1返回的值是True，则不会再运行后面 elif，else语句。如果判断条件都为False，则会执行else中的语句。

if 语句可以嵌套！

**实例1: 找出100以内的质数！**

质数：在大于1的自然数中，除了1和它本身以外不再有其他因数的自然数。

```
value = int(input("请输入查找的范围："))
for number in range(value+1):
#    number = int(input("请输入查找的范围："))
    if number >=2:
        n = 0
        for i in range(number):
            i += 1
            if (number % i) == 0:
                n += 1
        if n == 2:
            print(number, end = '\t')
        #else:
            #print("不是质数")
#else:
  #print("查找失败，请检查输入的数字")
  
```



