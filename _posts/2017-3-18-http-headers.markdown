---
layout:     post
title:      Http Headers里必须详细了解的
date:       2017-3-18
tags:
    - Others
---	

Http消息头目前大致分为请求头和响应头，具体详细内容可[点击查看](https://itbilu.com/other/relate/EJ3fKUwUx.html)，这里我就详细描述两大点如下：

一、浏览器缓存相关

    1、Cache-Control
        no-cache（并不代表浏览器不缓存，而是在缓存前要向服务器确认资源是否被更改）；
        no-store（绝对禁止缓存）；
        max-age（在max-age这段时间里浏览器就不会再向服务器发送请求了）；
        s-maxage（只用于共享缓存，如CDN缓存，若存在s-maxage，则会覆盖掉max-age和Expires header）；
        public （指定响应会被缓存，并且在多用户间共享）；
        private （响应只作为私有的缓存，不能在用户间共享。如果要求HTTP认证，响应会自动设置为private）
        must-revalidate（指定如果页面是过期的，则去服务器进行获取）。

    2、Expires
        缓存过期时间，用来指定资源到期的时间，在响应请求头中告诉浏览器在这个时间前浏览器可以直接从它的缓存取数据，而无需再次请求。

    3、Last-modified
        服务器端文件的最后修改时间，需要和cache-control共同使用，是检查服务器端资源是否更新的一种方式。当浏览器再次进行请求时，会向服务器传送If-Modified-Since报头，询问Last-Modified时间点之后资源是否被修改过。如果没有修改，则返回码为304，使用缓存；如果修改过，则再次去服务器请求资源，返回码和首次请求相同为200，资源为服务器最新资源。

    4、ETag
        根据实体内容生成一段hash字符串，标识资源的状态，由服务端产生。浏览器会将这串字符串传回服务器，验证资源是否已经修改。它可以解决Last-modified存在的一些问题：精确得到资源的最后修改时间，甚至精确到秒；一些资源的最后修改时间改变了，但是内容没改变，使用ETag就认为资源还是没有修改的。

想进一步理解304[可点击查看](http://www.cnblogs.com/ziyunfei/archive/2012/11/17/2772729.html)

大概流程图如下：   
![](http://www.alloyteam.com/wp-content/uploads/2016/03/%E5%9B%BE%E7%89%8761.png)


二、Keep-Alive模式

我们都知道HTTP协议为无连接的协议，所以每个请求/应答客户和服务器都要新建一个连接，完成之后立即断开。那有什么办法可以避免建立或者重新建立连接呢？

    肯定是有的，那就是使用Keep-Alive模式，即在header里面设置connection:keep-alive。

Keep-Alive模式发送完数据http，服务器不会自动断开连接，那客户端如何判断请求所得到的响应数据已经接收完成（或者说如何知道服务器已经发生完了数据）？

    1、使用Conent-Length，表示实体内容长度，客户端（服务器）可以根据这个值来判断数据是否接收完成；但是如果是动态页面等时，服务器是不可能预先知道内容大小，这时就要看接下来第二条了；

    2、使用Transfer-Encoding，如果一边产生数据，一边发给客户端，服务器就需要使用"Transfer-Encoding: chunked"这样的方式来代替Content-Length。chunk编码将数据分成一块一块的发生。Chunked编码将使用若干个Chunk串连而成，由一个标明长度为0 的chunk标示结束。每个Chunk分为头部和正文两部分，头部内容指定正文的字符总数（十六进制的数字 ）和数量单位（一般不写），正文部分就是指定长度的实际内容，两部分之间用回车换行(CRLF) 隔开。在最后一个长度为0的Chunk中的内容是称为footer的内容，是一些附加的Header信息（通常可以直接忽略


