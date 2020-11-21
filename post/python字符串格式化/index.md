
- **例子**1：

  ```
  age = 7
  print("我今年%d岁了!" %age)
  ```

- **例子2**：

  ```
  >>>"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
  'hello world'
   
  >>> "{0} {1}".format("hello", "world")  # 设置指定位置
  'hello world'
   
  >>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
  'world hello world'
  ```

- **例子3**：

  ```
  #!/usr/bin/python
  # -*- coding: UTF-8 -*-
   
  print("网站名：{name}, 地址 {url}".format(name="菜鸟教程", url="www.runoob.com"))
   
  # 通过字典设置参数
  site = {"name": "菜鸟教程", "url": "www.runoob.com"}
  print("网站名：{name}, 地址 {url}".format(**site))
   
  # 通过列表索引设置参数
  my_list = ['菜鸟教程', 'www.runoob.com']
  print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的
  ```

### 更多查看

- [Python format 格式化函数](https://www.runoob.com/python/att-string-format.html)
- [Python 字符串格式化](https://www.w3school.com.cn/python/python_string_formatting.asp)