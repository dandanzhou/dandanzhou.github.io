---
layout:     post
title:      支付拦截解决方案
date:       2016-06-05
tags:
    - Others
---	

额，先说点题外话哈。真实惭愧啊，距离上次写博客差不多有两个月的时间了。该写了，直接进入正题吧，哈哈哈哈...

如果你是直接点击充值跳到另外一个页面，不用向第三方传一些数据，以下就不用看了。
	
## 支付拦截解决方案		
 上个星期和后端做支付对接的时候，遇到一个小问题：点击充值按钮进行充值跳到第三方充值页的时候，充值页被拦截了！！！！！
 
 背景：点击充值的时候后台要我先传金额获取一些数据然后再掉充值接口跳到支付页
 	
 于是出现如下图所示：
 ![http://7xnl4q.com1.z0.glb.clouddn.com/fail.png]( http://7xnl4q.com1.z0.glb.clouddn.com/fail.png)
 
 后来在网上查找了原因，原来是这样滴：
    用户自己发起的浏览器不会阻止，如果触发动作是自动执行的则浏览器会阻止打开。（进入ajax是自动的但是ajax执行完）会认为你是弹广告xxxxxxx！想不被阻止就想办法让动作换成用户自己发起的。
    
 
 所以有了以下解决方案：
    由于之前跳到支付页用的xx.submit()，是在ajax内自动执行完的，并不是用户自己发起的；所以我们需要一个过渡，就是把这个动作赋予用户自己完成。
    我的想法是点击充值时让先弹出一个窗口确定输入的金额，然后让用户点击确定调用xx.sumbit();经过试验真的成功了。
    
    
 成功后的如下图：
  ![http://7xnl4q.com1.z0.glb.clouddn.com/way.png]( http://7xnl4q.com1.z0.glb.clouddn.com/way.png)
  ![http://7xnl4q.com1.z0.glb.clouddn.com/success.png]( http://7xnl4q.com1.z0.glb.clouddn.com/success.png)
  
  
 
   