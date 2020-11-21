
使用 **plt.scatter()** 函数来绘制散点图

**例子1:**

```
import numpy as np
import matplotlib.pyplot as plt

N = 50

x = np.linspace(0., 10., N)
y = np.sin(x)**2 + np.cos(x)

plt.figure()
plt.scatter(x, y)

plt.axis('equal')
plt.xlabel(r'$x$ (rad)')
plt.ylabel(r'$sin^2(x)$')
plt.scatter(x, y, s = 15, label = r'$y = sin^2(x) + cos(x)$', marker='^', color='b')
plt.legend()
```

![散点图1](/Users/huangyulong/myblog/static/散点图1.jpg)

解释：

- plt.axis('equal')：使x，y轴比例尺相同
- plt.ylabel(r'\$sin^2(x)​\$')：绘制y轴标签，**可以使用LaTex语法**。
- plt.scatter()：绘制散点图，参数s是标记样式marker大小的设置，label参数是图内标签，color是颜色
- plt.legend()：显示图内标签
- 更多样式参考：https://matplotlib.org/api/markers_api.html

**例子2:**

```
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.ticker import MultipleLocator

N = 30

plt.figure(figsize=(7, 6))

randx = np.random.random(N) * 100
randy = np.random.random(N) * 100
size = np.random.randint(50, 200, size=N)

plt.axis('equal')

ax = plt.gca()
ax.xaxis.set_minor_locator(MultipleLocator(10))
ax.yaxis.set_minor_locator(MultipleLocator(10))

plt.xlabel('randx')
plt.ylabel('randy')

plt.scatter(randx, randy, s = size, color = 'darkorange')
```

![散点图2](/Users/huangyulong/myblog/static/散点图2.jpg)

**解释：**

- MultipleLocator模块：在x轴，y轴上插入次刻度。
- plt.figure()：figsize参数用来设置图形尺寸参数

**例子3:**

```

```







### 参考资料

- [30000字 Matplotlib 实操干货，38个案例带你从入门到进阶！](https://mp.weixin.qq.com/s/cRSytYAOcmhfMkSIhKrfFw)







| 食物 | 单价（元） | 维他命A | 卡路里 |
| :--: | :--------: | :-----: | :----: |
| 玉米 |    1.8     |         |        |
| 牛奶 |    2.3     |         |        |
| 面包 |    5.0     |         |        |

