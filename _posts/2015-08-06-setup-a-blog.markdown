---
layout: post
title:  "关于建立一个独立的个人博客"
date:  2015-08-06  23:53
tags:
  - github
  - self
---

﻿使用 GitHub Pages+jekyll+Strikingly搭建个人博客

需要使用到的工具：

- github （一个在全球很出名的代码管理平台
- jekyll（一个简单的静态博客生成器
- Strikingly（一个一键式网站生成平台，还有域名购买服务（P.S.选用

关于github使用建议先去学习下git的操作，这里推荐[廖雪峰的git教学][1]或者[git官方的教学书git book][2]

了解了git的基本用法之后就可以开始在github上建立一个pages github的项目了,[这里][3]是说明，建立pages github的方法很简单，跟着我下面的步骤基本就可以完成：
![此处输入图片的描述][4]
首先点击右上角的加号然后点击“New repository”
![此处输入图片的描述][5]然后把项目名填写为username.github.io，username填自己的用户名，后面的是默认填写(我这里因为已经有这个项目了所以显示名称重复)。最后点击下面的Create repository的绿色按钮就已经创建完毕了。
现在上传一个简单的html文件命名为index.html的话就可以直接访问username.github.io访问看到效果了。

建立好之后就可以就可以使用jekyll来写博客了，首先推荐在自己的电脑上安装好运行jekyll的环境[点击这里][6]有大概的安装流程，虽然说不在电脑本机安装环境直接编辑好后上传到github上访问自己的域名也能直接查看效果，不过还是推荐在本机调试，这样会更加的方便。

环境安装好（或者不想安装环境（强烈不推荐，除非很了解jekyll框架并且觉得自己不用调试））就可以挑选一个自己喜欢的模板下载使用了，[这里][7]有官方整合的各种挺不错的模板，把模板下载下来之后修改文件夹里面的“_config.yml”文件里面的各种参数变量之后再上传到github就可以看到忙碌之后的效果了。关于jekyll的各项变量的配置以及自定义配置可以查看[这里][8]。

**怎么开始写博客：**
这里先说明一下，jekyll存放博客的文件夹是“_posts”里面，每一个新的博客要有一个独立的名字以及文件，名字的命名规则必须强烈按照“2015-08-04-hello-world.makedown”这样的格式，前面是日期后面是标题名称最后是文件格式，这里我推荐使用makedown的格式来撰写博客，因为md可以直接当作是一个文本文件来编辑而且效果也可以在各种编辑器上面及时可见，[这里][9]可以看到具体的说明可介绍。

写好自己的博客之后可以在文件头上面加上标签以及使用的模板名称以及时间例如：

    ---
    layout: post
    title:  "HelloWorld!!"
    date:  2015-08-04  10:41
    ---

这里说明下layout是这个文件使用的模板的样式名称，title就是博客标题，date就是日期时间还可以添加tags来添加标签。


  [1]: http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/
  [2]: https://git-scm.com/book/zh/v1
  [3]: https://pages.github.com/
  [4]: http://7xkxs2.com1.z0.glb.clouddn.com/add.png
  [5]: http://7xkxs2.com1.z0.glb.clouddn.com/create.png
  [6]: http://jekyllcn.com/docs/installation/
  [7]: http://jekyllthemes.org/
  [8]: http://jekyllcn.com/docs/configuration/
  [9]: http://www.jianshu.com/p/q81RER
