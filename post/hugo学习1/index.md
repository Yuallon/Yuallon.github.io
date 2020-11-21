
###前言：

​		搭建个人blog这个想法早在1年前就有了，直到最近这半个月看了一些视频教程and文字教程，才一步一步的搭建好最简单的样式。一开始自己是在bilibili搜索了一些视频教程，帮助最大的是**程序羊**的两个博客搭建视频： [手把手教你从0开始搭建自己的个人博客 |无坑版视频教程| hexo](https://www.bilibili.com/video/BV1Yb411a7ty) 和 [手把手教你从0开始搭建自己的个人博客 |第二种姿势 | hugo](手把手教你从0开始搭建自己的个人博客 |第二种姿势 | hugo)。一开始我是用Hexo搭建，由于Hexo搭建过程中需要做比较多的设置，看了有5遍教程又查找了两三天相关问题稀里糊涂的搭建成功一次，后面再重新搭建就一直没有成功便放弃了。

​		最后还是选取了采用Hugo来搭建自己的blog，虽然一开始也是按照**程序羊**的教程可以一步步搭建起来，我认为这个视频定位就是专门给那些试着搭建blog的小伙伴，看着视频跟着码代码确实可以过一把瘾，但是真正想搭建好一个简洁又能自己平时用的blog-site，这个视频还是过于简单了些。

​		我的目的是想搭建一个真正的个人blog-site，初期阶段可以满足自己上传blog的需求，和一些最简单的配置，这也是自己写此文档的目的。

### Step 1

​		前面跟着**程序羊**Hugo搭建视频教程做了几遍，自己对Hugo搭建的blog的流程已经比较熟悉，在自己搭建blog时主要是跟着 [How to start a blog using Hugo](https://flaviocopes.com/start-blog-with-hugo/) 这个教程一步步搭建起来的。这是一个很详细的文档教程，从如何安装Hugo到最后部署到GitHub and Netlify 讲的很详细。自己最喜欢的部分是如何配置**config.toml** 和 **Deploy the Hugo site to Netlify**。正如作者所讲的那样，一开始配置**config.toml** 时最好不要直接把**theme**中的文件直接复制过去，因为对于像我这样的新手来讲有些参数确实不能理解，如果不能很好配置反倒会影响自己的积极性(前面跟着好多视频做，都没有讲到这一点)，所以我是按照作者的建议配置的简化版的**config.toml**。一且都想预期中的那样顺利。

​		然而，当我按照文档中的方法把blog部署到GitHub上时，一直会出现问题，这个问题目前我还没有弄明白。采用GitHub客户端部署失败，我变想起了**程序羊**Hugo是视频中的方法，结合文档中的搭建新的blog和**程序羊**视频中的终端命令部署，最后我是成功把blog部署到了自己的GitHub上。

​		接下来便是*Deploy*到**Netlify**上，这个过程特别简单，就是在**Netlify**上面新建一个站点，然后把自己的GitHub仓库关联上就行了。这时候我突然意识到，我前面通过GitHub客户端一直没能把blog推到仓库，是不是我选的仓库不是**yuallon.github.io**而是其他类型的仓库的原因呢？

​		到此为止，我已经可以成功的搭建自己的blog-site，并且部署到了GitHub和Netlify上面。此外，每次上传新的blog，我都是通过**程序羊**视频中客户端命令。当你每次把blog推到GitHub上面时，Netlify会自动更新，这点特别棒。

​		[yuallon.github.io](https://yuallon.github.io/)

​		[Netlify-site](https://wizardly-haibt-4f165e.netlify.app/)

​		[My Netlify homepage](https://app.netlify.com/sites/wizardly-haibt-4f165e/overview)

### Step 2

​		虽然按照上面的文字教程可以成功的搭建好自己的blog，也可以很方便的推送自己新写的blog到GitHub正且正常显示，但是我还是很想自己写过的blog都能有一个标签归类，而且上传blog不仅仅是文字，还可以在blog上面插入图片。

​		如何给每一篇blog添加标签，我是参考这个文章[Blog养成记(4) Hugo中增加tags等分类](https://orianna-zzo.github.io/sci-tech/2018-01/blog养成记4-hugo中增加tags等分类/)，同时也让我自己发现一个学习Hugo进阶的参考文章。官方的介绍：[Taxonomies](https://gohugo.io/content-management/taxonomies/#example-front-matter-with-taxonomies)

​		如何在blog里面添加图片，把自己需要添加的图片放到blog的根目录中static文件夹中(/hugoblog(我的Hugo根目录)/static)，然后在**.md**文件中采用markdown格式插入图片的位置处即可(/xxx.png)，注意不要写成(/static/xxx.png)。

### Step 3

​		在上传一些包含Latex数学符号的文档时，Hugo不能正常显示数学公式，我是参考这篇文章解决此问题的：[在Hugo中使用MathJax](https://note.qidong.name/2018/03/hugo-mathjax/)。

​		我的问题事例：

![](/Latex_math_error.png)

我希望数学公式能像图片下面正常显示，可是Hugo的显示是上面的代码结构。

### 结语：

​		现在我可以使用这个很简洁的blog-site来每天写自己的blog了，希望自己后面可以通过慢慢学习逐渐把自己的个人blog修饰的很好看，fighting！

