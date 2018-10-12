---
layout: post
title:  "docker的简单使用说明"
date:  2016-01-06  16:14
tags:
  - docker
  - note
---

最近发现docker开始火了起来..它的移植性以及轻量级的虚拟化技术吸引了我，下面就记录一下我在接触docker时的一些笔记。

docker是一个基于go语言的一个开源项目，其主要提供的是实现轻量级的操作系统虚拟化方案。因为docker是基于linux内核进行封装，所以它只能对linux系统进行虚拟化。

![此处输入图片的描述][1]
![此处输入图片的描述][2]
从上面的两个图我们可以看到传统的VM技术是对物理层进行虚拟化然后还要为其安装一个新的操作系统，而docker是直接复用本地的操作系统试下系统层的虚拟化。

####好了，那么我们为什么要选择docker呢？
对于要管理以及部署多个服务器的运维和开发人员来说希望的是可以通过一次的创建部署好服务器的环境之后就能很方便以及移植到别的服务器上，很大的减少了每次都要重新部署服务器的时间。
而且使用docker的话有非常好的可移植性，它可以在各种平台上运行，可以很方便的把一个容器直接搬迁到别的地方。
虽然在分布式集群上docker还没有很好的表现，不过对于不同项目用不同的系统环境以及要同一开发环境的话docker是一个非常不错的选择。

#docker安装
在window和mac下安装docker是非常简单的，只需要在官网上下载安装包，然后就是熟悉的下一步大法了。

linux的话会麻烦一点，以下是ubuntu的安装过程：

 1. 安装docker需要用到wget的命令， 可以通过`which wget`来查看，
 2. 如果没有安装可以wget，就先升级包管理器然后再安装，命令如下：
 3. `sudo apt-get update`升级包管理器
 4. `sudo apt-get wget`安装wget命令
 5. `wget -q0- https://get.docker.com/ sh`获取docker安装包，

上面的命令会提示需要输入sudo密码，全部结束之后就可以安装好docker了。

如果要验证docker是否安装成功的话可以通过以下命令进行检查：
`sudo docker run hello-world`
*这个命令会下载一个测试用的镜像，并且在容器中运行这个镜像。

#开始使用docker
在使用docker之前要先明确三个名词，镜像、容器、仓库。
镜像简单来解释的话就是类似windown的镜像一样里面包含了系统还有各种软件以及集成环境。
容器的话就是用来运行镜像的一个工具也就类似传统vm的虚拟机一样。
仓库的话就是保存各种镜像的地方，有官方的镜像也有用户自己开发以及修改过的第三方镜像，类似于git的仓库。现在国内的话已经有很多第三方的仓库给用户上传以及下载不同的镜像，docker的官方仓库叫做[docker hub][3]，不过鉴于各种原因，有时候需要代理才可以连接上。

####接下来就大概的说一下docker的简单使用
*以下操作均为mac系统下操作

mac或者windows上使用docker的话要先安装一个linux的虚拟机，因为docker是基于linux系统命令进行虚拟化，所以mac和windows用户在使用docker的时候就要先多走一步了。

不过在使用官方的安装包的时候，他会自动帮你把所有的环境搭建好，同时会装上VirtualBox和docker-machine的工具，docker-machine是一个简化docker安装的命令行工具，通过一个简单的命令安装他可以在对应的不同平台上安装docker，如：VirtualBox、 Digital Ocean、Microsoft Azure。[github地址][4]

因为我之前一直安装好了所以可以通过docker-machine ls查看当前存在的docker平台状态。
![此处输入图片的描述][5]

如果没有创建的话也可以通过`docker-machine create -d virtualbox default`命令来创建一个基础的平台。

那么我们现在运行一下这个平台，通过`docker-machine start/restart/stop/rm NAME` 可以控制这个平台的状态。

成功运行了之后会提示一句话说已经为新启动的平台分配了新的ip，使用docker-machine env查看平台信息。
![此处输入图片的描述][6]
![此处输入图片的描述][7]
如此一来，就已经成功启动了一个docker服务。

接着只要使用`docker-machine ssh NAME`就能连接到安装好docker环境的虚拟机平台了。
![此处输入图片的描述][8]

那么在所有东西都准备好的情况之下我们要做什么？没错，就是运行一下输出hello world。
`docker run busybox echo hello world`
这个命令的意思是运行一个叫做busybox的镜像并且输出hello world，但这个镜像不存在本地的时候docker会现在官方的镜像仓库里下载这个镜像，如果存在的话就直接运行。
![镜像不存在本地时自动下载][9]
镜像不存在本地时自动下载

![镜像存在本地时直接执行][10]
镜像存在本地时直接执行

那么怎么查看本地存在的镜像呢？
`docker images`
这个命令会把当前存在的docker镜像安装列表的表示全部显示出来，其中包括了镜像的ID、TAG和创建时间等信息。
![此处输入图片的描述][11]

`docker ps`
而这个命令则是显示当前运行的容器的信息。
![此处输入图片的描述][12]

总的来说如果要运行一个镜像的话可以通过`docker run NAME`来运行一个镜像,然后他会自动创建一个新的容器来运行这个镜像，如果要停止这个容器的话可以通过`docker stop CONTAINER ID`来停止这个容器。

到这里为止docker的基本使用说明已经结束了，希望我这个普通的整理可以有帮助，以后会有以在docke里运行redis服务作为一个例子进行深入的记录。

  [1]: lpig-blog.test.upcdn.net/markdown/2018/10/12/virtualization.png
  [2]: lpig-blog.test.upcdn.net/markdown/2018/10/12/docker.png
  [3]: https://hub.docker.com/
  [4]: https://github.com/docker/machine
  [5]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker machine ls.png
  [6]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-machine-start.png
  [7]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-machine-env.png
  [8]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-machine-ssh.png
  [9]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-run.png
  [10]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-run2.png
  [11]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-images.png
  [12]: lpig-blog.test.upcdn.net/markdown/2018/10/12/dockerdocker-ps.png
