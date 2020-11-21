
#### Motivation

假设$f(x)$在$x_0$处具有n阶导数，是否可以找出一个关于$(x-x_0)$的n次多项式来近似表达函数$f(x_0)$的值？

即，$f(x)=p_n(x)=a_0+a_1(x-x_0)+a_2(x-x_0)^2+a_3(x-x_0)^3+···+a_n(x-x_0)^n+O((x-x_0)^n)$是否存在？

####Proof

既然$f(x)$在$x_0$处具有n阶导数，则对上面公式依次求取导数直至n阶，可以得到：

​	$a_0=f(x_0),···,a_n=\frac{1}{n!}f^n(x_0)$

#### Theorem 1

如果函数$f(x)$在$x_0$处具有n阶导数，那么存在$x_0$的一个邻域，对于该邻域内的任一$x$，有：

​	$f(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+···+\frac{f^n(x_0)}{n!}(x-x_0)^n+R_n(x)$

其中，$R_n(x)=o((x-x_0)^n)$称为佩亚诺余项（Peano form of the reminder）



反复使用洛必达法则，可以证明$R_n(x)$是$(x-x_0)$的n阶无穷小。

#### Theorem 2

如果函数$f(x)$在$x_0$处具有n+1阶导数，那么存在$x_0$的一个邻域，对于该邻域内的任一$x$，有：

​	$f(x)=\underbrace{f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+···+\frac{f^n(x_0)}{n!}(x-x_0)^n}_{p_n(x)}+R_n(x)$

其中，$R_n(x)=\frac{f^(n+1)(\epsilon)}{(n+1)!}(x-x_0)^{(n+1)}$称为拉格朗日余项（Lagrange form of the reminder），$\epsilon$是$x$和$x_0$之间的某个值。

##### proof

反复使用柯西中值定理，可以给出上面$R_n(x)$的表达式

根据Lagrange form of  the reminder可以给出误差估计，根据Theorem 2当用$p_n(x)$多项式去近似表达$f(x)$时，其误差为$|R_n(x)|$。如果对于某个固定的n，当$x\in U(x_0)$时，$|f^{n+1}(x)|\leq M$，那么就有：

  $|R_n(x)|=|\frac{f^(n+1)(\epsilon)}{(n+1)!}(x-x_0)^{(n+1)}|\leq\frac{M}{(n+1)!}|x-x_0|^{n+1}$















