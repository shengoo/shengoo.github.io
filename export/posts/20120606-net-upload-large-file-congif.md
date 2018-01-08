title: IIS .net upload large file congif
link: http://www.sheng00.com/376.html
author: admin
description: 
post_id: 376
created: 2012/06/06 14:06:06
created_gmt: 2012/06/06 06:06:06
comment_status: open
post_name: net-upload-large-file-congif
status: publish
post_type: post

# IIS .net upload large file congif

IIS 7.x, 
    
    
    ?<system.webServer>
     <security>
     <requestFiltering>
     <requestLimits maxAllowedContentLength="2147483648" />
     </requestFiltering>
     </security>
    </system.webServer>

IIS 6.0 
    
    
    ?<system.web>
     <httpRuntime maxRequestLength="2097151" />
    </system.web>