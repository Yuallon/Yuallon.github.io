
### 多任务

当我们利用电脑上网时，可以一遍听音乐一边看新闻或者一边做其他事情。这说明电脑在同时运行多个任务。我们知道无论是看新闻还是听音乐，最终都离不开CPU执行相应的程序，虽然多核的CUP电脑已经很普及了，不同的程序可以分给不同的CPU去执行。但是，即是是单核CPU也可以做到这点，当CPU处理速度很快时（0.01s），不同的任务（听音乐、看电影）交替执行，因为CPU速度很快，所以我们感觉这些程序同时执行一样。

#### 进程（Process）

对于操作系统来说，一个任务就是一个进程。如打开浏览器，打开记事本，打开播放器等。

#### 线程（Thread）

一个进程里面可以做很多事情，如打开浏览器是一个**进程**，在浏览器页面又可以打开很多网页，每一个网页就是一个**线程**。所以，一个进程一定至少包含一个线程。

#### 如何实现多任务？

1. 启动多个进程，每一个进程代表一个任务。
2. 在一个进程里面，启动多个线程，每一个线程代表一个任务。
3. 或者，多进程 + 多线程混合使用。

Python既支持多进程，也支持多线程。



### 多进程



### 多线程

 多任务可以由多个进程完成，也可以由一个进程内部的多个线程来完成。

在Python中，提供了 **_thread** 和 **threading** 两个模块实现多线程的操作。其中 **_thread**是低级模块，**threading**是高级模块。

#### threading  ---- 基于线程的并行

在 **threading**模块中，定义了以下函数和对象。

##### threading模块中的函数

- threading.**active_count()**
  返回当前存活的线程 **Thread类** 的个数。相当于len(threading.enumerate())见下面的解释。

  ```
  import time, threading
  threading.active_count()
  #output
  5
  ```

  

- threading.**enumerate()**

  enumerate：vt 枚举，列举，数

  以列表的形式返回当前存活的 **Thread** 对象。

  ```
  threading.enumerate()
  #output
  [<_MainThread(MainThread, started 140735653847936)>,
   <Thread(Thread-2, started daemon 123145329225728)>,
   <Heartbeat(Thread-3, started daemon 123145334480896)>,
   <HistorySavingThread(IPythonHistorySavingThread, started 123145340809216)>,
   <ParentPollerUnix(Thread-1, started daemon 123145347674112)>]
  ```

  

- 