---
layout:     post
title:      《http图解》读后感
date:       2016-11-29
tags:
    - Others
---	

读了《http图解》想到了去年面试的时候，面试官问过我一个问题：url输入浏览器到页面呈现给我们，中间发生了什么？当时听到这个问题的时候脑子里空空如也~~如今回想起来，如果面试官如果再次问起，我会怎样回答呢？
Now,我会给出我自己的理解：

    1、url输入到浏览器，负责域名解析的DNS服务会通过域名查找对应的IP地址（也就是获得url对应的ip地址）；
    2、利用TCP/IP协议族进行网络通信，发送数据包，建立网络连接。客户端（浏览器）会向服务器端发送请求，服务端会响应客户端的请求。
    其中，客户端（浏览器）向服务器端发送请求，发送端会经历应用层（http报文）->传输层（增加TCP首部）->网络层（IP数据包，增加IP首部）->数据链路层（增加以太网首部）；服务端则相反。
    3、客户端渲染，渲染引擎对html进行转换，转化成能够被DOM处理的形式，接着转换成一个dom树，在解析html的过程，会发送请求把对应的内容获取到，同时进行css的解析，构建出css样式规则应用到dom树上，然后进行一定的布局处理，最后根据这棵渲染树在浏览器窗口中进行绘制。

以下这张图（http图解中的）可以诠释1、2过程：

![](http://7xnl4q.com1.z0.glb.clouddn.com/http.jpeg)

## http报文
![](http://7xnl4q.com1.z0.glb.clouddn.com/http1.jpeg)
![](http://7xnl4q.com1.z0.glb.clouddn.com/http2.jpeg)
![](http://7xnl4q.com1.z0.glb.clouddn.com/http3.jpeg)
![](http://7xnl4q.com1.z0.glb.clouddn.com/http4.jpeg)

