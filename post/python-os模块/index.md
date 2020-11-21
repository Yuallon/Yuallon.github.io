
### 前言：

**OS模块** 提供了一个便捷的方法来使用操作系统所以依赖的函数。

- open() 函数，可以实现文件的读写功能
- os.path() 函数，可以实现对文件路径的操作
- fileinput 模块，可以实现文件在命令行上的读取
- tempfile 模块，可以实现创建临时的文件或文件夹
- 对文件或文件夹更高层次的操作，可以使用shutil 模块

**Note：在OS模块中，错误类型为 OSError。**



### open()函数

**完整语法格式：**

```
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```

**参数说明：**

- **file，必须参数。文件路径（相对路径 or 绝对路径）**
- **mode，可选参数，接受string类型。文件的打开方式**
  - "r"：默认，只读模式。指针放在文件开头
  - "w"：打开一个文件只用于写入。如果文件存在，则删除原有内容从头开始编辑。如果文件不存在，则创建新文件。
  - "x"：写入模式，新建一个文件。如果该文件存在，则报错。
  - "a"：append，打开一个文件用于追加内容。如果该文件存在，文件指针将会移到文件结尾，新添加的内容从已有的内容末尾开始添加。如果文件不存在，新建文件。
  - "b"：以二进制模式读取文件内容。
  - "t"：文本模式，默认。
  - "+"：打开一个文件进行更新（可读可写）。
  - "r+"：打开一个文件用于读写。
  - "rb"：以二进制格式打开一个文件用于只读。指针放在文件开头。一般用于非文本文件，如图片等。
  - "rb+"：以二进制格式打开一个文件用于只读写。指针放在文件开头。一般用于非文本文件，如图片等。
  - "w+"：打开一个文件用于读写。如果该文件已存在，则打开文件，并从头开始编辑，即原有内容会被删除。如果文件不存在，则创建一个新文件。
  - "wb"：以二进制格式打开一个文件用于写入。如果该文件已存在，则打开文件，并从头开始编辑，即原有内容会被删除。如果文件不存在，则创建一个新文件。一般用于非文本文件，如图片。
  - "wb+"：以二进制格式打开一个文件用于读写。如果该文件已存在，则打开文件，并从头开始编辑，即原有内容会被删除。如果文件不存在，则创建一个新文件。一般用于非文本文件，如图片。
  - "a+"：append，打开一个文件用于读写。如果该文件存在，文件指针将会移到文件结尾，新添加的内容从已有的内容末尾开始添加。如果文件不存在，新建文件。
  - "ab"：append，以二进制格式打开一个文件用于追加内容。如果该文件存在，文件指针将会移到文件结尾，新添加的内容从已有的内容末尾开始添加。如果文件不存在，新建文件。
  - "ab+"：append，以二进制格式打开一个文件用于追加内容。如果该文件存在，文件指针将会移到文件结尾，新添加的内容从已有的内容末尾开始添加。如果文件不存在，新建文件。
- buffering：设置缓冲
- **encoding，设置编码格式，一般用utf8**
- error：报错级别
- newline：区分换行符
- closefd：传入的file参数类型
- opener

```
with open("test.txt",'r',encoding='utf8') as f:
	print(f.read())
```



#### file对象

通过open函数，可以打开或创建文件，并返回一个file对象。下面列出file对象的常用函数。

- **file.close()**：关闭文件。文件打开提取文件内容后，一定要关闭文件。
- file.read(size)：size是指定读取的字节数，如果没有给定size值，读取文件的全部内容。
- file.readline(size)：读取整行，包括换行符\n。
- **file.readlines()**：**读取全部内容，并以列表形式返回。**
- **file.write(str)**：将str数据写入文件。
- file.tell()：返回文件指针所在位置。

