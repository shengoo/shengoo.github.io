title: Routing in ASP.NET Web API
link: http://www.sheng00.com/905.html
author: admin
description: 
post_id: 905
created: 2013/08/21 13:32:32
created_gmt: 2013/08/21 05:32:32
comment_status: open
post_name: routing-in-asp-net-web-api
status: publish
post_type: post

# Routing in ASP.NET Web API

## Routing Tables

In ASP.NET Web API, a?_controller_?is a class that handles HTTP requests. The public methods of the controller are called?_action methods_?or simply?_actions_. When the Web API framework receives a request, it routes the request to an action. To determine which action to invoke, the framework uses a?_routing table_. The Visual Studio project template for Web API creates a default route: 
    
    
    routes.MapHttpRoute(
        name: "API Default",
        routeTemplate: "api/{controller}/{id}",
        defaults: new { id = RouteParameter.Optional }
    );

This route is defined in the WebApiConfig.cs file, which is placed in the App_Start directory: ![](/wp-content/uploads/2013/08/94714.png?cdn_id=2013-08-19-002) For more information aboout the?**WebApiConfig**?class, see?[Configuring ASP.NET Web API?](http://www.asp.net/web-api/overview/extensibility/configuring-aspnet-web-api). If you self-host Web API, you must set the routing table directly on the?**HttpSelfHostConfiguration**?object. For more information, see?[Self-Host a Web API](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/self-host-a-web-api). Each entry in the routing table contains a?_route template_. The default route template for Web API is "api/{controller}/{id}". In this template, "api" is a literal path segment, and {controller} and {id} are placeholder variables. When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table. If no route matches, the client receives a 404 error. For example, the following URIs match the default route: 

  * /api/contacts
  * /api/contacts/1
  * /api/products/gizmo1
However, the following URI does not match, because it lacks the "api" segment: 
  * /contacts/1
**Note:**?The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing. That way, you can have "/contacts" go to an MVC controller, and "/api/contacts" go to a Web API controller. Of course, if you don't like this convention, you can change the default route table. Once a matching route is found, Web API selects the controller and the action: 

  * To find the controller, Web API adds "Controller" to the value of the?_{controller}_?variable.
  * To find the action, Web API looks at the HTTP method, and then looks for an action whose name begins with that HTTP method name. For example, with a GET request, Web API looks for an action that starts with "Get...", such as "GetContact" or "GetAllContacts".? This convention applies only to GET, POST, PUT, and DELETE methods. You can enable other HTTP methods by using attributes on your controller. We’ll see an example of that later.
  * Other placeholder variables in the route template, such as?_{id},_?are mapped to action parameters.
Let's look at an example. Suppose that you define the following controller: 
    
    
    public class ProductsController : ApiController
    {
        public void GetAllProducts() { }
        public IEnumerable<Product> GetProductById(int id) { }
        public HttpResponseMessage DeleteProduct(int id){ }
    }

Here are some possible HTTP requests, along with the action that gets invoked for each: 

HTTP Method URI Path Action Parameter

GET
api/products
GetAllProducts
_(none)_

GET
api/products/4
GetProductById
4

DELETE
api/products/4
DeleteProduct
4

POST
api/products
_(no match)_
Notice that the?_{id}_?segment of the URI, if present, is mapped to the?_id_?parameter of the action. In this example, the controller defines two GET methods, one with an?_id_?parameter and one with no parameters. Also, note that the POST request will fail, because the controller does not define a "Post..." method. 

## Routing Variations

The previous section described the basic routing mechanism for ASP.NET Web API. This section describes some variations. 

### HTTP Methods

Instead of using the naming convention for HTTP methods, you can explicitly specify the HTTP method for an action by decorating the action method with the?**HttpGet**,?**HttpPut**,?**HttpPost**, or?**HttpDelete**?attribute. In the following example, the FindProduct method is mapped to GET requests: 
    
    
    public class ProductsController : ApiController
    {
        [HttpGet]
        public Product FindProduct(id) {}
    }

To allow multiple HTTP methods for an action, or to allow HTTP methods other than GET, PUT, POST, and DELETE, use the?**AcceptVerbs**?attribute, which takes a list of HTTP methods. 
    
    
    public class ProductsController : ApiController
    {
        [AcceptVerbs("GET", "HEAD")]
        public Product FindProduct(id) { }
    
        // WebDAV method
        [AcceptVerbs("MKCOL")]
        public void MakeCollection() { }
    }

### Routing by Action Name

With the default routing template, Web API uses the HTTP method to select the action. However, you can also create a route where the action name is included in the URI: 
    
    
    routes.MapHttpRoute(
        name: "ActionApi",
        routeTemplate: "api/{controller}/{action}/{id}",
        defaults: new { id = RouteParameter.Optional }
    );

In this route template, the?_{action}_?parameter names the action method on the controller. With this style of routing, use attributes to specify the allowed HTTP methods. For example, suppose your controller has the following method: 
    
    
    public class ProductsController : ApiController
    {
        [HttpGet]
        public string Details(int id);
    }

In this case, a GET request for “api/products/details/1” would map to the Details method. This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API. You can override the action name by using the?**ActionName**?attribute. In the following example, there are two actions that map to "api/products/thumbnail/_id_. One supports GET and the other supports POST: 
    
    
    public class ProductsController : ApiController
    {
        [HttpGet]
        [ActionName("Thumbnail")]
        public HttpResponseMessage GetThumbnailImage(int id);
    
        [HttpPost]
        [ActionName("Thumbnail")]
        public void AddThumbnailImage(int id);
    }

### Non-Actions

To prevent a method from getting invoked as an action, use the?**NonAction**?attribute. This signals to the framework that the method is not an action, even if it would otherwise match the routing rules. 
    
    
    // Not an action method.
    [NonAction]  
    public string GetPrivateData() { ... }

## Further Reading

This topic provided a high-level view of routing. For more detail, see?[Routing and Action Selection](http://www.asp.net/web-api/overview/web-api-routing-and-actions/routing-and-action-selection), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.