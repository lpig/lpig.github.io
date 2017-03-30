---
layout: post
title:  "RESTful学习及理解笔记"
date:	2017-03-30  17:42
tags:
  - 后端
---




写了很久的API也没怎么去了解RESTful的理念，于是就去翻了各种文档和解析，这里记录下自己看到的以及理解的部分。

REST的全称是Representational State Transfer，直接翻译的话是‘表述性状态转移’，直接看上去的话很难理解，其实它真正要表达的意思是对资源的创建、删除和更改的操作。简单来表达的话就是客户端可以通过HTTP请求来直接操作资源的各种状态。目前公认的描述形式是一个URL就是对应一种资源。

举一个例子：我们在服务端有一个文章的资源，那么这个文章的链接就有可能是api.lpig.com/article/{id}/,id的参数代表不同文章的id,当我们的客户端要对这资源做操作的话就可以通过下面的方法：
```
GET：api.lpig.com/article/{id}/ （获取资源）
POST：api.lpig.com/article/ （创建资源）
PUT：api.lpig.com/article/{id}/ （更新、创建资源）
PATCH：api.lpig.com/article/{id}/ （更新资源）
DELETE：api.lpig.com/article/{id}/ （删除资源）
```

上面可以看到POST和PUT有创建资源的目的，不过PUT更多的时候都是用来更新对象，或者创建一个已知的资源，而POST方法更多是用来创建新的未知的资源，简单来说使用PUT方法多次提交相同数据的话最终的结果都是相同的，而使用POST方法多次提交相同数据最后会生成相应数量的资源。所以PUT更多是用于更新资源，PATCH是后来提出用来补充PUT方法的，它的作用是可以更新资源的部分属性而不是相对PUT一样要提供资源的全部属性。
![REST API Design][1]


####REST具体是什么？
下面的准则定义了REST系统的具体特征：

 - 客户-服务器（Client-Server），提供服务的服务器和使用服务的客户需要被隔离对待。
 - 无状态（Stateless），来自客户的每一个请求必须包含服务器处理该请求所需的所有信息。换句话说，服务器端不能存储来自某个客户的某个请求中的信息，并在该客户的其他请求中使用。
 - 可缓存（Cachable），服务器必须让客户知道请求是否可以被缓存。（Ross：更详细解释请参考 [理解本真的REST架构风格][2] 以及    [StackOverflow的这个问题][3] 中对缓存的解释。）
 - 分层系统（Layered System），服务器和客户之间的通信必须被这样标准化：允许服务器和客户之间的中间层（Ross：代理，网关等）可以代替服务器对客户的请求进行回应，而且这些对客户来说不需要特别支持。
 - 统一接口（Uniform    Interface），客户和服务器之间通信的方法必须是统一化的。（Ross：GET,POST,PUT.DELETE, etc）
 - 支持按需代码（Code-On-Demand，可选），服务器可以提供一些代码或者脚本（Ross：Javascrpt，flash，etc）并在客户的运行环境中执行。这条准则是这些准则中唯一不必必须满足的一条。（Ross：比如客户可以在客户端下载脚本生成密码访问服务器。）


无状态和有状态的区别就是当前的请求是否需要依赖上一个请求，如果不需要就是无状态，否则就是有状态。
![image_1bcf2kajk1lot1a5q1nc713mq108c13.png-59.2kB][4]
![image_1bcf2lh1kbcra5fodu1vmk1m381g.png-69.6kB][5]


####总结
REST的出现充分体现了客户端和服务端分离的场景，并且对不同客户端也有了更好的支持（不同客户端只要提交固定格式的数据就能操作资源），无需关心服务端是什么环境以及语言，对比与RPC模式的话可以更好的利用Http协议（RPC模式可以基于Http协议）。

![image_1bcf9b3aij5r196m1crt1gbs10om1t.png-65.8kB][6]
![image_1bcf9bkun16dnsn6r8tdjv12842a.png-51.8kB][7]


  [1]: http://static.zybuluo.com/l404864087/9qwem4xtg5t1e1wa8u402ic0/7405939b62a73f28846533de08db3a80_r.jpg
  [2]: http://www.infoq.com/cn/articles/understanding-restful-style
  [3]: http://stackoverflow.com/questions/20988051/what-is-cacheable-communications-protocol
  [4]: http://static.zybuluo.com/l404864087/2gxz4l54lokwnaciuv1pn7cg/image_1bcf2kajk1lot1a5q1nc713mq108c13.png
  [5]: http://static.zybuluo.com/l404864087/l21k6kednjs40zih4644viwp/image_1bcf2lh1kbcra5fodu1vmk1m381g.png
  [6]: http://static.zybuluo.com/l404864087/g455dvnb3tzjoknq6adintro/image_1bcf9b3aij5r196m1crt1gbs10om1t.png
  [7]: http://static.zybuluo.com/l404864087/gm7qkgtxak5ofyva64lg0xe3/image_1bcf9bkun16dnsn6r8tdjv12842a.png
