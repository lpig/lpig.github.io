---
layout: post
title:  "oauth2 学习记录"
date:  2016-09-02  16:00
tags:
  - oauth
  - 后端
---


使用场景:


    1:第三方登录
    2:第三方授权获取信息


oauth思路:

OAuth在"客户端"与"服务提供商"之间，设置了一个授权层（authorization layer）。"客户端"不能直接登录"服务提供商"，只能登录授权层，以此将用户与客户端区分开来。"客户端"登录授权层所用的令牌（token），与用户的密码不同。用户可以在登录的时候，指定授权层令牌的权限范围和有效期。
"客户端"登录授权层以后，"服务提供商"根据令牌的权限范围和有效期，向"客户端"开放用户储存的资料


oauth授权模式:

oauth2的授权模式分为以下四种：

 1. 授权码模式（authorization code）
 2. 简化模式（implicit）
 3. 密码模式（resource owner password credentials）
 4. 客户端模式（client credentials）

授权码模式和简化模式其实具体内容是一样的，都是通过key和secret向oauth服务器获取token的，只是简化模式不需要执行获取code的那一步，而是直接获得token。

密码模式是需要用户提交用户本身的账户密码，然后客户端再用用户的账户密码去向oauth服务器获取token。

客户端模式的话是直接在客户端上以客户端而不是用户的名义向oauth服务器获取token，严格来说这一步并不归属于oauth的协议里面。


授权流程图：



```seq
用户->客户端:打开
客户端-->用户:重定向
用户->oauth服务器:
oauth服务器-->oauth服务器:校验key、secret、域名
oauth服务器-->用户:重定向（带授权code）
用户->客户端:
客户端-->客户端:加密信息
客户端->oauth服务器:获取token
oauth服务器-->oauth服务器:校验
oauth服务器->客户端:返回token
```

```seq

```

小纪:

openid和oauth区别:

openid和oauth顺然都可以代表某个用户的信息，openid关注的是**用户是谁**，而oauth关注的是**用户能做什么**，一个比喻就是，openid等于一个人的身份证而oauth是代表一个人家里的门钥匙。

