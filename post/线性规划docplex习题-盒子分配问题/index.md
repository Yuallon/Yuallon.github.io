
英文文档的标题是 **Objects in boxes**，为了翻译方便我将采用   **盒子分配** 并且将 **object --> 小球**。

### 盒子分配

我们采用 IBM Decision Optimization CPLEX（DOCPLEX）python模块来解决此类线性规划问题。

#### 问题描述

- 我们希望将平面上有散落 N个小球 放入到 N个成列的盒子中。
- 盒子从左往右一次排列，序号依次递增（1号盒子在2号盒子左边）。
- 用 $B_i$ 表示第 $i$ 个盒子，$O_j$ 表示 第 $j$ 个小球。
- 我们想找到一组小球排列满足：
  - 每一个盒子只能容纳一个小球
  - 每一个小球只能被放到一个盒子里面
  - 盒子与小球之间的距离总和是最小
- 此外，当我们解决上述问题后，新增下面两个约束条件时，又该如何解决？
  - 在第一问题基础上，我们要求小球1所在的盒子必须挨着小球2所在盒子且在左边。
  - 要求小球5所在的盒子在小球6所在盒子旁边。

####如何做决策优化（decision optimization）

- 规范分析（决策优化）是基于预期结果来进行。它需要考虑 具体方案、资源、过去和目前的情况。将这些考虑进去，你会做出更好的决策，并且能更好的控制预期结果。
- 规范分析是迈向 *基于洞察力行动* 的下一步。它通过与预测分析一起来创造价值，该预测分析根据分析数据以预测未来的结果。
- 规范分析通过最优方法来洞察下一步结果，并处理未来情况。机构可以在动态条件下快速行动并在不确定环境下做出卓越的决策以获得强大的竞争优势。
- 使 **复杂决策和权衡** 更自动化来更好的管理你有限的资源。
- 抓住未来机遇、减少未来风险。
- 根据情况的改变提前更新建议。
- 满足经营目标、提高消费者忠诚度、防止威胁和欺诈和 优化商业过程。

#### 决策优化

##### 第一步：导入DOCLPEX模块

运行下面代码来导入 DOCPLEX 模块。DOCPLEX 模块包含 MP（Mathematical Programming）和 CP（Constrain Programming）两种模型。

```
import sys
try:
    import docplex.mp
except:
    raise Exception('Please install docplex. See https://pypi.org/project/docplex/')
```

如果 CPLEX 没有安装，请安装 CPLEX 社区版。

```
try:
    import cplex
except:
    raise Exception('Please install CPLEX. See https://pypi.org/project/cplex/')
```

##### 第二步：导入数据

导入数据包括：盒子与小球在(x,y)平面上的坐标及其数量N。

##### 第三步：数据准备

我们采用欧式距离来计算小球与盒子之间的距离。

```
from math import sqrt

N = 15
box_range = range(1, N+1)
obj_range = range(1, N+1)

import random

o_xmax = N*10
o_ymax = 2*N
box_coords = {b: (10*b, 1) for b in box_range}

obj_coords= {1: (140, 6), 2: (146, 8), 3: (132, 14), 4: (53, 28), 
             5: (146, 4), 6: (137, 13), 7: (95, 12), 8: (68, 9), 9: (102, 18), 
             10: (116, 8), 11: (19, 29), 12: (89, 15), 13: (141, 4), 14: (29, 4), 15: (4, 28)}

# the distance matrix from box i to object j
# 盒子i和小球j之间的距离矩阵
# actually we compute the square of distance to keep integer
# 实际上我们计算距离的平方值（为了取整数值）
# this does not change the essence of the problem
# 这并没有改变问题的本质
distances = {}
for o in obj_range:
    for b in box_range:
        dx = obj_coords[o][0]-box_coords[b][0]
        dy = obj_coords[o][1]-box_coords[b][1]
        d2 = dx*dx + dy*dy
        distances[b, o] = d2
```

##### 第四步：构建规范模型

```
from docplex.mp.environment import Environment
env = Environment()
env.print_information()
```

**创建 DOcplex 模型**

模型包含所有约束和定义目标函数。

```
from docplex.mp.model import Model

# 定义DOcplex模型的名称为 boxes
mdl = Model("boxes")
```

**定义决策变量**

- 对于每一个盒子$B_i$和小球$O_j$，定义一个二元变量 $X_{i, j}=1$ ，当且仅当小球$O_j$被放到盒子$B_i$中。

```
# decision variables is a 2d-matrix
# 决策变量是一个2D矩阵
x = mdl.binary_var_matrix(box_range, obj_range, lambda ij: "x_%d_%d" %(ij[0], ij[1]))
```

**约束表达式**

- 对于 $X_{i,j}$ 二元变量矩阵，每一行或每一列的和必须等于1（因为一个盒子只能放一个小球；同样一个小球也只能放在一个盒子里面）。因此会得到 $2 \times N$ 个约束（2在此处表示：行约束$N$个，列约束$N$个）。

```
# one object per box
# 一个小球只能放在一个盒子里面
mdl.add_constraints(mdl.sum(x[i,j] for j in obj_range) == 1
                   for i in box_range)
    
# one box for each object
# 一个盒子只能容纳一个小球
mdl.add_constraints(mdl.sum(x[i,j] for i in box_range) == 1
                  for j in obj_range)

mdl.print_information()
```

**目标函数表达式**

- 目标函数：小球与盒子距离和的最小值

```
# minimize total displacement
# 距离和最小
mdl.minimize( mdl.sum(distances[i,j] * x[i,j] for i in box_range for j in obj_range) )
```

