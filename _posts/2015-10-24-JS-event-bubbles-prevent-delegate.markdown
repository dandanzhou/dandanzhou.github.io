---
layout:     post
title:      JavaScript事件冒泡、事件委托和阻止事件
date:       2015-10-24 14:13:00
tags:
    - JavaScript
---

## 事件冒泡
  什么是“事件冒泡”呢？假设这里有一杯水，水被用某种神奇的方式分成不同颜色的几层。
  这时，从最底层冒出了一个气泡，气泡会一层一层地上升，直到最顶层。而你不管在水的
  哪一层观察都可以看到并捕捉到这个气泡。好了，把“水”改成“DOM”，把“气泡”改成“事件”。
  这就是“事件冒泡”。
  
  在网上查找了一个[demo](http://www.pureweber.com/works/demos/js-event-delegation/event-bubble.html)
  代码如下：

CSS 

      .white{background-color:#fff;}
      .d-1{width:400px;height:400px;border:1px solid #000;margin:50px 50px;}
      .d-2{width:300px;height:300px;border:1px solid #000;margin:50px 50px;}
      .d-3{width:200px;height:200px;border:1px solid #000;margin:50px 50px;}
      .d-4{width:100px;height:100px;border:1px solid #000;margin:50px 50px;}
      
HTML 

      <div id="d1" class="white d-1">
          <div id="d2" class="white d-2">
              <div id="d3" class="white d-3">
                   <div id="d4" class="white d-4"></div>
              </div>
           </div>
     </div>
     <button id="reset1">重置</button> 
     
JavaScript

     jQuery('#d4').click(function(){jQuery(this).css('background-color', 'yellow')});
     jQuery('#d3').click(function(){jQuery(this).css('background-color', 'green')});
     jQuery('#d2').click(function(){jQuery(this).css('background-color', 'blue')});
     jQuery('#d1').click(function(){jQuery(this).css('background-color', 'red')});
     jQuery('#reset1').click(function(){jQuery('.white').css('background-color', '#fff')});
  
  点击最小的那个，外面所有的都会被上色。你会发现，点击里层的正方形，外层所有的正方形都会被上色。
  因为它们也都捕捉到了点击事件。看，他们抓到“气泡”了！


## 事件委托
  修改上面的程序，使用事件委托来处理点击事件。当最顶层捕获点击事件时，查看事件来源于哪一层，然后只将那一层涂色。
  再次点击每一层，查看实际效果。只有当前点击的正方形变色了，其他的都毫无反应。
  
      jQuery('#d1').click(function(e){
        var t = jQuery(e.target);
        var id = t.attr('id');
        if (id==='d4'){
                t.css('background-color', 'yellow');
        } else if (id==='d3') {
                t.css('background-color', 'green');
        } else if (id==='d2') {
                t.css('background-color', 'blue');
        } else {
                t.css('background-color', 'red');
        }
});

  当然，如果你有这样嵌套的页面元素，使用了事件委托，委托到了最顶层，这时需要注意：如果其中某个元素，你不希望它的事件冒泡，
  那么可以使用某种方式阻止事件的冒泡。在jQuery框架中，可以使用stopPropagation()方法来实现而不必关心浏览器兼容性。
  
     $('#bind').click(function(){
        if ($(this).is(':checked')) {
            $('#d4').bind('click', function(e){
                e.stopPropagation();
                alert('冒泡被阻止，这块将不会改变颜色');
            });
        } else {
            $('#d4').unbind('click');
        }
    });


## 阻止事件
  w3c 的方法是 e.preventDefault()，IE 则是使用 e.returnValue = false;
  在支持 addEventListener() 的浏览器中，也能通过调用时间对象的 preventDefault() 方法取消时间的默认操作。
  不过，在 IE9 之前的 IE 中，可以通过设置事件对象的 returnValue 属性为 false 来达到同样的效果。
  下面的代码假设一个事件处理程序，它使用全部的三种取消技术：
  
      function cancelHandler(event){  
        var event = event || window.event;  //用于IE  
        if(event.preventDefault) event.preventDefault();  //标准技术  
        if(event.returnValue) event.returnValue = false;  //IE  
        return false;   //用于处理使用对象属性注册的处理程序  
      }  
      
  当前的 DOM 事件模型草案定义了 Event 对象属性 defaultPrevented。
  
  javascript 的 return false 只会阻止默认行为，而是用 jQuery 的话则既阻止默认行为又防止对象冒泡。
