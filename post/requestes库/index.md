
### Requestes库

[Requestes库官方网站](http://www.python-requests.org)

**安装方式：pip install requests（在终端）**

**Requestes库的7个主要方法：**

|              方法              |                      说明                      |
| :----------------------------: | :--------------------------------------------: |
|      requestes.request()       |     构造一个请求，支撑以下各方法的基础方法     |
| $\color{red}{requestes.get()}$ |    获取HTML网页的主要方法，对应于HTTP的GET     |
|        requestes.head()        |      获取网页头信息方法，对应于HTTP的HEAD      |
|        requestes.post()        | 向HTML网页提交POST请求的方法，对应于HTTP的POST |
|        requestes.put()         |  向HTML网页提交PUT请求的方法，对应于HTTP的PUT  |
|       requestes.patch()        | 向HTML网页提交局部修改请求，对应于HTTP的PATCH  |
|       requestes.delete()       |   向HTML网页提交删除请求，对应于HTTP的DELETE   |

在这个7个方法中，**requests.request()**函数，包含余下6个函数功能。最重要的是 **requestes.get()** 方法。

#### r = requests.get(url, params=None, **kwargs)

- url：拟获取页面的url连接

- params：url中的额外参数，字典或字节流格式，**作为参数增加到url中**

  ```
  import requests
  kv = {'key1' : 'value1', 'key2' : 'value2'}
  r = requests.get('http://python123.io/ws', params=kv)
  print(r.url)
  https://python123.io/ws?key1=value1&key2=value2
  ```

  

- **kwargs：12个可控制参数
  data：字典、字节序列或文件对象，作为Request的内容
  json：JSON格式数据，作为Request的内容
  headers：字典，可以修改HTTP协议头部信息，用来模拟浏览器访问服务器

  ```
  hd = {'user-agent' : 'Chrome/10'}
  r = requests.post('http;//python123.io/ws', headers=hd)
  ```

  coocies：字典或CookieJJar，Request中cookie
  auth：元组，支持HTTP认证功能
  files：字典类型，传输文件

  ```
  fs = {'file' : open('data.xls', 'rb')}
  r = requests.post('http://python123.io/ws', files=fs)
  ```

  timeout：设定超时时间，秒为单位

  ```
  r = requests.get('http://www.baidu.com', timeout=30)
  ```

  proxies：字典类型，设定访问代理服务器，可以增加登陆认证

  ```
  pxs = {'http' : 'http://user:pass@10.10.10.1:1234'
  			 'https:' : 'https://10.10.10.1:1234'}
  r = requests.get('http://www.baidu.com', proxies=pxs)
  #注释：因此用户爬取源的IP信息，而采用代理服务器的IP地址爬取百度，防止逆追踪
  ```

  allow_redirects：True/False，默认为Ture，重定向开关
  strem：True/False，默认为Ture，获取内容立即下载开关
  verify：True/False，默认为Ture，认证SSL证书开关
  cert：本地SSL认证书路径

- r：是返回的对象，response对象，下面是Response对象常用属性（$\color{red}{重点掌握}$）

  |        属性         |                             说明                             |
  | :-----------------: | :----------------------------------------------------------: |
  |    r.status_code    | HTTP请求返回的状态码，200表示连接成功，404表示失败。其余的详细参考HTTP返回状态码值及其含义 |
  |       r.text        |       HTTP相应内容的字符串格式，即，url对应的页面内容        |
  |     r.encoding      |          从HTTP header中 **猜测** 响应内容编码格式           |
  | r.apparent_encoding |        从 **HTTP页面内容** 中分析出相应内容的编码格式        |
  |      r.content      | HTTP响应内容的二进制格式（比如图片的信息，是以二进制存储的） |
  |      r.headers      |                   HTTP响应内容的header信息                   |

#### 通用代码框架

```
import requests

def getHTMLText(url):
	try:
		r = requests.get(url, timeout=30)
		r.raise_for_status() #如果状态码不是200，引发HTTPError异常
		r.encoding = r.apparent_encoding
		return r.text
	except:
		return "产生异常"
		
if __name__ == "__main__" :
	url = "http://www.baidu.com"
	print (getHTMLText(url))
```

通用代码框架，可以有效的处理爬取过程中可能会出现的异常情况。使得程序变得**更有效，更稳定，更可靠**。





