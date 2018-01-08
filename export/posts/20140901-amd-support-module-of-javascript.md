title: AMD support Module of JavaScript
link: http://www.sheng00.com/1423.html
author: admin
description: 
post_id: 1423
created: 2014/09/01 17:52:37
created_gmt: 2014/09/01 09:52:37
comment_status: open
post_name: amd-support-module-of-javascript
status: publish
post_type: post

# AMD support Module of JavaScript

var myModule = {
      awesome: 'not really'
    };
    
    if (typeof define === 'function' && define.amd) {
      define('myModule', [], function() {
        return myModule;
      });
    }