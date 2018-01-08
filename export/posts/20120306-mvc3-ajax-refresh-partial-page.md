title: mvc3 ajax refresh partial page 
link: http://www.sheng00.com/333.html
author: admin
description: 
post_id: 333
created: 2012/03/06 14:37:27
created_gmt: 2012/03/06 06:37:27
comment_status: open
post_name: mvc3-ajax-refresh-partial-page
status: publish
post_type: post

# mvc3 ajax refresh partial page 

$.get('@(Url.Action("HeaderLinks", "Common" ))', function (data) {
                $('#header-links-wrapper').html(data);
            });