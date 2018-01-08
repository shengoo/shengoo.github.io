title: Check if Function Exists Before Calling
link: http://www.sheng00.com/1067.html
author: admin
description: 
post_id: 1067
created: 2014/02/13 15:08:07
created_gmt: 2014/02/13 07:08:07
comment_status: open
post_name: check-if-function-exists-before-calling
status: publish
post_type: post

# Check if Function Exists Before Calling

When using scripts that are shared between different areas of a site, there may be cases where a function is called that doesn't exist. It makes sense on one page (the dependency is there) but not another. The difference is too slight to warrant forking the file into different versions. Instead, you can just check if the function exists before calling it to avoid the error: