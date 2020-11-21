
### 前言

理解BeautifulSoup库的一些命令，需要提前学习HTML标记语言。

当我们用Request库获取HTML的页面信息时，获取的信息其实是HTML源代码，不方便我们提取一些感兴趣的信息。而BeautifulSoup库的功能就是对HTML页面源代码进行树状分析：即，对HTML标记语言进行类区分，以便我们对HTML页面标记语言的搜索。

对HTML标签树：解析、遍历、维护。

###BeautifulSoup库的引用

```
from bs4 import BeautifulSoup
import bs4
```

**安装小测：**

```
import requests
from bs4 import BeautifulSoup
url = "http://python123.io/ws/demo.html"
r = requests.get()
print(r.text)
print('\n')
demo = r.text
soup = BeatifulSoup(demo, 'html.parser')
print(soup.prettify())
```

 ### BeautifulSoup类的基本元素

**解释器：**在给BeautifulSoup库传递网页标记语言时，要有对应的解释器，才能把网页标记语言转换成BeautifulSoup类。

```
soup = BeatifulSoup(demo, 'html.parser')
```

因为demo变量对应的是html标记语言，所以用 **html.parser** 解释器。

**BeautifulSoup类的基本元素：**

|    基本元素     |                             说明                             |
| :-------------: | :----------------------------------------------------------: |
|       Tag       |   标签，最基本的信息组织单元，分别用<>和</>标明开头和结尾    |
|      Name       | 标签的名字，对应html的标签，如\<p>...\</p>，格式：soup.name  |
|   Attributes    | 标签的属性，字典形式，对应是html语言中标签的属性值，格式：soup.attrs |
| NavigableString | 标签内非属性字符串，包括空格，换行符，文本信息等。格式：soup.string |
|     Comment     |         html语言内的注释部分，格式：soup.tag.comment         |

```
soup.title
<title>This is a python demo page</title>
#获取a标签所有信息
soup.a
<a class="py1" href="http://www.icourse163.org/course/BIT-268001" id="link1">Basic Python</a>
#获取a标签的属性值，返回的是字典
soup.a.attrs
{'href': 'http://www.icourse163.org/course/BIT-268001',
 'class': ['py1'],
 'id': 'link1'}
#获取a标签的非属性字符串信息，因为只有文本信息，所以输出的是文本
soup.a.string
'Basic Python'

#html标签等级用父子关系来表示
soup.a.name
'a'
soup.a.parent.name
'p'
soup.a.parent.parent.name
'body'

soup.parents.name
 
```

**解释：**

![BeautifulSoup_tag](/BeautifulSoup_tag.jpg)

### 基于BS4库的HTML内容遍历方法

#### 下行遍历

|     属性     |                            说明                            |
| :----------: | :--------------------------------------------------------: |
|  .contents   | 字节点的列表，将\<tag>所有儿子节点（包含换行符等）存入列表 |
|  .children   |    字节点的迭代类型，与.contents类似，用于遍历儿子节点     |
| .descendants |     子孙节点的迭代类型，包含所有子孙节点，用于循环遍历     |

#### 上行遍历

|   属性   |           说明           |
| :------: | :----------------------: |
| .parent  |      节点的父亲标签      |
| .parents | 节点的先辈标签，迭代类型 |

根标签html其parent标签就是其本身

```
for parent in soup.a.parents:
    if parent is  None:
        print(parent)
    else:
        print(parent.name)

p
body
html
[document]
```

遍历所有先辈节点，包括soup本身，所以要区别判断。

#### 平行遍历

|        属性        |                         说明                         |
| :----------------: | :--------------------------------------------------: |
|   .next_sibling    |       返回按照HTML文本顺序的下一个平行节点标签       |
| .previous_sibling  |       返回按照HTML文本顺序的上一个平行节点标签       |
|   .next_siblings   | 迭代类型，返回按照HTML文本顺序的后面所有平行节点标签 |
| .previous_siblings | 迭代类型，返回按照HTML文本顺序的前面所有平行节点标签 |

注：平行遍历发生在**同一个父节点下**！节点含义，包含所有跟标签并列关系。要好好理解。

![BeautifulSoup_遍历](/BeautifulSoup_遍历.jpg)

#### prettify()方法

使得HTML文件更友好的显示，而且可用于标签。

```
<tag>.prettify()
```







