---
layout: post
title:  "django用使用ETag和Last-Modified"
date:	2018-04-07  11:08
tags:
  - django
---

##django用使用ETag和Last-Modified

在http请求中为了减少请求时间以及减少服务器的压力一般情况下都会采用浏览器缓存、CDN、服务器缓存已经ETag和Last-Modified的方案，现在记录一下在django直接使用ETag和Last-Modified的方法。

只需要在settings里面添加

    USE_ETAGS = True

以及在中间件的设置里添加
```python
MIDDLEWARE_CLASSES = (
    ...
    'django.middleware.http.ConditionalGetMiddleware',
    ...
)
```

就会在http请求里返回ETag和Last-Modified了（一般情况下返回ETag时不需要返回Last-Modified）,那么服务端接收到ETag后并检查发现数据没有更新就会返回304状态码告知客户端数据没有更新，从而减少服务端重复查询数据的压力。
