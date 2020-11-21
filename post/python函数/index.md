
###前言

在平时的工作中，我们会遇到很多需要重复的地方，比如统计一个班上所有同学的成绩。虽然我们可以通过循环实现，但是每次都去写一个循环结构显然是麻烦的。

函数，顾名思义与数学中的函数概念一样，比如：$y=kx+b$，只要我们知道 $x$ 值就可以根据方程式，求取 $y$ 值。在python中，$x$ 值就相当于某类工作的重复，通过定义函数就可以帮助我们更方便的去处理相同类型的数据要求。

在python中，函数是组织好的，可重复使用的，用来实现单一的、或相关联功能的代码。在python中有很多内置函数，如：print()，当然用户也可以根据处理问题的不同自定义自己的函数。



### 函数定义

- 函数代码块以 **def** 关键词开头，后接 **函数名** 和 **圆括号** 然后以 **:** 结束
- 任何传入的参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数
- 函数的第一行语句最好写一段注释语句，用于对函数的描述
- 可以用 **return[表达式]** 选择性地返回一个值。不带表达式的return相当于返回None。



**语法定义：**

```
def function(argument1, argument2, ...):
	function body
```

在python中，我们使用 **def** 来声明一个函数。后接函数的名字，圆括号内（parentheses）内的参数（argument）使用逗号（comma）分开，并以冒号结尾换行，然后是函数体，即函数实现的功能是什么。

**参数类型：**

1. 形参（parameter）：顾名思义，它只是形式上的参数，是指函数定义中圆括号内的参数列表。
2. 实参（argument）：就是当我们调用函数时，实际传给函数的参数。

一般情况下在函数调用中，传给函数的实参要与函数的形参一一对应。即有多少个形参，就传入多少个实参。

**参数分类：**

- 必须参数：必须以正确的顺序传入函数，调用时的数量必须和声明时一样。
  ![必须参数](/必须参数.jpg)

- 关键字参数：关键字参数与必须参数相比，调用时参数的顺序可变，因为python解释器能够用参数名匹配参数值。

- 默认参数：调用函数时，如果没有参数 传递，会使用默认参数。

  ```
  #可写函数说明
  def printinfo( name, age = 35 ):
     #"打印任何传入的字符串"
     print ("名字: ", name)
     print ("年龄: ", age)
     return
   
  #调用printinfo函数
  printinfo( age=50, name="runoob" )
  print ("------------------------")
  printinfo( name="runoob" )
  ```

  输出:

  ```
  名字:  runoob
  年龄:  50
  ------------------------
  名字:  runoob
  年龄:  35
  ```

  

- 不定长参数：是指我们传入函数的参数个数不确定。放在参数最后面

  - 加 ***arg** 的参数会以 **元组（tuple）** 的形式导入，存放所有未命名的变量参数。单值参数

    ```
    # 可写函数说明
    def printinfo( arg1, *vartuple ):
       #"打印任何传入的参数"
       print ("输出: ")
       print (arg1)
       for var in vartuple:
          print (var)
       return
     
    # 调用printinfo 函数
    printinfo( 10 )
    printinfo( 70, 60, 50 )
    ```

    输出:

    ```
    输出:
    10
    输出:
    70
    60
    50
    ```

    

  - 加 **\**kwarg** 的参数会以 **字典** 的形式导入。多值参数

    ```
    # 可写函数说明
    def printinfo( arg1, **vardict ):
       #"打印任何传入的参数"
       print ("输出: ")
       print (arg1)
       print (vardict)
     
    # 调用printinfo 函数
    printinfo(1, a=2,b=3)
    ```

    输出:

    ```
    输出: 
    1
    {'a': 2, 'b': 3}
    ```

    如果单独出现 ***** 号，后面的参数必须用关键字传入

    ```
    >>> def f(a,b,*,c):
    	     return a+b+c
    	 
    >>> f(1,2,3)   # 报错
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: f() takes 2 positional arguments but 3 were given
    >>> f(1,2,c=3) # 正常
    6
    ```

    

**参数传递：**

在python中，类型属于对象，变量时没有类型的。

```
a = [1,2,3]
a = 'Runnob'
```

[1,2,3]是List类型，'Runnob'是String类型，而变量a是没有类型，她仅仅是一个对象的引用（一个指针），可以指向List类型，也可以指向String类型。

- 不可更改（immutable）类型：在 python中，strings，tuples 和 numbers 是不可更改的对象。

  变量赋值 a=5 后再赋值 a=10，这里实际上是新生成一个int值对象10，再让a指向它，而5被丢弃，不是改变了a的值，相当于新生成了a。

- 可变（mutable）类型：除了不可变类型以外都是可变类型，如lists，dictionary等。


  变量 la=[1,2,3,4] 后再赋值 la[2]=5，则是第三个元素由3改为5，本身的la没有动，即指针的位置是没有改变的。

**提示：**python中调用函数时，参数的传递可以是可变类型，也可以是不变类型。当传入可变类型时，函数内部对该参数修改后，外部也会受影响。当传入不可变类型时，传递的只是a的值，没有影响a对象本身，在函数内修改a的值，只是修改了一个新的复制对象，外部的a不会受到影响。

```
#传入不可变类型
def ChangeInt( a ):
    a = 10
 
b = 2
ChangeInt(b)
print( b ) # 结果是 2

#传入可变类型

```

实例中有 int 对象 2，指向它的变量是 b，在传递给 ChangeInt 函数时，按传值的方式复制了变量 b，a 和 b 都指向了同一个 Int 对象，在 a=10 时，则新生成一个 int 值对象 10，并让 a 指向它。

