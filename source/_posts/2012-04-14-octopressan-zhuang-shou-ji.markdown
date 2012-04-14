---
layout: post
title: "Octopress安装手记"
date: 2012-04-14 16:55
comments: true
categories: [github, Octopress]
---

# 前言
本来我是想主攻**底层操作系统方向**和**嵌入式软件设计**，理应和WEB没什么关系，但是前几天**Maplist**大神准许我加入去维护一个MAC服务器，要我们去尝试在服务器上搭博客玩，于是就手痒找资料。

刚开始就在SAE（Sina App Engine）上面搭了个WordPress的博客*[Nerd?Zonyitoo](nerdzonyitoo.sinaapp.com)*，过程毫无技术含量，基本上就是点几下博客就出来了，毫无成就感。

再接着就是强大的师弟**LPY**告诉我*[github](github.com)*上面可以搭博客，于是趁今天有点空就去找了一下资料，发现过程同样简单！

# 在github在建一个博客
## 当然首先要有个[github.com](http://github.com)的帐号
* 先登上github.com申请一个免费的帐号
* 然后在个人主页右下方点`New repository`
* 然后它会教你怎么把一个*HelloWorld*项目上传到那个repositoriy上去，基本上就是如下步骤:

        $ mkdir ~/Hello-World
        $ cd ~/Hello-World
        $ git init
        Initialized empty Git repository in /Users/your_name_directory/Hello-World/.git/
        $ touch README
        # 下面开始Commit
        $ git add README
        $ git commit -m 'first commit'
        # 上面这两句就是要把改变的文件记录到git里去
        # 然后上传
        $ git remote add origin git@github.com:username/Hello-World.git
        $ git push -u origin master
        
    这个时候打开你的Repository应该就能看到已经上传了的**README**

* 这时已经学会了简单的git操作技巧，那么就可以开始搭博客了。
首先要得到SSH Public Keys
        
        $ ssh-keygen -t rsa -C "your_email@youremail.com"
        
然后在`~/.ssh/`下面会看见一个叫`id_rsa.pub`的文件，用VIM或GEdit打开，把里面的东西拷到github网站里："Account Settings" >> "SSH Public Keys" >> "Add another public key"，都复制到那个框内。
> PS：如果是第一次的话很容易就会忽略右上角那个**Add another public key**，这时应该认真读一下[github help](http://help.github.com/ssh-key-passphrases/)

* 然后，就要建一个github pages。就是创建一个新的Repository，如果你的博客名是http://yourname.github.com，那么Repository的_project name_就**必须**是yourname.github.com
* 接下来可以看一下github的help页面中[关于如何搭建一个github pages](http://help.github.com/pages/)的教程，可以简单地上传一个index.html即可！但是这太简单了...
* 不过，如果你现在已经按照help页面的方法做了的话，那么访问http://yourname.github.com就应该会看到一个大大的**Hello!!**
* 那么，大功告成_^

不过，我们是不会简单地满足于只有一个index.html页面的，反正本人是比较懒，不想自己去写一个博客网站，那太费力了，那么采用现成的博客系统就是最好的选择，现成的话我知道的比较好用的有两个：WordPress和Octopress，而Github在这两者之中只支持Octopress = =

# 为什么要用Octopress?
其实，这个我不就不用多说了，为什么不直接去[Octopress的官网](http://octopress.org)看一看呢

# 安装Ruby
Octopress是用Ruby写的系统，所以要用它那必须得先在自己电脑上装Ruby，安装其实很简单，一般的Linux发行版的包管理器中都会有Ruby，Ubuntu中则是：

####用包管理器安装**Ruby 1.9.2**
        
    # apt-get install ruby-1.9.1
        

要注意的是，这里必须是要装**Ruby 1.9.2**，但为什么命令里是1.9.1？我也不知道，apt-get里面显示最新版就只有1.9.1但是装完后用`ruby -v`查看的话会显示`ruby 1.9.2p290 (2011-07-09 revision 32553) [x86_64-linux]`
> PS: 千万不要图省事直接`apt-get install ruby`，这样装完之后会陷入无尽的纠结之中（若你没有学过Ruby，我就是），因为它默认装的是1.8.x的版本，这是不能运行**Octopress**的！

#安装Octopress
* 获取octopress，直接执行
        
        $ git clone git://github.com/imathis/octopress.git yourblogfolder

* `gem install bundler`
* `bundle install`
* `rake install`    这一步是装默认主题

至此，Octopress已经安装完毕，可以开始写日志了

#激动人心的一步，写日志！
* 在你的博客根目录处，执行`rake new_post["my first blog"]，然后你会发现在/source/_post/下会生成一个.markdown文件，这时你就可以拿它来写日志了，写好了日志然后保存回去
* 完成之后执行`rake generate`，生成
* 执行`rake preview`可以在浏览器[这个地址](http://127.0.0.1:4000)进行预览
* 最后执行`rake deploy`，将日志提交到github上，完成！

#补充一些
在第一次同步之前，要先执行
    
    rake setup_github_pages
    
设定github发布，然后要填入你的Git URL，就是你的Respository页里面的SSH同步地址，格式如：`git@github.com:yourname/yourname.github.com.git`

#小结
这就是我这一个晚上研究的成果，终于成功搭了一个博客，虽然自己再回去看感觉其实过程也是很简单的，都是一些操作而没有要研究的东西，只是因为是第一次很多都是摸着石头过河，没有Ruby基础是关键！

下一篇就来聊聊怎么配置Octopress，我还在学习中

#学习参考:
* [github.com](github.com)
* [我是清都山水郎的博文](http://hopes4.me/blog/introduce-octopress-on-github/)
* [图灵社区Markdown语法](http://www.ituring.com.cn/article/details/775)
