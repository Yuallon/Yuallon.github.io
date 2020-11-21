
###MD5加密简介

全称：MD5消息摘要算法(英语：MD5 Message-Digest Algorithm)，一种被广泛使用的密码散列函数，可以产生出一个128位(16字节)的散列值(hash value)，用于确保信息传输完整一致。md5加密算法是不可逆的，所以解密一般都是通过暴力穷举方法，通过网站的接口实现解密。

### python 实现

```
###导入哈希模块
import hashlib
###创建md5对象
m = hashlib.md5()
###传入需要加密的字符串进行MD5加密
m.update(string.encode('utf-8'))
###然后获得经过MD5加密后的字符串
encodeStr = m.hexdigest()
###输入结果
print('encodeStr')


###method1
def md5str(str):
    m = hashlib.md5(str.encode(encoding="utf-8"))
    return m.hexdigest()
    
###method2
def md5(byte):
    return hashlib.md5(byte).hexdigest()
```

### 参考

- [Python MD5加密](https://cloud.tencent.com/developer/article/1406679)
- [Python实现常见的几种加密算法(MD5，SHA-1，HMAC，DES/AES，RSA和ECC)](https://www.jb51.net/article/186188.htm)

