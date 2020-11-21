
###前言：

虽然自己很早以前就注册了GitHub账号，最近因为看着教程搭建了个人blog，才频繁接触到git一些命令。而且，管理好自己的GitHub的repositories也是一个很好的习惯。所以，今天看了一些有关GitHub and git命令的教学视频，记录一下自己的学习。

###创建repository

在GitHub个人主页，点击个人头像，点击**Your repositories**即可创建一个仓库。在平时的天文数据处理中，我希望自己写的一些代码托管到GitHub上，所以很希望可以熟练使用git命令。

今天的git学习视频来自：[【教程】学会Git玩转Github【全】](https://www.bilibili.com/video/BV1Xx411m7kn?p=9)，其中对自己帮助最大的是**P8 & P9**两个视频。这两个视频主要讲解了**如何使用git命令创建仓库，并同步到GitHub上**。也让自己对前面搭建个人blog时，遇到的一些git命令有了深刻的理解。

![Git工作区域](/git1.png)

![Git文件添加流程](/git2.png)

**git命令**

```
#将当前目录转换为git仓库
git init
#查看当前文件的状况，是在工作区域还是在暂存区or仓库
git status
#添加文件
git add xxx.py
#添加当前文件夹所有的文件
git add .
#备注
git commit -m "内容"
#将本地文件同步到GitHub上
git push -u origin master
```

###问题&解决方式

当我在本地创建了一个新的git仓库，在把仓库推送到GitHub上时，出现下面的问题

![远程库与本地库不一致](/git_error1.png)

解决方式参考：[git push错误failed to push some refs to的解决](https://blog.csdn.net/MBuger/article/details/70197532?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)

根据文章的解释，我这个问题的出现是因为我在GitHub远程仓库中新添加了README文件，但是这个文件没有同步到本地的git仓库，这时候当运行**push**命令是就会出现这个报错。

**问题总结：** 当我们在github版本库中发现一个问题后，你在github上对它进行了在线的修改；或者你直接在github上的某个库中添加readme文件或者其他什么文件，但是没有对本地库进行同步。这个时候当你再次有commit想要从本地库提交到远程的github库中时就会出现push失败的问题。

**解决方式：**

```
git pull --rebase origin master
```

上述命令是把远程库同步到本地库。**--rebase**的作用是取消本地库中刚刚的commit，并把他们接到更新后的版本库之中。

**注意：此处使用的是master分支，请根据自己的开发分支更换**

**图例解释：**

![Git_push1](/git_push1.png)

git pull --rebase origin master意为先取消commit记录，并且把它们临时 保存为补丁(patch)(这些补丁放到".git/rebase"目录中)，之后同步远程库到本地，最后合并补丁到本地库之中。

![Git_push1](/git_push2.png)

接下来就可以把本地库push到远程库当中了。

![Git_push1](/git_push3.png)



