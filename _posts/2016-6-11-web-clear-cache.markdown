---
layout:     post
title:      web静态资源缓存自动更新
date:       2016-6-11
tags:
    - Others
---	

核心：

    在每次发布之前，利用Gulp对所有的静态资源进行预处理，重命名为原文件名 + 文件MD5值 + 文件后缀名的形式。比如register.js重命名为register-87f3f22ee7.js

步骤：

    1、先用npm下载gulp-clean  gulp-rev  gulp-rev-collector这几个依赖，其次配置好gulpfile.js里面的内容（已配置好），有兴趣可去项目根目录里面查看；
    2、如果第一步已经完成，如果你只是修改了www端得css或者ts，依次执行gulp www-clean( 取决于你gulpfile.js里面的配置) 、gulp ，然后在你配置的相关文件里面就会生成对应的rev-manifest.json（路径：public/assets/rev/css/和public/assets/rev/js/），如下图所示
   
![http://7xnl4q.com1.z0.glb.clouddn.com/cache1.png](http://7xnl4q.com1.z0.glb.clouddn.com/cache1.png)
![http://7xnl4q.com1.z0.glb.clouddn.com/cache2.png](http://7xnl4q.com1.z0.glb.clouddn.com/cache2.png)
 
    3、到这里对应css名称就会发生对应的变化
    但是js没有，为什么呢？？？？？？ 因为我们项目里面用的是require模块加载，在每个html里面都是require对应的js，而不是普通的<script src=""></script>。
    在网上找了一些相关资料，有两种还凑合：
    (1)在require.congfig配置里面加上 urlArgs: "bust=" +  (new Date()).getTime()，但这只适合开发环境
    (2)在每次发布的时候需要根据rev-manifest在require.congfig对模块进行mapping，将配置文件以内联JS的形式写入到模版页面里面，类似于：

![http://7xnl4q.com1.z0.glb.clouddn.com/cache3.png](http://7xnl4q.com1.z0.glb.clouddn.com/cache3.png)
    

    看起来有点麻烦哈，因为每次修改完js或者pull代码获得更新的js，rev-manifest.json里面对应的js名称后的一串字符会自动变化，但是require.congfig里面需要我们手动去改变，这需要我们细心啊啊啊啊啊！！！！