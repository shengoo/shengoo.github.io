title: jQuery prepend class add class to first position
link: http://www.sheng00.com/1368.html
author: admin
description: 
post_id: 1368
created: 2014/08/12 09:56:37
created_gmt: 2014/08/12 01:56:37
comment_status: open
post_name: jquery-prepend-class-add-class-to-first-position
status: publish
post_type: post

# jQuery prepend class add class to first position

var prependClass = function (sel, strClass) {
      var $el = jQuery(sel);
      if ($el.hasClass(strClass)) {
        return;
      }
    
      /* prepend class */
      var classes = $el.attr('class');
      classes = strClass + ' ' + classes;
      $el.attr('class', classes);
    }