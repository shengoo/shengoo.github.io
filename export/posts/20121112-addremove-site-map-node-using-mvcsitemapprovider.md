title: Add/remove site map node using MvcSiteMapProvider
link: http://www.sheng00.com/488.html
author: admin
description: 
post_id: 488
created: 2012/11/12 11:20:07
created_gmt: 2012/11/12 03:20:07
comment_status: open
post_name: addremove-site-map-node-using-mvcsitemapprovider
status: publish
post_type: post

# Add/remove site map node using MvcSiteMapProvider

add new CustomSiteMapProvider 
    
    
    public class CustomSiteMapProvider : DefaultSiteMapProvider
    {
    public void ClearSiteMap()
    {
    Clear();
    }
    }
    

Change web.config file to use the custom sitemapprovider instead of DefaultSiteMapProvider. When node changes, add 
    
    
    ((CustomSiteMapProvider)SiteMap.Provider).ClearSiteMap();