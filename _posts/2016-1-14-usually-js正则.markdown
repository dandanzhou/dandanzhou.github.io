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

    function getKeyValue(url){
        var result = {};
        var sign = '';
        if(url.indexOf('#') != -1){
            sign = '#'
        }else{
            sign = '?'
        }
        var data = url.split(sign)[1].split('&');
        for(var i = 0; i < data.length; i++){
            result[data[i].split('=')[0]] = data[i].split('=')[1];
        }
        return result;
    }
    getKeyValue(window.location.href);

