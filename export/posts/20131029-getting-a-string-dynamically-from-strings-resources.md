title: Getting a string dynamically from strings resources
link: http://www.sheng00.com/996.html
author: admin
description: 
post_id: 996
created: 2013/10/29 17:18:05
created_gmt: 2013/10/29 09:18:05
comment_status: open
post_name: getting-a-string-dynamically-from-strings-resources
status: publish
post_type: post

# Getting a string dynamically from strings resources

ResourceManager rm = new ResourceManager("RootResourceName",
                                             typeof(SomeClass).Assembly);
    string someString = rm.GetString("someString");