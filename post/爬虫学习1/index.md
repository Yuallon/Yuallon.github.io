
### 爬虫有风险，操作需谨慎！



### 网络爬虫的限制

- 来源审查：判断 **user-agent** 进行限制
  检查来访HTTP协议头的user-agent域，只响应浏览器或友好爬虫访问
- 发布公告：**Robots协议**
  告知所有爬虫网站的爬取策略，要求爬虫遵守。
  准备爬取某个网站信息的时候，一定要看该网站的robots.txt文件，看有哪些数据限制。

### Robots协议基本语法

```
#注释，*代表所有，/代表根目录
User-agent：*
Disallow：/
```

### 实例1: 京东商品页面的爬取

```
import requests


def getHTMLText(url):
	try:
		r = requests.get(url, timeout=30)
		r.raise_for_status() #如果状态码不是200，引发HTTPError异常
		r.encoding = r.apparent_encoding
		print(r.text[:1000])
	except:
		return "产生异常"
    
    
##爬取京东商品页面
url_jd = "https://item.jd.com/2967929.html"
getHTMLText(url_jd)
```

但是我用相同的方式去爬取亚马逊页面上的商品信息时，亚马逊页面进行了 **cookie** 保护。不能成功爬取。

那么：反爬的方法有哪些呢？cookie，au如何实现反爬呢？

### 实例2：360搜索引擎关键词提交口

实现这个关键，是用参数 **params=keyword**。可以吧keyword添加到url中，使得满足一些搜索引擎的关键字接口。

**360的关键词接口：**

```
http://www.so.com/s?q=keyword
```

代码实现

```
import requests
keyword = "python"
url = "http://www.so.com/s"
#url = "http://www.baidu.com/s"
try:
    kv = {'q':keyword}
    r = requests.get(url, params=kv)
    r.raise_for_status() #如果状态码不是200，引发HTTPError异常
    r.encoding = r.apparent_encoding
    print(r.text[:])
except:
    print("产生异常")
```

但是对百度进行类似的操作时，出现了问题，说明百度实行了反爬机制！

百度关键词接口

```
http://www.baidu.com/s?wd=keyword
```

### 实例3:网络图片的爬取和存储

实现这个关键，是用 **r.content** 。因为图片是采用二进制存储的。

**代码实现：**

```
import requests
import os
url = "https://gss0.baidu.com/-vo3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/ca1349540923dd546b32cfb8d909b3de9d824898.jpg"

root = "/Users/huangyulong/Desktop/"
path = root + url.split('/')[-1]
try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r =requests.get(url)
        with open(path, 'wb') as f:
            f.write(r.content)
            f.close()
            print("文件保存成功")
    else:
        print("文件已存在")
except:
    print("爬取失败")
```

### 学习心得

实例2，给了我很大的启发。当我们对某个网站感兴趣时，并且想借助该网站通过代码完成自己某个搜索功能。那我们就要先学会分析该网站的 **关键字接口** 即 在该网站手动输入一个关键字，然后查看网站http界面的变化。分析完该网站的http接口方式，这样就可以用爬虫利用该网站的某些功能啦。

**r.content** 返回的是内容的二进制信息，可用来保存图片。

### 待学习内容：

1. 如何实现发爬机制？