注：加黑的三个参数是最常用的，其他参数的详细解释参考[open_function](https://docs.python.org/3/library/functions.html#open)。文件打开，一定要在最后关闭文件。



### os.path模块

该模块用于操作文件路径。路径参数可以是string或bytes，返回的对象类型与传入的类型保持一致。不过建议使用string。

- **os.path.abspath(path)**：返回绝对路径

  ```
  pwd
  '/Users/huangyulong/Desktop'
  os.path.abspath('aaaa.txt')
  '/Users/huangyulong/Desktop/aaaa.txt'
  ```

- **os.path.basename(path)**：返回文件名

  ```
  os.path.basename('/Users/huangyulong/Desktop/aaaa.txt')
  'aaaa.txt'
  ```

- **os.path.dirname(path)**：返回所在文件夹路径

  ```
  os.path.dirname('/Users/huangyulong/Desktop/aaaa.txt')
  '/Users/huangyulong/Desktop'
  ```

- **os.path.split(path)**：把路径分隔为 dirname 和 basename，返回一个元组

  ```
  os.path.split('/Users/huangyulong/Desktop/aaaa.txt')
  ('/Users/huangyulong/Desktop', 'aaaa.txt')
  ```

- **os.path.splitext(path)**：分隔路径，返回路径名和文件扩展名

  ```
  os.path.splitext('/Users/huangyulong/Desktop/aaaa.txt')
  ('/Users/huangyulong/Desktop/aaaa', '.txt')
  ```

- **os.path.exists(path)**：检查路径是否存在，存在返回True，不存在返回False。

- **os.path.getatime(path)**：返回最近访问时间（浮点型数秒）

- **os.path.getmtime(path)**：返回文件最近修改的时间

- **os.path.getctime(path)**：返回文件路径创建时间

- **os.path.getsize(path)**：返回文件大小，如果路径不存在则报错

- **os.path.isfile(path)**：判断路径是否为文件

- **os.path.isdir(path)**：判断路径是否为目录

- **os.path.islink(path)**：判断路径是否为链接

- **os.path.join(path1, *paths)**：把一个或多个path参数拼接，返回一个路径名

  - 除了最后一个path参数，其他要求非空
  - 如果最后一个path是空，则返回的路径把其转换成\
  - 如果有一个path参数是绝对路径，则在它之前的所有path参数都会被舍弃。

  ```
  os.path.join('/Users','huangyulong','Desktop/test.py','')
  '/Users/huangyulong/Desktop/test.py/'
  
  os.path.join('/Users','/Desktop/test.py','huangyulong')
  '/Desktop/test.py/huangyulong'
  ```

  

- **os.path.samefile(path1, path2)**：判断目录或文件是否相同

- **os.path.sameopenfile(fp1, fp2)**：判断fp1 和 fp2 是否指向同一文件

#### Reference:

1. [os.path](https://docs.python.org/3/library/os.path.html#module-os.path)
2. [Python os.path() 模块](https://www.runoob.com/python/python-os-path.html)



### 常用OS函数

- **os.name**：返回操作系统类型，Windows是'nt'，Linux/Mac（Unix）是'posix'。

- **os.getcwd()**：返回python当前工作路径，string类型

- **os.listdir(path='.')**：返回当前路径下所有文件的名字，返回列表类型。

- **os.access(path, mode)**：检查文件的权限。

  - os.F_OK 作为mode参数，测试path是否存在
  - os.R_OK 作为mode参数，测试path是否可读
  - os.W_OK 作为mode参数，测试path是否可写
  - os.X_OK 作为mode参数，测试path是否可执行

  ```
  import os, sys
  
  result = os.access("/tmp/foo.txt", os.F_OK)
  print("F_OK - 返回值%s" % result)
  ```

- **os.chmod(path, mode)**：用于更改文件或目录的权限

  - path -- 文件或目录路径
  - flags -- 可用以下选项按位或操作生成， 目录的读权限表示可以获取目录里文件名列表， ，执行权限表示可以把工作目录切换到此目录 ，删除添加目录里的文件必须同时有写和执行权限 ，文件权限以用户id->组id->其它顺序检验,最先匹配的允许或禁止权限被应用。
    - **stat.S_IXOTH:** 其他用户有执行权0o001
    - **stat.S_IWOTH:** 其他用户有写权限0o002
    - **stat.S_IROTH:** 其他用户有读权限0o004
    - **stat.S_IRWXO:** 其他用户有全部权限(权限掩码)0o007
    - **stat.S_IXGRP:** 组用户有执行权限0o010
    - **stat.S_IWGRP:** 组用户有写权限0o020
    - **stat.S_IRGRP:** 组用户有读权限0o040
    - **stat.S_IRWXG:** 组用户有全部权限(权限掩码)0o070
    - **stat.S_IXUSR:** 拥有者具有执行权限0o100
    - **stat.S_IWUSR:** 拥有者具有写权限0o200
    - **stat.S_IRUSR:** 拥有者具有读权限0o400
    - **stat.S_IRWXU:** 拥有者有全部权限(权限掩码)0o700
    - **stat.S_ISVTX:** 目录里文件目录只有拥有者才可删除更改0o1000
    - **stat.S_ISGID:** 执行此文件其进程有效组为文件所在组0o2000
    - **stat.S_ISUID:** 执行此文件其进程有效用户为文件所有者0o4000
    - **stat.S_IREAD:** windows下设为只读
    - **stat.S_IWRITE:** windows下取消只读

- **os.mkdir(path)**：创建文件夹（目录），如果目录已存在，FileExistsError。

- **os.remove(path)**：移除文件，如果指定的路径是个目录，OSError

- **os.rmdir(path)**：移除文件夹（目录）

- **os.rename(old, new)**：重命名

- **os.renames(old, new)**：重命名，与rename类型，不过这个用于递归操作

- **os.chdir(path)**：改变python工作目录到path

- **os.link(src, dst)**：用于创建硬连接，src--用于创建硬连接的源地址；dst--用于创建硬连接的目标地址。*该方法对用于创建一个已存在文件的拷贝非常有用。*

- **os.unlink(path)**：用于删除文件，如果文件是一个目录，则报错。



### Reference

1. [OS模块](https://docs.python.org/3/library/os.html#os-file-dir)
2. [Python3 OS 文件/目录方法](https://www.runoob.com/python3/python3-os-file-methods.html)

