title: .net mvc display image from file
link: http://www.sheng00.com/378.html
author: admin
description: 
post_id: 378
created: 2012/06/08 13:51:57
created_gmt: 2012/06/08 05:51:57
comment_status: open
post_name: net-mvc-display-image-from-file
status: publish
post_type: post

# .net mvc display image from file

controller: 
    
    
    public ActionResult Image(string id)
    {
      var dir = Server.MapPath("/Images");
      var path = Path.Combine(dir, id + ".jpg");
      return base.File(path, "image/jpeg");
    }
    

view: 
    
    
    <img src="@Url.Action("Image", new { id= Model.Guid })" alt="@Model.Name" width="300" >

## Comments

**[admin](#5 "2014-07-31 00:28:56"):** _hhh_

