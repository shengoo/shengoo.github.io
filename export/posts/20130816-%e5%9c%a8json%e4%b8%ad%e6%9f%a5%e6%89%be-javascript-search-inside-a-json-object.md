title: 在Json中查找 Javascript search inside a JSON object
link: http://www.sheng00.com/897.html
author: admin
description: 
post_id: 897
created: 2013/08/16 16:39:00
created_gmt: 2013/08/16 08:39:00
comment_status: open
post_name: %e5%9c%a8json%e4%b8%ad%e6%9f%a5%e6%89%be-javascript-search-inside-a-json-object
status: publish
post_type: post

# 在Json中查找 Javascript search inside a JSON object

var jsonObj ={"list": [
      {"name":"my Name","id":12,"type":"car owner"},
      {"name":"my Name2","id":13,"type":"car owner2"},
      {"name":"my Name4","id":14,"type":"car owner3"},
      {"name":"my Name4","id":15,"type":"car owner5"}
    ]};
    var results = [];
    var searchField = "name";
    var searchVal = "my Name";
    for (var i=0 ; i < jsonObj.list.length ; i++)
    {
      if (jsonObj.list[i][searchField] == searchVal) {
        results.push(jsonObj.list[i]);
      }
    }
    alert(results[0]["id"]);