此处 distances[i, j] * x[i, j] 表示前面每一个距离值distances都对应着一个x，当x[i ,j]=1时对应的distances[i,j]表示小球小球$O_j$与盒子$B_i$真正的距离。

**模型求解**

```
mdl.print_information()

assert mdl.solve(), "!!! Solve of the model fails"
```

```

mdl.report()
d1 = mdl.objective_value
#mdl.print_solution()

def make_solution_vector(x_vars):
    sol = [0]* N
    for i in box_range:
        for j in obj_range:
            if x[i,j].solution_value >= 0.5:
                sol[i-1] = j
                break
    return sol

def make_obj_box_dir(sol_vec):
    # sol_vec contains an array of objects in box order at slot b-1 we have obj(b)
    return { sol_vec[b]: b+1 for b in range(N)}
    
               
sol1 = make_solution_vector(x)
print("* solution: {0!s}".format(sol1))
```

##### 额外约束1

我们想要求 小球$O_1$ 直接放在 小球$O_2$ 的左边（挨着）。这种情况下，小球$O_2$ 就不能被放置在 盒子$B_1$ 里面了。所以添加的约束条件为：

```
mdl.add_constraint(x[1,2] == 0)
```

同样，对于盒子序号 $k\geq 2$ 时，如果 $x[k, 2]==1$，则 $x[k-1, 1]==1$。

```
mdl.add_constraints(x[k-1,1] >= x[k,2]
                   for k in range(2,N+1))
mdl.print_information()
```

现在让我们再次求解并查看新的约束是否满足，小球$O_1$ 直接放在 小球$O_2$ 的左边（挨着）。

```
ok2 = mdl.solve()
assert ok2, "solve failed"
mdl.report()
d2 = mdl.objective_value
sol2 = make_solution_vector(x)
print(" solution #2 ={0!s}".format(sol2))
```

约束条件确实被满足了，预料之中**目标函数值变大**。

##### 额外约束2

现在，我们要求 包含小球$O_5$的盒子 在 包含小球$O_6$盒子的旁边，要么在左边要么在右边。

换句话来讲，当 $x[k, 6]==1$ 时，$x[k-1,5]==1$ 或 $x[k+1, 5]==1$。

对于一些极端情况我们必须注意！

```
# for all k in 2..N-1 then we can use the sum on the right hand side
# 当 k值范围为[2, N-1]时，要么在左边要么在右边可以用下面的不等式来表示
mdl.add_constraints(x[k,6] <= x[k-1,5] + x[k+1,5]
                  for k in range(2,N))
    
# if 6 is in box 1 then 5 must be in 2
# 如果小球6在盒子1里面，那么小球5必须在盒子2里面
mdl.add_constraint(x[1,6] <= x[2,5])

# if 6 is last, then 5 must be before last
# 如果小球6在最后一个（第N=15个）盒子里面，小球5必须在前一个（N-1=14）盒子里面
mdl.add_constraint(x[N,6] <= x[N-1,5])

# we solve again
# 再次求解
ok3 = mdl.solve()
assert ok3, "solve failed"
mdl.report()
d3 = mdl.objective_value

sol3 = make_solution_vector(x)
print(" solution #3 ={0!s}".format(sol3))
```

 约束条件再次满足了，同时目标函数值更大了。

##### 第五步：查看结果和示例分析

使用 Matplotlib 我们把解答中小球和盒子用线段连接起来

```
import matplotlib.pyplot as plt
from pylab import rcParams
%matplotlib inline
rcParams['figure.figsize'] = 12, 6

def display_solution(sol):
    obj_boxes = make_obj_box_dir(sol)
    xs = []
    ys = []
    for o in obj_range:
        b = obj_boxes[o]
        box_x = box_coords[b][0]
        box_y = box_coords[b][1]
        obj_x = obj_coords[o][0]
        obj_y = obj_coords[o][1]
        plt.text(obj_x, obj_y, str(o), bbox=dict(facecolor='red', alpha=0.5))
        plt.plot([obj_x, box_x], [obj_y, box_y])
```

**第1个结果没有线段相交。**

```
display_solution(sol1)
```

**第2，3个结果有线段相交**

```
display_solution(sol2)
```

```
display_solution(sol3)
```

```

def display(myDict, title):
    if True: #env.has_matplotlib:
        N = len(myDict)
        labels = myDict.keys()
        values= myDict.values()

        try: # Python 2
            ind = xrange(N)  # the x locations for the groups
        except: # Python 3
            ind = range(N)
        width = 0.2      # the width of the bars

        fig, ax = plt.subplots()
        rects1 = ax.bar(ind, values, width, color='g')	
        ax.set_title(title)
        ax.set_xticks([ind[i]+width/2 for i in ind])
        ax.set_xticklabels( labels )	
        #ax.legend( (rects1[0]), (title) )

        plt.show()
    else:
        print("warning: no display")
        
from collections import OrderedDict
dists = OrderedDict()
dists["d1"]= d1 -8000
dists["d2"] = d2 - 8000
dists["d3"] = d3 - 8000
print(dists)

display(dists, "evolution of distance objective")
```

### 总结



### 附录--函数解释



### 参考

- [**Objects in boxes**](https://github.com/IBMDecisionOptimization/docplex-examples/blob/master/examples/mp/jupyter/boxes.ipynb)
- [CPLEX Modeling for Python documentation](http://ibmdecisionoptimization.github.io/docplex-doc/)
- [Decision Optimization on Cloud](https://developer.ibm.com/docloud/)
- Need help with DOcplex or to report a bug? Please go [here](https://stackoverflow.com/questions/tagged/docplex).
- Contact us at dofeedback@wwpdl.vnet.ibm.com.

