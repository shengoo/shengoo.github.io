title: .net mvc 中使用ActionFilterAttribute过滤器
link: http://www.sheng00.com/27.html
author: admin
description: 
post_id: 27
created: 2010/03/24 08:00:00
created_gmt: 2010/03/24 00:00:00
comment_status: open
post_name: net-mvc-%e4%b8%ad%e4%bd%bf%e7%94%a8actionfilterattribute%e8%bf%87%e6%bb%a4%e5%99%a8
status: publish
post_type: post

# .net mvc 中使用ActionFilterAttribute过滤器

过滤器是mvc中常用的 在.net mvc 中直接继承和实现ActionFilterAttribute类就可以了 很简单 下面贴出一个例子 过滤器： 
    
    
    public class UseStopwatchAttribute : ActionFilterAttribute
    {
      public override void OnActionExecuting(ActionExecutingContext filterContext)
      {
        Stopwatch stopWatch = new Stopwatch();
        stopWatch.Start();
    
        filterContext.Controller.ViewData["stopWatch"] = stopWatch;
      }
    
      public override void OnResultExecuting(ResultExecutingContext filterContext)
      {
        Stopwatch stopWatch = (Stopwatch)filterContext.Controller.ViewData["stopWatch"];
        stopWatch.Stop();
        Random r = new Random();
    
        filterContext.Controller.ViewData["elapsedTime"] = stopWatch.ElapsedMilliseconds
        + " milliseconds -   Rand  " + r.Next(1000).ToString();
      }
    }
    

这的话这个过滤器就写好了 在使用的时候只要在controller上写上就行了 
    
    
    [UseStopwatch]
    public class ProductsController : Controller
    {
      //
      // GET: /Store/Products/
    
      public ActionResult List()
      {
        return View();
      }
    
      public ActionResult Details()
      {
        return View();
      }
    
      public ActionResult AddReview()
      {
        return View();
      }
    }