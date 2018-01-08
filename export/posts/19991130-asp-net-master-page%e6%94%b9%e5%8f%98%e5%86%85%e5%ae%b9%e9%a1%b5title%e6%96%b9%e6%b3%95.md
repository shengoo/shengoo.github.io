title: ASP.NET Master Page改变内容页title方法
link: http://www.sheng00.com/73.html
author: admin
description: 
post_id: 73
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: asp-net-master-page%e6%94%b9%e5%8f%98%e5%86%85%e5%ae%b9%e9%a1%b5title%e6%96%b9%e6%b3%95
status: publish
post_type: post

# ASP.NET Master Page改变内容页title方法

在定义好母版页以后，有时我们需要改变网页的标题但是如果直接在母版页中更改title属性又会导致其他的内容页出现相同的title情况,VS2008中提供了母版页的新功能。 

### 1.通过内容页中的Page指令中Title属性改变内容页title:
    
    
    <%@ Page Language=”C#” MasterPageFile=”~/MyMaster.master” Title=”My Title” %>
    

### 2.通过编程改变:前提是