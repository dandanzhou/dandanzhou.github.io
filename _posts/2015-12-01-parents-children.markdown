---
layout:     post
title:      易混淆的方法
date:       2015-12-01 18:05:00
tags:
    - Jquery
---

## 易混淆的方法

  parent()：查找<em style="color:red;">直接的</em>父节点
  parents()：查找<em style="color:red;">所有的</em>祖先元素
  sibling()：查找兄弟节点，不分前后
  children()：查找所有子元素，只会找到<em style="color:red;">直接的</em>孩子节点，不会返回所有子孙
  find()：会在div元素内 寻找 class为classname的元素。(<em style="color:red;">子元素</em>找)
  filter()：则是筛选div的class为classname的元素。(<em style="color:red;">平级</em>找)
  
  
  get()：接受一个索引值参数并返回对应的DOM节点
  index()：接受一个DOM节点然后返回其索引值，index(this)返回当前值的索引值
  eq(index)：index为正整数时以0为基数，index为负整数时从集合中的最后一个元素开始倒数（从1开始倒数）