
###前言

前两天面试一家游戏公司，其中面试的第一题描述如下：

**题目**：给定二维坐标ABCD四个点，和点E，判断点E与四边形ABCD的位置关系。

### 解题思路

#### 题目分析：

根据题目的描述，是确定任意一点E与四边形ABCD的位置关系：在四边形内部 or 在四边形外部。

那这两种位置的本质区别是什么呢？对于给定的四边形ABCD，则其面积大小是一定的。对于凸四边形而言，如果点E在其内部与A，B，C，D四个点分别连线，可以将四边形分成四个三角形，四个三角形的面积之和等于四边形ABCD的面积，如果在外部则大于。可是对于凹四边形某些情况来说，这样判定就不正确了。

#### 解题思路：

既然根据四边形的面积大小直接判断有些情况不能很好区分，那么可以把四边形沿对角线分成两个三角形，对于三角形而言，就没有凸、凹一说了。可以根据面积来做判定。

- 如果点E在四边形ABCD内部，则其一定在两个三角形任意其一（如果点E在对角线上，则都在两个三角形上）。
- 如果点E在四边形ABCD外部，则一定不在两个三角形任意一个里面。

#### 代码实现：

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sat Oct 10 00:53:59 2020

@author: huangyulong
"""

import numpy as np



def tri_length(point_list):
    """
    根据三角形点的位置，给出三角形的边长
    """
    a, b, c = point_list 
    t1 = np.sqrt((a[0]-b[0])**2 + (a[1]-b[1])**2)
    t2 = np.sqrt((b[0]-c[0])**2 + (b[1]-c[1])**2)
    t3 = np.sqrt((a[0]-c[0])**2 + (a[1]-c[1])**2)
    return [t1, t2, t3]
    
    


def heron_formula(tri_list):
    """
    triangle_list: 三角形的三边长度list
    根据海伦公式给出三角形的面积
    """
    q = np.sum(tri_list)/2
    # return q
    q_list = [q-x for x in tri_list]
    # return q_list
    s = q
    for i in q_list:
        s *= i
    
    return np.sqrt(s) #此处的s值是三角形面积



def in_out(obj_list):
    """
    obj_list 包含4个点a, b, c, d 其中 a, b, c 是三角形的定点，d是待判断的点
    """
    a, b, c, d = obj_list
    
    s_abc = heron_formula(tri_length([a,b,c]))
    s_abd = heron_formula(tri_length([a,b,d]))
    s_acd = heron_formula(tri_length([a,c,d]))
    s_bcd = heron_formula(tri_length([b,c,d]))
    
    # print(s_abc)
    # print(s_abd + s_acd + s_bcd)
    # print(s_abd)
    # print(s_acd)
    # print(s_bcd)
    
    
    if round(s_abc, 3) == round((s_abd + s_acd + s_bcd), 3):
        return True
    else:
        return False
    
def quadrangle(qua_list):
    """
    que_list: 包含5个点a, b, c, d, e 其中a, b, c, d 是四边形的定点，e是待判断的点
    step1: 将四边形根据对角线划分成两个三角形
    step2: 如果点e在上述两个三角形任一内部，则点在四边形内部；否则点俄就在四边形外部
    """
    a, b, c, d, e = qua_list
    
    obj_list1 = [a, b, c, e]
    obj_list2 = [c, d, a, e]
    in_out1 = in_out(obj_list1)
    in_out2 = in_out(obj_list2)
    
    if in_out1 or in_out2:
        return True
    else:
        return False
    
    
if __name__ == '__main__':
    # qua_list = [[0,0], [0,1], [1,1], [1,0], [2,2]]
    # qua_list = [[0,0], [0,1], [1,1], [1,0], [0.5,0.5]]
    qua_list = [[0,0], [-1,-1], [0,1], [1,-1], [0,0.8]]
    result = quadrangle(qua_list)
    print(result)
```



