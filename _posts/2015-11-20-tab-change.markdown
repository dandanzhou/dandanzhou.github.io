---
layout:     post
title:      tab切换
date:       2015-11-20 9:00:00
tags:
    - Jquery
---

## tab切换
 
HTML部分 
 
    <ul class="tabs" id="tab">
        <li><a href="javascript:void(0)" class="current">tab切换一</a></li>
        <li><a href="javascript:void(0)" >tab切换二</a></li>
        <li><a href="javascript:void(0)">tab切换三</a></li>
    </ul>

    <div class="container" id="contain">
        <div class="con">显示内容一</div>
        <div class="con">显示内容二</div>
        <div class="con">显示内容三</div>
    </div>
    
    
Jquery部分
 
    $(function(){
        tabs($("#tab a"), $('#contain .con'));  
    });

    var tabs = function(tab, con){
        tab.click(function(){
            var dIndex = tab.index(this);
            tab.removeClass('current');
            $(this).addClass('current');
            con.hide();
            con.eq(dIndex).show();
        });    
    }