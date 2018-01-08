title: MVC3-Razor输出Html
link: http://www.sheng00.com/292.html
author: admin
description: 
post_id: 292
created: 2012/01/19 17:33:02
created_gmt: 2012/01/19 09:33:02
comment_status: open
post_name: mvc3-razor%e8%be%93%e5%87%bahtml
status: publish
post_type: post

# MVC3-Razor输出Html

## 输出HTML代码（包含标签）：直接输出，
    
    
    string html = "文本"; 
    @html

## 输出HTML内容（不包含标签）：有两种方法，

### 第一种：
    
    
    IHtmlString html=new HtmlString("文本");
    @html ;

### 第二种：
    
    
    string html = "文本"; 
    @Html.Raw(html);