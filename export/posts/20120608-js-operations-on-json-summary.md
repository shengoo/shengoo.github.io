title: JS operations on JSON summary
link: http://www.sheng00.com/380.html
author: admin
description: 
post_id: 380
created: 2012/06/08 15:45:38
created_gmt: 2012/06/08 07:45:38
comment_status: open
post_name: js-operations-on-json-summary
status: publish
post_type: post

# JS operations on JSON summary

`JSON`(JavaScript Object Notation) 是一种轻量级的数据交换格式，采用完全独立于语言的文本格式，是理想的数据交换格式。同时，JSON是 JavaScript 原生格式，这意味着在 JavaScript 中处理 JSON数据不须要任何特殊的 API 或工具包。 本文主要是对JS操作JSON的要领做下总结。 在JSON中，有两种结构：对象和数组。 

  1. 一个对象以`{`（左括号）开始，`}`（右括号）结束。每个“名称”后跟一个`:`（冒号）；“‘名称/值’ 对”之间运用 `,`（逗号）分隔。 名称用引号括起来；值如果是字符串则必须用括号，数值型则不须要。例如： 
    
        var o = {
      "xlid": "cxh",
      "xldigitid": 123456,
      "topscore": 2000,
      "topplaytime": "2009-08-20"
    }
    

  2. 数组是值（value）的有序集合。一个数组以`[`（左中括号）开始，`]`（右中括号）结束。值之间运用 `,`（逗号）分隔。例如： 
    
        var jsonranklist = [{
      "xlid": "cxh",
      "xldigitid": 123456,
      "topscore": 2000,
      "topplaytime": "2009-08-20"
    }, {
      "xlid": "zd",
      "xldigitid": 123456,
      "topscore": 1500,
      "topplaytime": "2009-11-20"
    }];
    

为了方便地处理JSON数据，JSON提供了json.js包，下载地址：<http://www.json.org/json.js> 在数据传输流程中，json是以文本，即字符串的形式传递的，而JS操作的是JSON对象，所以，JSON对象和JSON字符串之间的相互转换是关键。例如： 

  * JSON字符串: 
    
        var str1 = '{ "name": "cxh", "sex": "man" }';
    

  * JSON对象: 
    
        var str2 = { "name": "cxh", "sex": "man" };
    

  1. JSON字符串转换为JSON对象,要运用上面的str1，必须运用下面的要领先转化为JSON对象： 
    
        var obj = eval('(' + str + ')');//由JSON字符串转换为JSON对象
    

或者 
    
        var obj = str.parseJSON(); //由JSON字符串转换为JSON对象
    

或者 
    
        var obj = JSON.parse(str); //由JSON字符串转换为JSON对象
    

然后，就可以这样读取： 
    
        Alert(obj.name);
    Alert(obj.sex);
    

特别留心：如果obj本来就是一个JSON对象，那么运用 eval（）函数转换后（哪怕是多次转换）还是JSON对象，但是运用 parseJSON（）函数处理后会有疑问（抛出语法异常）。

  2. 可以运用 toJSONString()或者全局要领 JSON.stringify()将JSON对象转化为JSON字符串。 例如： 
    
        var last=obj.toJSONString(); //将JSON对象转化为JSON字符
    

或者 
    
        var last=JSON.stringify(obj); //将JSON对象转化为JSON字符
    
    
        alert(last);
    

留心：上面的多个要领中，除了`eval()`函数是js自带的之外，其他的多个要领都来自`json.js`包。新版本的 JSON 修改了 API，将 `JSON.stringify()` 和 `JSON.parse()` 两个要领都注入到了 Javascript 的内建对象里面，前者变成了 `Object.toJSONString()`，而后者变成了 `String.parseJSON()`。如果提示找不到`toJSONString()`和`parseJSON()`要领，则说明您的json包版本太低。