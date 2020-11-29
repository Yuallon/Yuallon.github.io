
###决策树介绍

决策树类似于流程图，其内部每个节点代表一个属性上的“测试”，每一个分支代表测试的结果，每个叶节点代表一个分类。从根节点到叶节点代表分类的规则。

一个决策树包含3种节点：

- 决策节点（Decision nodes）：一般用方形表示，决策开始的根节点。
- 机会节点（Chance nodes）：一般用圆形表示，表示一个特征或属性。
- 尾节点（End nodes）：一般用三角形表示，表示一个分类。

![决策树图1](/决策树图1.jpg)

####例子

问题：银行要用机器学习算法来确定是否给客户发放贷款，为此需要考察客户的年收入，是否有房产这两个指标。

思路：首先判断客户的年收入指标。如果大于20万，可以贷款；否则继续判断。然后判断客户是否有房产。如果有房产，可以贷款；否则不能贷款。

![决策树图2](/决策树图2.jpg)

####决策树学习的 3 个步骤

1. **特征选择**

   特征选择决定了使用哪些特征来做判断。在训练数据集中，每个样本的属性可能有很多个，不同属性的作用有大有小。因而特征选择的作用就是筛选出跟分类结果相关性较高的特征，也就是分类能力较强的特征。

   在特征选择中通常使用的准则是：信息增益。

2. **决策树生成**

   选择好特征后，就从根节点触发，对节点计算所有特征的信息增益，选择信息增益最大的特征作为节点特征，根据该特征的不同取值建立子节点；对每个子节点使用相同的方式生成新的子节点，直到信息增益很小或者没有特征可以选择为止。

3. **决策树剪枝**

   剪枝的主要目的是对抗「过拟合」，通过主动去掉部分分支来降低过拟合的风险。

####优缺点

#####优点：

- 容易理解，可以可视化分析，容易提取出规则。
- 可以同时处理标称型和数值型数据
- 比较适合处理有缺失属性的样本
- 能够处理不相关的特征
- 运行速度比较快（随着节点的下降速度越快）
- 短时间内能够对大型数据源做出可行且效果良好的结果
- 可以有多个输出
- 树的可靠性可以被测试和量化

#####缺点：

- 容易发生过拟合（随机深林可以很大程度上减少过拟合）
- 容易忽略数据集中属性的相互关联
- 对于那些各类别样本数量不一致的数据，在决策树中，进行属性划分时，不同的判定准则会带来不同的属性选择倾向；信息增益准则对可取数目较多的属性有所偏好（典型代表ID3算法），而增益率准则（CART）则对可取数目较少的属性有所偏好，但CART进行属性划分时候不再简单地直接利用增益率尽心划分，而是采用一种启发式规则）（只要是使用了信息增益，都有这个缺点，如RF）。
- ID3算法计算信息增益时结果偏向数值比较多的特征。
- 处理不确定性和许多相关输出时，计算可能会变得复杂。

###决策树在机器学习和数据挖掘中的应用

决策树可以用来构建预测模型，常用于机器学习、数据挖掘和统计分析。这种方法称为决策树学习，通过对item观察以预测item的value。

在这些决策树中，节点代表了数据而不是决策。比如典型的分类树。每一个分支包含了一些的特征或者分类规则，这个特征或规则来决定末端节点的标签类别。这些决策规则可以用 **if-then-else** 语句来解释。

有时候预测的变量可能是真实的数值，如价格。输出连续值的决策树被称为回归树。

为了提高决策树的精度，有时候需要多个决策树共同作用：

- **Bagging方法**：多个决策树投票给出结果。
- **Random Forest classifier 方法**：由多个树模型组成，用来提高分类效率。
- **Boosted trees**：可以分为回归树和分类树。
- **Rotation Forest**：基于数据的随机片段，通过PCA训练树模型。

###Scikit-Learn中决策树可视化

```
from matplotlib import pyplot as plt
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier 
from sklearn import tree

#数据准备
iris = datasets.load_iris()
X = iris.data
y = iris.target

#模型训练
clf = DecisionTreeClassifier(random_state=1234)
model = clf.fit(X, y)

#打印文字信息
#对于没有用户交互的应用界面和当我们想记录决策树日志时，打印出决策树文字有时候很有用
text_representation = tree.export_text(clf)
print(text_representation)

#绘制决策树
fig = plt.figure(figsize=(25,20))
dt_fig = tree.plot_tree(clf, 
                   feature_names=iris.feature_names,  
                   class_names=iris.target_names,
                   filled=True)
```

效果图如下：

![decistion_tree](/decistion_tree.png)

### 参考资料

- [决策树 – Decision tree](https://easyai.tech/ai-definition/decision-tree/#:~:text=决策树的优缺点%201%20决策树易于理解和解释，可以可视化分析，容易提取出规则；%202%20可以同时处理标称型和数值型数据；%203,比较适合处理有缺失属性的样本；%204%20能够处理不相关的特征；%205%20测试数据集时，运行速度比较快；%206%20在相对短的时间内能够对大型数据源做出可行且效果良好的结果%E3%80%82)
- [**What is a Decision Tree Diagram**](https://www.lucidchart.com/pages/decision-tree)
- [Visualize a Decision Tree in 4 Ways with Scikit-Learn and Python](https://mljar.com/blog/visualize-decision-tree/)

  

