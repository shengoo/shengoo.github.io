title: 在AngularJS的使用$apply更新model
link: http://www.sheng00.com/1070.html
author: admin
description: 
post_id: 1070
created: 2014/02/14 14:20:56
created_gmt: 2014/02/14 06:20:56
comment_status: open
post_name: %e5%9c%a8angularjs%e7%9a%84%e4%bd%bf%e7%94%a8apply%e6%9b%b4%e6%96%b0model
status: publish
post_type: post

# 在AngularJS的使用$apply更新model

先看一个不能work的  如果ng-app和ng-controller写在一个dom里，这样就不能更新model里的值 分开写就没问题 解决这个问题可以这样：  当然也可以这样： 
    
    
    function Ctrl($scope) {
      $scope.message = "Waiting 2000ms for update";
        
        setTimeout(function () {
            $scope.message = "Timeout called!";
            $scope.$apply();
        }, 2000);
    }