
### 为什么要JS解析？

刚开始学习爬虫的时候，我练习的案例主要是通过Requests库请求一些简单的网页，或者通过Selenium自动化工具来抓取页面渲染过后的数据。使用Selenium最大的缺点就是：慢、效率低。因为Selenium爬取网页是通过模拟人对浏览器的行为，来实现数据的爬取的。对于数据量比较少的，Selenium还是可以胜任，但是如果爬取的数据量很庞大，那么用Selenium来进行数据的爬取显然是不合适的。

鉴于Selenium爬取效率低下的问题，让我们回到一个最初始的问题：为什么要爬虫？

显然，我们做爬虫程序就是为了获取互联网上的资源，狭隘的讲是获取HTML页面上的数据，而HTML数据是服务器对客户端请求响应生成的。那么爬虫问题归根结底就成为了：**如何给服务器成功发送请求？**的问题。

客户端给服务器发送请求，便属于HTTP协议范畴，在这里不细讲。简单来说：客户端需要给服务器发送一个信息包（请求头部信息+请求数据信息），头部信息会告诉服务器（我是谁、我需要什么类型的数据等等），请求的数据信息则会告诉服务器你想要哪一个数据的信息（比如：我想知道world中文翻译的信息，那么数据信息里面就包含了world这个单词）。

虽然 **请求 = 请求头+数据信息** ，但是服务器为了自身的安全性考虑，并不会直接接收 **world** 这个单词，而是接收加密后的字符串再返回响应结果。这就是 **JS加密：当我们在浏览器中输入某一个关键字时，JS代码会先进行加密，然后将加密后的信息放在 请求 里面发送给服务器。** 所以为了爬取有道翻译，我们最先要解决的便是如何知道我们输入一个单词（world），有道翻译界面是如何把单词加密的，这便是 **JS解析**。只有拿到加密后的数据放到请求里面发送给有道翻译服务器，才能成功获得响应数据。

### JS解析的一般步骤

JS解析的目的：获取每次输入关键字后，加密后的数据。所以最关键的目标就是找到加密的方式——JS代码。

![爬取有道翻译界面](/爬取有道翻译界面.jpg)

- **查看请求的数据参数有哪些**

  ![yd请求头](/yd请求头.jpg)

  请求头信息

  ![yd请求数据](/yd请求数据.jpg)

  输入world时，请求的数据信息

  ![hi请求数据信息](/hi请求数据信息.jpg)

  输入hi时请求数据信息

  对比发现：world请求信息 与 hi请求信息 只有i、salt、sign、lts四个参数不同。i代表查询的单词这个很明显，剩余的3个参数时如何生成的呢？

- **JS数据解析 **

  在 Initiator中点击js代码（如果一开始不知道点那个，就慢慢试一试吧）

  ![ydJS解析](/ydJS解析.jpg)

  然后搜索前面找到的参数，找到对应的JS函数

  ![ydJS解析1](/ydJS解析1.jpg)

  通过对上面红色框框里的JS函数代码分析，可知道：

  - ts：r是获得当前的时间戳
  - salt：i是当前时间戳+[0,9]之间一个随机数
  - sign：对("fanyideskweb" + e + i + "]BjuETDhU)zqSxf-=B#7m")MD5加密，e代表输入的单词，i是salt值。

- **python代码实现JS函数功能**

  ```
  """
  获取请求data中 ts、salt、sign参数值
  word：为输入的单词
  return：返回data参数
  """
  # word = input("请输入查询的英文单词：")
  ####  生成字符串时间戳
  lts = str(int(time.time()*1000)) 
  ####  salt值
  salt = lts + str(random.randint(0, 9))
  ###   MD5加密
  string = "fanyideskweb" + word + salt + "]BjuETDhU)zqSxf-=B#7m"
  m = hashlib.md5()
  m.update(string.encode('utf-8'))
  sign = m.hexdigest() 
  ```

### 完整代码

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sat Oct  3 09:06:33 2020

@author: huangyulong
"""



import time 
import random
import hashlib
import requests



class YdSpider:
    def __init__(self):
        self.url = 'http://fanyi.youdao.com/translate_o?smartresult=dict&smartresult=rule'
        self.headers = {
            'Accept': 'application/json, text/javascript, */*; q=0.01',
            'Accept-Encoding': 'gzip, deflate',
            'Accept-Language': 'zh,en-US;q=0.9,en;q=0.8',
            'Connection': 'keep-alive',
            'Content-Length': '239',
            'Cookie': 'OUTFOX_SEARCH_USER_ID=-1723811673@10.108.160.19; JSESSIONID=aaaMiirrU-S23-SA6tQtx; OUTFOX_SEARCH_USER_ID_NCOO=937885199.0894697; ___rl__test__cookies=1601659248133',
            'Host': 'fanyi.youdao.com',
            'Origin': 'http://fanyi.youdao.com',
            'Referer': 'http://fanyi.youdao.com/',
            'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36',
            'X-Requested-With': 'XMLHttpRequest'      
            }
    def get_lts_salt_sign(self, word):
        """
        获取请求data中 ts、salt、sign参数值
        word：为输入的单词
        return：返回data参数
        """
        # word = input("请输入查询的英文单词：")
        ####  生成字符串时间戳
        lts = str(int(time.time()*1000)) 
        ####  salt值
        salt = lts + str(random.randint(0, 9))
        ###   MD5加密
        string = "fanyideskweb" + word + salt + "]BjuETDhU)zqSxf-=B#7m"
        m = hashlib.md5()
        m.update(string.encode('utf-8'))
        sign = m.hexdigest()
        
        data = {
            'i': word,
            'from': 'AUTO',
            'to': 'AUTO',
            'smartresult': 'dict',
            'client': 'fanyideskweb',
            'salt': salt,
            'sign': sign,
            'lts': lts,
            'bv': 'ce569c6db40f23fa5fccffa48b782c4b',
            'doctype': 'json',
            'version': '2.1',
            'keyfrom': 'fanyi.web',
            'action': 'FY_BY_REALTlME'
            }
        return data
    
    def req_translate(self, data):
        """发起请求"""
        resp = requests.post(url=self.url, headers=self.headers, data=data).json()
        # print(resp)
        return resp
    
    def decode_translate(self, resp):
        translateResult = resp['translateResult']
        tgt = translateResult[0][0]['tgt']
        src = translateResult[0][0]['src']
        return tgt, src
        # smartResult = resp['smartResult']

    
    def main(self, word):
        data = self.get_lts_salt_sign(word)
        resp = self.req_translate(data)
        tgt, src = self.decode_translate(resp)
        print("您查询的单词是：%s" %src)
        print("中文翻译结果是：%s" %tgt)
        
        
        
if __name__ == '__main__':
    spider = YdSpider()
    word = input("请输入查询的英文单词：")
    spider.main(word)

```

### 总结

通过学习有道翻译界面的爬取，是自己第一次进行JS解析，然后再爬取数据。这个例子让我深刻理解了HTTP请求的流程，以前只是局限于书中介绍的一些知识点。其实真实的HTTP请求中，是先通过JS函数对数据加密，然后再添加再请求数据包里面。这也是目前绝大部分网站反爬虫的主要手段。

### 参考

[【Python爬虫 Js逆向】简单案例 +环境配置](https://www.bilibili.com/video/BV1fC4y1H7XD?p=1)

