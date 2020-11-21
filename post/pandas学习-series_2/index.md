
上一篇文章讲述了pandas.Series()函数，主要讲述函数的input和output的数据类型。既然在默认输出情况下，output的类型跟input类型保持一致。则一个很自然的想法就是：python对input数据的相关operation同样也适用于output数据。如：对数组的slicing，对dict的添加元素和一些vectorized operations。以及其特有的**name attribute**。上面提到便是这此的学习记录。

###Series is ndarry-like

Series与数组结构很像，一些Numpy函数操作同样也适用于Series，比如slicing。当对Series数据做切片操作时，同时也对index做切片。

```
#input
import numpy as np
import pandas as pd
s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
#output
a    0.325586
b   -1.225338
c   -0.400249
d   -0.924700
e    1.622577
dtype: float64
######
s[0]
0.3255858143443221
######
s[:3]
a    0.325586
b   -1.225338
c   -0.400249
dtype: float64
######
s[s > s.median()]
a    0.325586
e    1.622577
dtype: float64
######
s[[4, 3, 1]]
e    1.622577
d   -0.924700
b   -1.225338
dtype: float64
######
np.exp(s)
a    1.384842
b    0.293658
c    0.670153
d    0.396650
e    5.066129
dtype: float64
```

像Numpy数组一样，Series也有**dtype**属性。

```
s.dtype
dtype('float64')
```

如果我们只想要一个pandas的数据数组，而不要index。可以使用**Series.array**。

```
s.array
<PandasArray>
[  0.3255858143443221,   -1.225338237628694, -0.40024888819126353,
  -0.9247004170525731,    1.622577070446212]
Length: 5, dtype: float64
######
s.array[0]
0.3255858143443221
```

如果想要获得Numpy数据数组，可以使用**Series.to_numpy()**。

```
s.to_numpy
array([ 0.32558581, -1.22533824, -0.40024889, -0.92470042,  1.62257707])
```

###Series is dict-like

Series也很像一个dict，通过index label可以索引对应的值or赋值。

```
#get
s['a']
0.3255858143443221
#set
s['f','e']=[5.0,7.0]
s
a      0.325586
b     -1.225338
c     -0.400249
d     -0.924700
e      7.000000
f      5.000000
dtype: float64
```

###Vectorized operations

跟Numpy array一样，Series也可以直接进行向量操作(加减乘除or函数)。唯一的区别是Series会自动关联到index label。

```
#
s
a    0.325586
b   -1.225338
c   -0.400249
d   -0.924700
e    7.000000
f    5.000000
dtype: float64
##plus
s + s
a     0.651172
b    -2.450676
c    -0.800498
d    -1.849401
e    14.000000
f    10.000000
dtype: float64
##times
s * 2
a     0.651172
b    -2.450676
c    -0.800498
d    -1.849401
e    14.000000
f    10.000000
dtype: float64
##function
np.exp(s)
a       1.384842
b       0.293658
c       0.670153
d       0.396650
e    1096.633158
f     148.413159
dtype: float64
```

如果两个Series做向量操作时，如果一个index label只在其中一个存在的话，则在向量操作后对应的标签结果会被标记为**NAN(miss value)**。

```
s[1:] + s[:-1]
a          NaN
b    -2.450676
c    -0.800498
d    -1.849401
e    14.000000
f          NaN
dtype: float64
```

###Name attribute

Series同时拥有**name**属性，当我们对DataFrame做1D slicing操作时，得到的Series会自动赋予name值，详情见DataFrame。

```
s = pd.Series(np.random.randn(5))
0    0.827283
1    0.644301
2    2.471672
3    1.610652
4    0.485569
dtype: float64
####add name attribute
s = pd.Series(np.random.randn(5), name='something')
0    0.042302
1   -0.876080
2    0.380833
3   -2.168175
4    0.048872
Name: something, dtype: float64
```

如果想改变Series的name属性，可以用**Series.rename()**

```
s1 = s.rename('one')
s1.name
'one'
```

