title: Add jsonp support for your .net mvc api project
link: http://www.sheng00.com/1483.html
author: admin
description: 
post_id: 1483
created: 2014/10/21 13:20:07
created_gmt: 2014/10/21 05:20:07
comment_status: open
post_name: add-jsonp-support-for-your-net-mvc-api-project
status: publish
post_type: post

# Add jsonp support for your .net mvc api project

使用Attribute来实现jsonp支持 
    
    
    public class JsonpAttribute : ActionFilterAttribute
    {
      private const string CallbackQueryParameter = "callback";
      
      public override void OnActionExecuted(HttpActionExecutedContext context)
      {
        var callback = string.Empty;
     
        if (IsJsonp(out callback))
        {
          var jsonBuilder = new StringBuilder(callback);
     
          jsonBuilder.AppendFormat("({0})", context.Response.Content.ReadAsStringAsync().Result);
     
          context.Response.Content = new StringContent(jsonBuilder.ToString());
        }
     
        base.OnActionExecuted(context);
      }
      
      private bool IsJsonp(out string callback)
      {
        callback = HttpContext.Current.Request.QueryString[CallbackQueryParameter];
     
        return !string.IsNullOrEmpty(callback);
      }
    }

然后在你的WebApiConfig里面加上 `config.Filters.Add(new JsonpAttribute());` 这样你的api既能支持json，又能支持jsonp了。 如果url里有?callback=?，就会返回jsonp格式的数据，如果没有，依然是json