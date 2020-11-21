
###基于BS4库的HTML内容查找方法

**函数：**

```
<>.find_all(name, attrs, recursive, string, **kwargs)
```

返回一个列表类型，存储查找的结果

- name：对标签名称的检索，字符串类型。可以输入字符串列表。
- attrs：对标签属性值进行检索
- recursive：是否对子孙全部检索，默认为True
- string：对标签内字符串区域检索

注：tag(..) 等价于 tag.find_all()；soup(..) 等价于 soup.find_all(..)

扩展方法：

1. <>.find()：只返回一个结果
2. <>.find_parents()：返回一个列表
3. <>.find_parent()
4. <>.find_next_siblings()
5. <>.find_next_sibling()
6. <>.find_previous_siblings()
7. <>.find_previous_sibling()



### 实例

提取HTML中所有URL链接

思路：

1. 找到所有的 **a** 标签
2. 解析 **a** 标签，提取href后的链接内容

**代码实现：**

```
from bs4 import BeautifulSoup
import requests
url = "http://python123.io/ws/demo.html"
r = requests.get()
demo = r.text
soup = BeatifulSoup(demo, 'html.parser')
for link in soup.find_all('a'):
	print(link.get('herf'))
```

### 爬取最好大学网上面2020年最新大学排名

#### 目标：

- 在 *最好大学网* 找到2020年全国大学排名页面，分析html页面构成
- 利用爬虫方法实现对：大学排名的爬取，并存到Excel表格里面

#### 程序的结构设计：

- 步骤1: 从网络上获取2020年大学排名的网页内容，可用Requests库实现
- 步骤2: 提取网页内容中信息到合适的数据结构
- 步骤3: 存取提取到的数据到Excel

参考网站：[2020软科中国大学排名（总榜）](http://www.zuihaodaxue.com/zuihaodaxuepaiming-zongbang-2020.html)

```
import requests
from bs4 import BeautifulSoup
import pandas as pd

#url = "http://www.zuihaodaxue.com/zuihaodaxuepaiming-zongbang-2020.html"
#步骤1
def getHTMLText(url):
	try:
		r = requests.get(url)
		r.raise_for_status()
		r.encoding = r.apparent_encoding
		return r.text
	except:
		return "爬取异常"
        

#html = getHTMLText(url)
#步骤2
def UnivList(html):
    try:
        soup = BeautifulSoup(html, 'html.parser')
        ulist=[]
        #找到数据列表主体<body>...</body>
        body = soup.find('body')
        #数据行<tr>...</tr>表示每一个学校的信息
        trs = body.find_all('tr')
        for tr in trs[1:]:
            #提取每一个数据行中的数据块string信息
            tds = tr.find_all('td')
            a = []
            for td in tds:
                a.append(td.string)
            ulist.append(a)
        return ulist   
    except:
        return "异常"
        
#步骤3       
def dfList(ulist, columns):
    try:
        df = pd.DataFrame(ulist)
        #列表第一行信息
        df.columns = columns
        return df
    except:
        print("获取列表异常")
    
 
def main():
    url = "http://www.zuihaodaxue.com/zuihaodaxuepaiming-zongbang-2020.html"
    columns=['排名','学校名称','省市','学校类型','总分']
    html = getHTMLText(url)
    University_list = UnivList(html)
    df = dfList(University_list, columns)
    df.to_excel("uList.xlsx", index=False)
    print("爬取成功")
main()
```

我的思路跟嵩老师的不一样， 嵩老师是通过RE库的命令来优化大学排名在打印时候的美观性。爬虫的目的是爬取信息，所以我选择直接存储到Excel文件中。

在写代码的时候遇到了一个问题：对一个变量修改后再赋予同一个变量名，会引发NoneType

例如：步骤2中我返回的变量是ulist，如果我在main函数中，把UnivList函数返回的结果再赋值给ulist，则就会出现报错

```
ulist = UnivList(html)
```

这时候要采用新的变量名。

#### 嵩老师代码：

```
#CrawUnivRankingB.py
import requests
from bs4 import BeautifulSoup
import bs4

def getHTMLText(url):
    try:
        r = requests.get(url, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ""

def fillUnivList(ulist, html):
    soup = BeautifulSoup(html, "html.parser")
    for tr in soup.find('tbody').children:
        if isinstance(tr, bs4.element.Tag):
            tds = tr('td')
            ulist.append([tds[0].string, tds[1].string, tds[3].string])

def printUnivList(ulist, num):
    tplt = "{0:^10}\t{1:{3}^10}\t{2:^10}"
    print(tplt.format("排名","学校名称","总分",chr(12288)))
    for i in range(num):
        u=ulist[i]
        print(tplt.format(u[0],u[1],u[2],chr(12288)))
    
def main():
    uinfo = []
    url = 'http://www.zuihaodaxue.cn/zuihaodaxuepaiming2016.html'
    html = getHTMLText(url)
    fillUnivList(uinfo, html)
    printUnivList(uinfo, 20) # 20 univs
main()
```

