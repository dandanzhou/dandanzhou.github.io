---
layout:     post
title:      parent()、parents()、closest()的区别
date:       2015-10-14 20:52:42
tags:
    - Jquery
---


![](http://7xnl4q.com1.z0.glb.clouddn.com/post-bg-jquery-classfication.png)

## 区别   

    1.parent()方法从指定类型的直接父节点开始查找，在"0"中， <a> 的直接父节点是<li>所以在这里找不到<ul>父节点。在"2"中先找到了<li>，接着找到<ul>，并将它的背景色设置为yellow。parent()返回一个节点。   
 
    2.parents()方法查找方式同parent()方法类似，不同的一点在于，当它找到第一的父节点时并没有停止查找，而是继续查找，最后返回多个父节点，如在"2"中，使得id为menu的ul整个背景色变成了yellow。      
  
    3.closest()方法查找时从包含自身的节点找起，它同parents()很类似，不同点就在于它只返回一个节点如在"3"中，实现的功能同1相同。但它使得代码量减小，同"2"相比又只返回单一的一个节点。可见，closest()方法在项目中的使用频率是比较大的。


## 寻找子节点和兄弟节点

* children(expr) //查找所有子元素，只会找到直接的孩子节点，不会返回所有子孙
* contents() //查找下面的所有内容，包括节点和文本。
* prev() //查找上一个兄弟节点，不是所有的兄弟节点
* prevAll() //查找所有之前的兄弟节点
* next() //查找下一个兄弟节点，不是所有的兄弟节点
* nextAll() //查找所有之后的兄弟节点
* siblings() //查找兄弟节点，不分前后
* find() //会在div元素内 寻找 class为classname的元素。(子元素找)
* filter() //则是筛选div的class为classname的元素。(平级找)