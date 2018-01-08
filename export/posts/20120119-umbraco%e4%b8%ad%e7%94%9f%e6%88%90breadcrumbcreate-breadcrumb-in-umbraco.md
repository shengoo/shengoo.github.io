title: Umbraco中生成Breadcrumb,create Breadcrumb in Umbraco
link: http://www.sheng00.com/298.html
author: admin
description: 
post_id: 298
created: 2012/01/19 17:39:01
created_gmt: 2012/01/19 09:39:01
comment_status: open
post_name: umbraco%e4%b8%ad%e7%94%9f%e6%88%90breadcrumbcreate-breadcrumb-in-umbraco
status: publish
post_type: post

# Umbraco中生成Breadcrumb,create Breadcrumb in Umbraco

我的Breadcrumb是用Partial 首先新建一个Partial:Breadcrumb ![2012-01-19_17-33-33](/wp-content/uploads/2012/01/2012-01-19_17-33-33_thumb.png) 在里面插入代码: 
    
    
    @inherits RenderViewPage
    @using Umbraco.Cms.Web
    @using System
    
     @{
         var Homepage = @DynamicModel;
         var lis = string.Empty;
         lis = string.Format("
    * {0}
    ", Homepage.Name) + lis;
         while (Homepage.ContentType.Alias != "homePage";)
         {
             Homepage = Homepage.Parent;
             lis = string.Format("
    * [{1}]({0})
    ", Homepage.Url, Homepage.Name) + lis; 
         } 
    }
    
    
    @Html.Raw(lis)
    
    

这样就行了 在使用的地方: @Html.Partial("Breadcrumb")   效果如下: ![2012-01-19_17-33-52](/wp-content/uploads/2012/01/2012-01-19_17-33-52_thumb.png) 当然必要的css还是需要的,这里就不贴了.