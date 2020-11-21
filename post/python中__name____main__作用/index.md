
###前言

在平常阅读python代码时，在代码末尾，我们经常会看见如下代码：

```
if __name__ == '__main__':
		print("This is test code!")
```

**这行代码到底是什么意思呢？或者有什么样的作用呢？**



###解释

首先，利用终端Terminal，我在Desktop创建了两个py文件

```
touch test.py
touch quote.py
```

test.py内容如下：

```
def test():
    print("This is a test code!")

print(__name__)
```

quote.py内容如下：

```
import test
test.test()
```

- 在Terminal先运行test.py，发现打印出来的值是 **\__main__**

```
python quote.py
__main__
```

解释：当我们运行 **当前py文件** 时，python的解释器，会默认的 **\__name__** = **\__main__**

即，默认把main赋值给name，这是运行当前py文件时。

- 如果我们运行quote.py，发现 **print(\__name__)** 打印出来的是 **test** 和 **This is a test code!**

解释：当运行quote.py文件时，我们只是导入test文件，并调用了里面的test函数。所以打印出来的内容有 *This is a test code!* 是在意料之中。可是与前面直接运行的 test 文件相比，print(\__name__) 输出的是 test。这说明，**当我们调用这个文件时，python的解释器会把文件名，赋值给  \_\_name\_\_，这就是直接运行与调用文件时，python解释器对 name 的赋值不同。**

**总结：**

1. 当直接运行一个python代码时，python解释器对 name 赋值 为 main。

2. 当在一个python文件调用另一python个代码时（test.py），python解释器对 name 的赋值为所调用文件的名字（test）。

3. 用途：所以当我们写好一个代码，在最后写上一行

   ```
   if __name__ == "__main__":
   	test()
   ```

   这样可以起到测试代码，且别人引用该代码时，不会输出两次。



### Reference：

[Python小技巧#1：__name__ == '__main__' 是做什么用的？](https://www.bilibili.com/video/BV1T7411v7n8)

