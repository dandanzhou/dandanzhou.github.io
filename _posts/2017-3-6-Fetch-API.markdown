---
layout:     post
title:      Fetch API
date:       2017-3-6
tags:
    - JavaScript
---	

自我从事前端，一直使用XMLHttpRequest(XHR)发送异步请求；直到最近了解到Fetch API，发现它完美基于事件的模型与最近流行的 Promise 和 generator 异步编程模型，然后果断替换掉ajax换这个实用的方法来获取网络资源。

#### 简单示例
    Fetch API中最常用的是fetch()方法，该方法最简单的形式是，接受一个URL参数并返回以一个promise对象
    fetch("/data.json").then(function(res) {
        // res instanceof Response == true.
        if (res.ok) {
            res.json().then(function(data) {
            console.log(data.entries);
            });
        } else {
            console.log("Looks like the response wasn't perfect, got status", res.status);
        }
        }, function(e) {
        console.log("Fetch failed!", e);
    });

    如果是提交一个POST请求，代码如下：
    fetch("http://www.example.org/submit.php", {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded"
        },
        body: "firstName=Nikhil&favColor=blue&password=easytoguess"
        }).then(function(res) {
        if (res.ok) {
            alert("Perfect! Your settings are saved.");
        } else if (res.status == 401) {
            alert("Oops! You are not authorized.");
        }
        }, function(e) {
        alert("Error submitting form!");
    });


#### Fetch引入的3个接口
1、Headers 它可以是键值对，也可以是一个多维数组或JS字面量对象；可以通过has来检索它是否有那个内容。

2、Request 通过构造一个 Request 对象来获取网络资源，构造函数需要 URL、method 和 headers 参数，同时也可以提供请求体（body）、请求模式（mode）、credentials 和 cache hints 等参数。

    var uploadReq = new Request("/uploadImage", {
        method: "POST",
        headers: {
            "Content-Type": "image/png",
        },
        body: "image data"
    });
    mode 参数用来决定是否允许跨域请求，以及哪些 response 属性可读。可选的 mode 值为 "same-origin"（所有的请求遵守同源策略）、"no-cors"（默认，该模式允许来自 CDN 的脚本、其他域的图片和其他一些跨域资源，但是首先有个前提条件，就是请求的 method 只能是HEAD、GET 或 POST。此外，如果 ServiceWorkers 拦截了这些请求，它不能随意添加或者修改除这些之外 Header 属性。第三，JS 不能访问 Response 对象中的任何属性，这确保了跨域时 ServiceWorkers 的安全和隐私信息泄漏问题）以及 "cors"（用于跨域请求）。另外，credentials 属性决定了是否可以跨域访问 cookie 。该属性与 XHR 的withCredentials 标志相同，但是只有三个值，分别是 omit（默认）、same-origin 和 include。

3、Response  fetch() 的回调中获得，有一个 type 属性，它的值可能是 "basic"、"cors"、"default"、"error" 或 "opaque"。

#### 流和克隆
1、注意Request和Response的body只能被读取一次！它们有一个属性叫bodyUsed，读取一次之后设置为true，就不能再读取了。

    var res = new Response("one time use");
        console.log(res.bodyUsed); // false
        res.text().then(function(v) {
        console.log(res.bodyUsed); // true
        });
        console.log(res.bodyUsed); // true

        res.text().catch(function(e) {
        console.log("Tried to read already consumed Response");
    });


2、API提供了一个clone()方法。调用这个方法可以得到一个克隆对象。

    addEventListener('fetch', function(evt) {
        var sheep = new Response("Dolly");
        console.log(sheep.bodyUsed); // false
        var clone = sheep.clone();
        console.log(clone.bodyUsed); // false

        clone.text();
        console.log(sheep.bodyUsed); // false
        console.log(clone.bodyUsed); // true

        evt.respondWith(cache.add(sheep.clone()).then(function(e) {
            return sheep;
        });
    });

不过要记得，clone()必须要在读取之前调用，也就是先clone()再读取。


#### vue + vue-fetch
学习了fetch，立马拿到最近做demo中去应用。
首先，npm install vue-fetch，然后相关代码如下：
![](http://7xnl4q.com1.z0.glb.clouddn.com/fetch-1.png)
![](http://7xnl4q.com1.z0.glb.clouddn.com/fetch-2.png)
![](http://7xnl4q.com1.z0.glb.clouddn.com/fetch-3.png)
![](http://7xnl4q.com1.z0.glb.clouddn.com/fetch-4.png)