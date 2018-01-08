title: .net mvc html form beginform beginrouteform
link: http://www.sheng00.com/62.html
author: admin
description: 
post_id: 62
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: net-mvc-html-form-beginform-beginrouteform
status: publish
post_type: post

# .net mvc html form beginform beginrouteform

FormExtensions类  
该类定了3种类型的扩展方法，它们分别是`BeginForm`,`BeginRouteForm`,`EndForm`  
BeginForm共有13种重载方法，这里参数不一一介绍。  
BeginRouteForm共有12种重载方法，主要表现定义表单的开始部分，其中是以路由的方式设置action的值  
EndForm 主要表现在表单的结尾，生成`</form>`  
如下表单使用的几种方式:  
方式1:  

    
    
    <%=Html.BeginForm("Login", "Home", FormMethod.Post, new { id="name"})%>
    姓名<%=Html.TextBox("name", null, new { id="name",width="200px"})%><br />
    密码<%=Html.Password("pass", null, new { id = "pass", width = "200px" })%><br />
    <input type="submit" id="btnSubmit" value="Submit" />
    <%Html.EndForm(); %>
    

这里注意`<%=Html.BeginForm() %>` 和`<%Html.EndForm();%>`后者有 `" ; "`  
Login:是指Action，Home是指Conroller，FormMethod.Post是指用Post方式来提交表单  
new{id="name"} 是指表单元素属性。<form id="name" action="Home/Login" method="post"></form>  
  
方式2: 
    
    
    <fieldset>
    <%=Html.BeginRouteForm("Start", new { controller = "Home", action = "Login" }, FormMethod.Post)%>
    姓名<%=Html.TextBox("name", null, new { id="name",width="200px"})%><br />
    密码<%=Html.Password("pass", null, new { id = "pass", width = "200px" })%><br />
    <input type="submit" id="Submit1" value="Submit" />
    <%Html.EndForm(); %>
    </fieldset>
    

这种方式的表单是以路由的方式设置action 的，"Start" 是路由的名称:  

    
    
    routes.MapRoute(
    "Start",
    "{controller}/{action}",
    new { controller="Home",action="Index"}
    );
    

  
方式3:  

    
    
    <fieldset>
    <%using (Html.BeginForm("Login", "Home", FormMethod.Post, new { id = "name" }))
    {
    %>
    姓名<%=Html.TextBox("name", null, new { id="name",width="200px"})%><br />
    密码<%=Html.Password("pass", null, new { id = "pass", width = "200px" })%><br />
    <input type="submit" id="btnSubmit" value="Submit" />
    <%
    } %>
    </fieldset>
    

这种方式不需要`<%Html.EndForm();%>` 其余的方式基本相同  
  
方式4:  
就是普通的html代码  

    
    
    <form id="name" method="post" action="Home/Login">
    </form>
    

这里不做介绍