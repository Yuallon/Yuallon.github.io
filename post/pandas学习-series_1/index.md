
###Intro to pandas

在平时的工作中，经常会遇到很多表格类型的数据(如：txt, csv, excel, sql, json, parquet, ...)。**Pandas**的出现正是为了专门处理这些类型数据。在Pandas中，**Series**和**DataFrame**是数据最基本的表现形式。其中Series是一维的、有索引的、支持任何类型的数据结构(整数，字符串，浮点数，python对象等等)，DataFrame是二维的数据结构。

**Pandas**通过对Series和DataFrame的操作，可以实现对数据进行切片，提取特定的行列信息，过滤，并合，拆分等从而更便于对数据统计分析。Pandas通过**Matplotlib**模块可以方便对数据进行绘图，此外Pandas还支持对时间序列数据的处理。总而言之，平时工作中遇到的任何数据格式都可以通过Pandas做数据分析。

**Reference:** [pandas: powerful Python data analysis toolkit](https://pandas.pydata.org/docs/pandas.pdf)

###pandas.Series

回想起自己刚开始学习编程语言时，很多教程都是让我们跟着他们机械的敲一些代码：

```
print ("Hello World!")
```

说实话，这种类型的教程前期给我的学习带来了很大困扰，因为我是一个很喜欢刨根问底的人，虽然我也能跟着在Terminal打印出“Hello World!”这句话，但是如果没能搞明白这段代码的原理，会影响自己后续的学习动力。

其实，搞懂前面的问题也就一句话的事情。在编程语言的学习中，**只要把每一个代码看成一个函数结构，每个函数结构又有一定的参数设置**，这样我就会很好理解print这个函数了。而且有了这个概念在脑中时，以后凡事遇见一个命令时，我都会想考虑其中有那些函数？这个函数又有那些参数？

因此在总结Pandas学习中，我希望自己能延续这个习惯(学习任何一个模块都应该这样吧)。首先从pandas.Series的参数结构开始说起，当然一开始只会总结一些主要的参数。

```
pandas.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)
```

在上面的语法结构中，**=**号后面表示默认的设置(data=None，默认没有数据，言外之意没有任何输入直接执行pandas.Series()是没有输出的)。

**主要参数：**

1. data: 可以是数组类型，可迭代结构，字典，或者常数
2. index: 数组类型or指针
   index必须跟data有相同的长度，但是不要求每个index值是唯一的。如果没有给定，默认是(0, 1, 2, ..., len(data)-1)。对于字典，在把dict转成Series过程中，如果给定index则会优先于dict的关键字，如果没有输入index默认把dict的key生成index。
3. dtype: 如果没有要求生成的Series的数据类型，默认的数据类型来自于输入的数据类型

**Reference:** [pandas.Series](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html)

#### 例子

```
#Customarily, we import as follows:
import numpy as np
import pandas as pd
s = pd.Series([1,3,5,np.nan,6,8])
#out
0 1.0
1 3.0
2 5.0
3 NaN
4 6.0
5 8.0 dtype: float64

##from ndarry
s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
#out
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
e    1.212112
dtype: float64

#index
s.index
#out
Index(['a', 'b', 'c', 'd', 'e'], dtype='object')

#默认index
pd.Series(np.random.randn(5))

0   -0.173215
1    0.119209
2   -1.044236
3   -0.861849
4   -2.104569
dtype: float64

##from dict
d = {'b': 1, 'a': 0, 'c': 2}
pd.Series(d)
b    1
a    0
c    2
dtype: int64

pd.Series(d, index=['b', 'c', 'd', 'a'])
b    1.0
c    2.0
d    NaN
a    0.0
dtype: float64

##from scalar value
pd.Series(5., index=['a', 'b', 'c', 'd', 'e'])
a    5.0
b    5.0
c    5.0
d    5.0
e    5.0
dtype: float64



```

###Reference:

1.  [Intro to data structures](https://pandas.pydata.org/pandas-docs/stable/getting_started/dsintro.html#intro-to-data-structures)
2.  [10 minutes to pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html)



