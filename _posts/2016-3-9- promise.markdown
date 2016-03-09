---
layout:     post
title:      Promise初探
date:       2016-3-9 20:00:00
tags:
    - JavaScript
---
## Promise初探
Promise是抽象异步处理对象以及对其进行各种操作的组件。
创建promise对象的流程如下所示。
1、new Promise(fn) 返回一个promise对象

    var promise = new Promise(function(resolve, reject) {
            // 异步处理
            // 处理结束后、调用resolve 或 reject
    });

2、在fn 中指定异步等处理

    处理结果正常的话，调用resolve(处理结果值)
    处理结果错误的话，调用reject(Error对象)
    
  
Promise.reject(error)是和 Promise.resolve(value) 类似的静态方法，是 new Promise() 方法的快捷方式。
比如 Promise.resolve(42); 可以认为是以下代码的语法糖。

    new Promise(function(resolve){
        resolve(42);
    });
    
比如 Promise.reject(new Error("出错了")) 就是下面代码的语法糖形式。

    new Promise(function(resolve,reject){
        reject(new Error("出错了"));
    });
    
promise可以写成方法链的形式
  
    function taskA() {
        console.log("Task A");
    }
    function taskB() {
        console.log("Task B");
    }
    function onRejected(error) {
        console.log("Catch Error: A or B", error);
    }
    function finalTask() {
        console.log("Final Task");
    }

    var promise = Promise.resolve();
    promise
        .then(taskA)
        .then(taskB)
        .catch(onRejected)
        .then(finalTask);
        
    运行结果：Task A
    Task B
    Final Task
    