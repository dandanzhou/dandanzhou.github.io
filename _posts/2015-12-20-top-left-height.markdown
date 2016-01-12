---
layout:     post
title:      各种top、left、height
date:       2015-12-20 22:00:00
tags:
    - JavaScript
---

## 各种top、left、height

> 网页可见区域宽： document.body.clientWidth;
网页可见区域高： document.body.clientHeight;
网页可见区域宽： document.body.offsetWidth   (包括边线的宽);
网页可见区域高： document.body.offsetHeight  (包括边线的宽);
网页正文全文宽： document.body.scrollWidth;
网页正文全文高： document.body.scrollHeight;
网页被卷去的高： document.body.scrollTop;
网页被卷去的左： document.body.scrollLeft;
    
假设 obj 为某个 HTML 控件。

    obj.offsetTop 指 obj 距离上方或上层控件的位置，整型，单位像素。
    obj.offsetLeft 指 obj 距离左方或上层控件的位置，整型，单位像素。
    obj.offsetWidth 指 obj 控件自身的宽度，整型，单位像素。
    obj.offsetHeight 指 obj 控件自身的高度，整型，单位像素。
    
offsetTop 与 style.top 的区别

    1、offsetTop 返回的是数字，而 style.top 返回的是字符串，除了数字外还带有单位：px。
    2、offsetTop 只读，而 style.top 可读写。
    3、如果没有给 HTML 元素指定过 top 样式，则 style.top 返回的是空字符串。
    
offsetWidth 与 style.width 的区别
  
    如对象的宽度设定值为百分比宽度,则无论页面变大还是变小,style.width都返回此百分比,而offsetWidth则返回在不同页面中对象的宽度值而不是百分比值

clientHeight、offsetHeight和scrollHeight 的区别

    clientHeight 就是透过浏览器看内容的这个区域高度。
    NS（Netscape）、 FF （FireFox）认为 offsetHeight 和 scrollHeight 都是网页内容高度，只不过当网页内容高度小于等于 clientHeight 时，scrollHeight 的值是 clientHeight，而 offsetHeight 可以小于 clientHeight。
    IE、Opera 认为 offsetHeight 是可视区域 clientHeight 滚动条加边框。scrollHeight 则是网页内容实际高度。




    
            
