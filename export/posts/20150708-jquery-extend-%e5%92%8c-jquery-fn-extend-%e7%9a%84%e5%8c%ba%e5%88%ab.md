title: jQuery.extend 和 jQuery.fn.extend 的区别
link: http://www.sheng00.com/2114.html
author: admin
description: 
post_id: 2114
created: 2015/07/08 22:07:04
created_gmt: 2015/07/08 14:07:04
comment_status: open
post_name: jquery-extend-%e5%92%8c-jquery-fn-extend-%e7%9a%84%e5%8c%ba%e5%88%ab
status: publish
post_type: post

# jQuery.extend 和 jQuery.fn.extend 的区别

## jQuery.extend

jQuery.extend可以扩展jQuery对象本身。 用来在jQuery命名空间上增加新函数，或者合并对象。 1\. 增加方法： 
    
    
    $.extend({
      hello: function () {
        console.log(this)//function jQuery(selector, context)
      }
    });
    
    $.hello();
    

  1. 合并对象
    
    
    var obj1 = {'name' : 'sheng00'};
    var obj2 = {'sex' : 'Male'};
    
    $.extend(obj1, obj2);
    
    console.log(obj1)//Object {name: "sheng00", sex: "Male"}
    

## jQuery.fn.extend

用来扩展 jQuery 元素集来提供新的方法（通常用来制作插件） 
    
    
    $.fn.extend({
      turn_red: function () {
        return this.each(function () {
          this.style.color = 'red'
        });
      }
    });
    
    $('.elements').turn_red(); // sets color to red
    

效果和`jQuery.fn.turn_red=function(){}`是一样的