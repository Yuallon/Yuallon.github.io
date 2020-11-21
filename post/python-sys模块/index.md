
### 前言

**sys模块** 提供了对解释器及相关功能的操作。主要用于操控python运行时的环境。

### 常用函数

- **sys.argv()**：用于从命令行获取传入python script的变量。argv[0]是脚本的名字，如果没有脚本名字传给python解释器，则为空。

  [Python中 sys.argv[]的用法简明解释](https://www.cnblogs.com/aland-1415/p/6613449.html)，给出了比较详细的代码分析。

- **sys.platform()**：返回系统平台类型。

  |  系统   |  返回值  |
  | :-----: | :------: |
  | Windows | 'win32'  |
  |  Linux  | 'linux'  |
  |  macOS  | 'darwin' |

- **sys.exit()**：从python程序退出。在try 语句中，通过产生SystemExit 错误类型，实现程序的清除。一般传入整数类型，0是默认，表示正常退出。非0值（1-127），表示非正常退出。

- **sys.path()**：返回一个路径string列表。path[0]表示唤醒python解释器的路径。

- **sys.modules.keys()**：返回python中已导入的模块。



### Reference

1. [sys -- System -- specific parameters and functions](https://docs.python.org/3/library/sys.html)
2. [python学习之——import sys模块](https://blog.csdn.net/u013203733/article/details/72540075?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

