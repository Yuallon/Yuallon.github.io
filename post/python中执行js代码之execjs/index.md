
#### JS代码编写

js代码执行之前需要在运行时环境下编译才能执行
　　由于该js环境下没有`window`、`document`对象，也没有console面板，因此在使用某些基于浏览器的原生对象在编译过程时会报错。所以在使用`compile`函数时尽量以函数的形式来写js代码，方便Python调用。

```
import execjs 


js = """ 
function add(x, y) { 
  return x + y; 
} 
"""

###  编译成JS代码 
ctx = execjs.compile(js) 
###  call方法来调用JS代码中的add函数
print(ctx.call("add", 3, 2)) 
```

另外有时候js代码过长，我们可以将js代码先保存到文件中。
　　由于历史遗留问题，ExecJS以前使用python2编写的，所以在代码实现过程中会涉及到文件编码的问题。ExecJS先将js代码读到内存中，然后再把调用js的代码和js文件的代码一同写入到一个临时文件（C:\Users\user\AppData\Local\Temp\xx.js）中，如果js文件采用的是UTF-8编码，那么在写入到临时文件时，模块会报`UnicodeEncodeError: 'gbk' codec can't encode character xxx` ，主要是因为模块在进行文件写入时采用的是windows的默认编码gbk，而没有指定`encoding=utf-8`，所以js文件需要以gbk编码保存。

```
with open('/Users/huangyulong/Desktop/js_test.js') as f:
    js = f.read()
    
ctx = execjs.compile(js)
print(ctx.call("add", 3, 2)) 
```

### 参考

- [Python3 ExecJS爬坑](https://www.jianshu.com/p/6e12c6a69f10)
- [python爬虫 execjs安装配置及使用](https://www.jb51.net/article/166556.htm)

