title: JavaScript 格式化 json 时间 C# datetime
link: http://www.sheng00.com/60.html
author: admin
description: 
post_id: 60
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: javascript-%e6%a0%bc%e5%bc%8f%e5%8c%96-json-%e6%97%b6%e9%97%b4-c-datetime
status: publish
post_type: post

# JavaScript 格式化 json 时间 C# datetime

function FormatTime(jsonDate,formatString) {
        jsonDate = jsonDate.split('(')[1].split(')')[0];
        var rDate = new Date(parseInt(jsonDate));
        return rDate.format(formatString);
    }
    

` function FormatTime(jsonDate,formatString) { jsonDate = jsonDate.split('(')[1].split(')')[0]; var rDate = new Date(parseInt(jsonDate)); return rDate.format(formatString); } `