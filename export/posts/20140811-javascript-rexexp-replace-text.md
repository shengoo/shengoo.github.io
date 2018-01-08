title: JavaScript RexExp replace text 
link: http://www.sheng00.com/1365.html
author: admin
description: 
post_id: 1365
created: 2014/08/11 17:59:46
created_gmt: 2014/08/11 09:59:46
comment_status: open
post_name: javascript-rexexp-replace-text
status: publish
post_type: post

# JavaScript RexExp replace text 

function addBrackets(match){
      return '(' + match+ ')';
    }
    
    var str = 'zhllZHaa';
    var reg = new RegExp('zh', 'ig');
    console.log(str.replace(reg,addBrackets))//(zh)ll(ZH)aa