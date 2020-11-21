
今天用python写了一个求取10,000以内的质数算法，想着查看程序运行的的时间。来对比不同算法执行时间。

在python官网有 **time模块**计数器的介绍：[time-Time access and conversion](https://docs.python.org/3/library/time.html?highlight=time%20clock#time.process_time)。现在写一下自己的理解。

**部分术语：**

1. **纪元（epoch）：**是指时间开始的最初时刻点，它对系统（platform）有依赖性。对于 **Unix系统** 纪元是指：1970年1月1日0时0分0秒（世界时UTC）。执行 *time.gmtime(0)* 可以查看系统的纪元。
2. **自纪元以来秒数：**是指从纪元开始以来，总共流逝的时间。这里面不包含跳秒。

**函数对比：**

- **time.perf_counter()：**返回 **系统计数器的值**（以秒为单位，包含小数值）。它是系统内分辨率最高的计数器，可以给出很小的执行时间。返回值是系统层面上的，包含系统休眠时间。参考的时间起点不明确（因为不同的电脑升级or安装Unix系统的时间轴不是固定的？），所以取两次返回值的差才是有意义的。
  **所以，我们可以在一个程序（process）开始 和 结束 分别取值，差值就是系统对程序的响应时间。**
- **time.process_time()：**返回的值是 **系统** 和 **CPU** 对当前程序（current process）运行的总时间（以秒为单位，包含小数值）。它不包含系统的休眠时间（因为你要执行程序，就需要激活系统状态）。所以它是全过程的（process-wide）。参考的时间点不明确，只有差值有意义。
  **所以，可以利用这个差值查看一个程序，在某台电脑上，系统和CPU的总响应时间。**
- **time.time()：**返回自 **纪元** 以来的 **秒数**（以秒为单位，浮点数）。纪元的具体日期和对跳秒的处理方式取决于不同的系统。在Windows和大部分的Unix系统，纪元都是设定在 January 1, 1970, 00:00:00 (UTC) 且 不包含跳秒。
  **所以，这个返回值是系统对于纪元的时间长度，有明确的时间起点，也可以用差值计算程序的系统响应时间。**
  **注意⚠️：尽管它总是给出一个浮点数值，并不是所有的系统的时间精度都好于1秒，虽然这个函数通常返回非递减值，如果在两次响应之间系统时间被回调，第二次的返回值可能会比第一次返回值要小。**

### 程序实例：

```
import time
start1 = time.process_time()
start2 = time.perf_counter()
start3 = time.time()
#value = int(input("请输入查找的范围："))
value = 10000
prime_number = []
for number in range(value+1):
#    number = int(input("请输入查找的范围："))
    if number >=2:
        n = 0
        for i in range(number):
            i += 1
            if (number % i) == 0:
                n += 1
        if n == 2:
            #print(number, end = '\t')
            prime_number.append(number)
        #else:
            #print("不是质数")
#else:
  #print("查找失败，请检查输入的数字")
end1 = time.process_time()
end2 = time.perf_counter()
end3 = time.time()
sum1_time = end1 - start1
sum2_time = end2 - start2
sum3_time = end3 - start3
print("process_time:%.3f" % sum1_time)
print("perf_time:%.3f" % sum2_time)
print("time_time:%.3f" % sum3_time)

#output:我的电脑响应时间对比
process_time:16.129
perf_time:8.173
time_time:8.173
```

