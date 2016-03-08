---
layout:     post
title:      Js常用正则
date:       2016-1-14 14:12:00
tags:
    - JavaScript
---
##  Js常用正则
前端开发中总避免不了使用一些正则表达式来处理一些问题，下面就列常用的几例

> 字符串去重

    var str = "adsfjjbkk";  
    // \1匹配第一个子串  
    // 只去除连续重复  
    console.log(str.replace(/(.)(\1)+/g,function($1,$2,$3){  
        return $2;  
    }));// adsfjbk

> js获取URL中的参数

    function GetQueryString(name) {
        var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
        var r = window.location.search.substr(1).match(reg); //获取url中"?"符后的字符串并正则匹配
        var context = "";
        if (r != null)
        context = r[2];
        reg = null;
        r = null;
        return context == null || context == "" || context == "undefined" ? "" : context;
    }
    alert(GetQueryString("q"));
