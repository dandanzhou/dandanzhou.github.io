---
layout:     post
title:      webpack打包工具
date:       2016-8-4
tags:
    - Others
---	

最近在webpack上折腾了几天，终于有了眉目，差点就要放弃了，折腾的过程中最大的收获就是：掌握了学习新东西的方法～～
	
## 折腾的第一点:下载webpack
最开始全局下载webpack,也就是npm install -g webpack比较顺利，但是后来在根目录下npm install webpack，一直报错如下：

![http://7xnl4q.com1.z0.glb.clouddn.com/webpack1.jpg](http://7xnl4q.com1.z0.glb.clouddn.com/webpack1.jpg)

最关键的是我在别人电脑上一安装就成了－－
在网上查了各种解决方案，但最终都木有解决问题，后来突然想到了之前装gulp的时候，每次装到gulp-sass时会出现问题（后来直接把以前好的gulp－sass复制了过来）；
于是我决定把根目录下的node_modules全删了，重新安装，当安装到gulp－sass,同样出现了问题，在网上找到了一个解决方案，直接执行：npm install rebulid,终于成功安装了gulp;
接着在根目录下安装webpack时，成功了！！！

## 折腾的第二点：webpack的配置文件及运行

为了实际演示，我在目前的项目中，用webpack打包了ts文件如下：

![http://7xnl4q.com1.z0.glb.clouddn.com/webpack2.png](http://7xnl4q.com1.z0.glb.clouddn.com/webpack2.png)

在做好配置后，运行webpack,也出现了问题，原因是在根目录下没有下载ts-loader,后来才知道，每一种模块对应的loader都应该先下载（只要配置中有就要下载）	



目前，只是webpack有了一个大概的了解和大概的实际操作，还需我继续去探索～～
   
