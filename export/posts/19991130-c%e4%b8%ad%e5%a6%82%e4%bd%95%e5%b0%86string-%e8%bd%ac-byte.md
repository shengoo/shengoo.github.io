title: c#中如何将string 转 byte
link: http://www.sheng00.com/48.html
author: admin
description: 
post_id: 48
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: c%e4%b8%ad%e5%a6%82%e4%bd%95%e5%b0%86string-%e8%bd%ac-byte
status: publish
post_type: post

# c#中如何将string 转 byte

System.Text.Encoding.Default.GetBytes(string);

反之亦然

System.Text.Encoding.Default.GetString(byte);