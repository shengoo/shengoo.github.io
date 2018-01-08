title: Using the ASP.NET MVC 3 Logon returnUrl Parameter
link: http://www.sheng00.com/371.html
author: admin
description: 
post_id: 371
created: 2012/05/07 16:36:44
created_gmt: 2012/05/07 08:36:44
comment_status: open
post_name: using-the-asp-net-mvc-3-logon-returnurl-parameter
status: publish
post_type: post

# Using the ASP.NET MVC 3 Logon returnUrl Parameter

### razor:
    
    
    @{ 
      ViewBag.Title = "登陆"; 
      Layout = "~/Views/Shared/_LoginLayout.cshtml"; 
      string retUrl = "";
    
      if (Request["ReturnUrl"] != null) 
      {
    
        retUrl = ViewContext.HttpContext.Request["ReturnUrl"];
    
      } 
    }
    
    @using (Html.BeginForm("Logon", "Account", new { model = this.Model, ReturnUrl = retUrl })) 
    {
    //form  
    }
    

### controller:
    
    
    [HttpPost] 
    public ActionResult LogOn(LogOnModel model, string ReturnUrl) 
    { 
      ViewBag.UserLogOut = true; 
      if (!ModelState.IsValid) 
        return View("Logon"); 
    
      if (ModelState.IsValid) 
      { 
        try 
        { 
          //login
    
        } 
        catch (Exception e) 
        { 
          ModelState.AddModelError("", e.Message); 
          return View(model); 
        }
      } 
      if (!string.IsNullOrEmpty(ReturnUrl)) 
        return Redirect(ReturnUrl);//return 
      return RedirectToAction("Index", "Product");
    }
    

### UserSessionAuthorizeAttribute:
    
    
    public class UserSessionAuthorizeAttribute : AuthorizeAttribute 
    { 
      public override void OnAuthorization(AuthorizationContext  filterContext) 
      { 
    
        base.OnAuthorization(filterContext); 
        if(//check session) 
        { 
          filterContext.Result = new RedirectToRouteResult( 
            new System.Web.Routing.RouteValueDictionary 
                { 
                  { "controller", "Account" }, 
                  { "action", "LogOn" }, 
                  { "ReturnUrl", filterContext.HttpContext.Request.RawUrl } 
                }); 
        }
    
      } 
    }