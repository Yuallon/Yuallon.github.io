
### Mysql安装

关于Mysql的安装，可以去[官方网站](https://www.mysql.com/downloads/)下载DMG文件，一路点到底就好了。在这里我推荐参照这篇安装教程[Mac电脑安装及终端命令使用mysql](https://blog.csdn.net/potato512/article/details/78564106?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param)。算是对于初学者很友好的教程了。

### Mysql重置密码

我下载的是DMG文件，一路AGREE以后，很容易忘记Mysql安装时的初始密码（初始密码也很乱，不方便记忆）。下面的这篇教程是介绍，如何使用终端命令来重置Mysql的密码。

#### 首先，停止Mysql程序

我的Mac电脑上是：“系统便好设置” --> Mysql  --> "Stop Mysql Server"

#### 打开终端输入：

以安全模式启动Mysql

```
sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
```

#### 打开另一个终端，输入：



```
sudo /usr/local/mysql/bin/mysql -u root（需要输入的密码为用户的开机密码）

UPDATE mysql.user SET authentication_string=PASSWORD('你的新密码') WHERE User='root';（重置密码）

FLUSH PRIVILEGES;（刷新）

exit;（退出）
```

#### 重启Mysql，完成

### 参考

- [重置mysql的root密码最简单的方法](https://www.jb51.net/article/182063.htm)
- [Mac电脑安装及终端命令使用mysql](https://blog.csdn.net/potato512/article/details/78564106?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param)

