---
layout:     post
title:      移动web经验总结
date:       2015-11-10 20:07:00
tags:
    - Others
---

## 移动web经验总结

一、头部引用 

    <meta name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1.0; user-scalable=0;" /><!-- 禁止缩放 -->

    <meta http-equiv="Cache-Control" content="no-cache" /><!-- 清浏览器缓存 -->

    <meta content="telephone=no" name="format-detection"><!-- 告诉设备忽略将页面中的数字识别为电话号码 -->

    <meta name="apple-mobile-web-app-capable" content="yes" /><!-- 删除默认的苹果工具栏和菜单栏。 -->

    <meta name="apple-mobile-web-app-status-bar-style" content="black" /><!-- 当启用webapp功能时，控制手机顶部导航栏的颜色，根据实际页面的主题色进行设置 -->

    <meta name="apple-mobile-web-app-capable" contenat="yes" /><!-- 网站开启对web app程序的支持 -->

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> <!-- 优先使用 IE 最新版本和 Chrome -->

    <meta content="email=no" name="format-detection" /><!-- 禁止Android自动识别页面中的邮件地址 -->

    <meta content="description" content="内容不超过150字" /> <!-- 页面描述-->

    <meta name="keywords" content=""/>     <!-- 页面关键词 -->

    <meta name="msapplication-tap-highlight" content="no">   <!-- windows phone 点击无高光 -->

二、整体布局

   慎用flex布局，本人亲测，flex布局在安卓机上不是很管用，详见请点击[说明](http://www.ayqy.net/blog/flexbox%E5%B8%83%E5%B1%80%E7%9A%84%E5%85%BC%E5%AE%B9%E6%80%A7/)；

三、使用html5

  > 1、简洁的 DOCTYPE HTML5 只需一个简洁的文档类型：<!DOCTYPE html>。它有意不使用版本，因此文档将会适用所有版本的HTML。
    2、简单易记的语言标签 你并不需要在 <html> 中使用 xmlns 或 xml:lang 标记。 <html lang=”en”> 将对 HTML5 有效。
    3、简单易记的编码类型 你现在可以在 meta 标签中使用 “charset”：<meta charset=”utf-8″ />
    4、不需要闭合标签 在 HTML5 中，空标签（如：br、img 和 input ）并不需要闭合标签。
    5、新增标签 新增的语义化标签
    
    header:用于表示头部区域;
    hgroup:我们可以使用 hgroup 元素包裹网站标题（h1)和网站副标题（h2）;
    nav:通常用于以下场合：网站导航条、侧边栏导航条、页内导航、前页后页翻页等。但是，普遍认为的是，一个页面上最好只用一个 nav 标签，用它来标记最重要的导航条（一般就是网站的导航条）。这样，可以让搜索引擎等快速定位，避免误导;
    section:通常对网站或页面上的内容，进行分开[article 元素与 section 元素区别详解](http://www.qianxingzhem.com/post-915.html)；
    article:来表示文档、页面或者独立的、完整的、可以独自被外部引用的内容;
    aside:表示属于这个 article 的相关描述信息。此外,aside 也用于边栏功能;
    time:标记文字的发布时间，可以让机器、搜索引擎等理解这篇文章是什么时间发表的;
    figure:规定独立的流内容（图像、图表、照片、代码等等）;
    figcaption:元素应该被置于 "figure" 元素的第一个或最后一个子元素的位置。
    mark, audio, video, source, track, bdi, canvas, command, datalist, summary, embed, keygen, meter, output, progress, rp, rt, ruby。
    
  > 6、新增属性 在 HTML5 中，增加了很多form表单属性，当然还有其他属性。 required, from, pattern, placeholder, email, range[min, max, step], url, date, time, datetime, datetime-local, month, week, tel, number, search, --, contentcontenteditableable, contextmenu, data-yourvalue, draggable, item, itemprop,spellcheck, subject。  

四、字的单位

  >  使用rem(是通过根元素进行适配的，网页中的根元素指的是html我们通过设置html的字体大小就可以控制rem的大小);
   
  


