title: 如何让ASP.NET WEB API 默认返回JSON 格式
link: http://www.sheng00.com/913.html
author: admin
description: 
post_id: 913
created: 2013/08/22 10:46:06
created_gmt: 2013/08/22 02:46:06
comment_status: open
post_name: %e5%a6%82%e4%bd%95%e8%ae%a9asp-net-web-api-%e9%bb%98%e8%ae%a4%e8%bf%94%e5%9b%9ejson-%e6%a0%bc%e5%bc%8f
status: publish
post_type: post

# 如何让ASP.NET WEB API 默认返回JSON 格式

Web API 默认是返回JSON和XML的，在WebApiConfig的Register方法里可以去掉XML formatter 
    
    
    public static class WebApiConfig
    {
      public static void Register(HttpConfiguration config)
      {
        config.Routes.MapHttpRoute(
            name: "DefaultApi",
            routeTemplate: "api/{controller}/{id}",
            defaults: new { id = RouteParameter.Optional }
        );
    
        //remove xml, default json
        config.Formatters.Remove(config.Formatters.XmlFormatter);
      }
    }