```
#传入可变对象
# 可写函数说明
def changeme( mylist ):
   #"修改传入的列表"
   mylist.append([1,2,3,4])
   print ("函数内取值: ", mylist)
   return
 
# 调用changeme函数
mylist = [10,20,30]
changeme( mylist )
print ("函数外取值: ", mylist)
```

输出：

```
函数内取值:  [10, 20, 30, [1, 2, 3, 4]]
函数外取值:  [10, 20, 30, [1, 2, 3, 4]]
```



**局部变量和全局变量**

1. 局部变量：函数内部的变量都是局部变量。
2. 全局变量：函数外部的变量都是全局变量。

注：当有函数嵌套的时候，上述概念是相对的。比如，函数1包含了函数2，函数1内的变量相对函数2而言是全局的，函数2内部的变量相对函数1是局部的。

当函数一个变量名，同时在函数外部和函数内部，优先使用函数内部赋给的值（就近原则）。如果想在函数内部修改全局变量，需要用global对变量声明。



**return语句**

用return语句是让函数返回一个值。

1. 返回值是需要有变量去接受，如果没有返回值就没用了
2. 如果只是使用return没有具体的返回值，默认返回的是None
3. 如果函数中没有使用，默认返回的也是None
4. return语句代表了函数的结束，函数中return以下代码不会被执行



**pass语句**

根据函数的定义，函数体是不能为空的，但是因为某些原因，你准备使用某个函数名，但是还没有放入或写好函数体相关内容，可以通过使用pass语句来避免执行到此函数时出现报错。

```
def myfunction():
  pass
```



**函数的递归（recursion）**

在python中，支持函数的递归操作。就是定义的函数可以调用自身。

**递归：**是常见的数学方法和 程序概念。就是指函数本身可以调用自己。这样的好处是：你可以通过遍历数据来获得结果。

但是使用递归的时候一定要非常小心，因为很容易出现死循环。然而，如果使用正确，递归是一种非常有效且数学精巧的编程方法。

对于新手来讲，是需要时间来消化递归的概念。最好的方式就是测试某种递归方式，通过修改一些参数，来认知理解它。

```
#函数递归的使用，求取1->k的和
def tri_recursion(k):
  if(k > 0):
    result = k + tri_recursion(k - 1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6)
```

输出:

```

Recursion Example Results
1
3
6
10
15
21
```



在上述例子中，**tri_recursion()** 在 **if** 语句中调用了自身。**k** 做为数据变量，每次递归后 **-1**。递归结束语句是k值大于0。



**对于函数名的理解**

我们是否想过，当def一个函数后，为什么直接使用定义的函数名就可以进行函数相关操作呢？

```
def func():
	body

id(func)
```

在上面的表达式中，**函数名是存放函数代码所在的磁盘id**，**func()** 后+圆括号代表调用函数。可以使用 **id()** 函数查看函数存放的磁盘id。

因此，**函数也可以作为参数来使用**。

```
def func01(test):
	a = 10
	b = 20
	result = test(a,b)
	print(result)

def add_value(num1,num2):
	return num1 + num2


func01(add_value)
```



### 匿名函数lambda

与def一样，lambda表达式也是创建了一个之后可以调用的函数，但是它返回的是函数本身，而不是将其赋值给一个变量名。这也是lambda称为**匿名函数**的原因。

#### lambda表达式

```
lambda argument1, argument2, ... argumentN : expression using arguments
```

lambda的一般形式：关键字lambda后面跟上一个或多个参数（与一个def头部内用括号括起来的参数列表极其相似），之后是一个冒号，再之后是表达式。

1. **lambda是一个表达式，而不是语句**。因为这一点，lambda可以出现在Python语法不允许def出现的地方。例如在一个**列表字面量中**或者**函数调用参数中**。def语句总是要在其它地方创建，并头部将一个新的函数赋值给一个名称(变量variable)，lambda函数直接返回一个值(一个新的函数)，也可以选择性地被赋值给一个变量名。
2. **lambda的主体是一个单独的表达式，而不是一个代码块**。lambda的主体简单的就像def主体的return语句中的代码一样。由于lambda局限于一个表达式中，因此lambda通常要比def功能小。只能在lambda主体中封装有限的逻辑，**if语句**不能用目的是限制程序的嵌套。lambda是为了编写简单函数而设计的。

#### 为什么使用lambda？

通常来说，lambda起到一种函数速写作用，可以在使用它的代码中嵌套一个函数定义。此外，每次使用def代码，都需要占用临时性函数名称(可能同其他名称相冲突)，而想用的函数定义也会位于要使用的上下文外。

#### Example

1. lambda可以在列表字面量中工作，而def则不能。

   ```
   #lambda
   >>> L = [lambda x: x**2, lambda x: x**3, lambda x: x**4]
   >>> for f in L:
   	print(f(2))
   #def
   >>> def f1(x): return x**2
   >>> def f2(x): return x**3
   >>> def f3(x): return x**4
   
   >>> L = [f1, f2, f3]
   >>> for f in L:
   	print(f(2))
   ```

   

2. lambda可以在函数调用参数中使用。

   ```
   >>> sorted(range(-5, 6), key=lambda x: x ** 2)
   [0, -1, 1, -2, 2, -3, 3, -4, 4, -5, 5]
   
   >>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
   >>> sorted(students, key=lambda s: s[2])            # 按年龄排序
   [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
   ```





### Reference

- [w3schools.com](https://www.w3schools.com/)

- [RUNOOB.COM](https://www.runoob.com/)

- [Python sorted() 函数](https://www.runoob.com/python/python-func-sorted.html)

- [Lambda Function in Python: What are they good for?](https://dbader.org/blog/python-lambda-functions)

- Python学习手册第五版

  





