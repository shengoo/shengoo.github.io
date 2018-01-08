title: angularjs shared module
link: http://www.sheng00.com/1839.html
author: admin
description: 
post_id: 1839
created: 2014/12/03 14:37:35
created_gmt: 2014/12/03 06:37:35
comment_status: open
post_name: angularjs-shared-module
status: publish
post_type: post

# angularjs shared module

"use strict";
     
    // make a common module
    angular.module("common",[])
    .filter("someFilter", function (){
      return function (text) {
        return text;
      };
    });
     
    // use it
    angular.module("app",["common"]);