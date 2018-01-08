title: 使用angularjs directive生成api方法供其他地方调用angularjs directive expose api
link: http://www.sheng00.com/2009.html
author: admin
description: 
post_id: 2009
created: 2014/12/30 12:52:14
created_gmt: 2014/12/30 04:52:14
comment_status: open
post_name: %e4%bd%bf%e7%94%a8angularjs-directive%e7%94%9f%e6%88%90api%e6%96%b9%e6%b3%95%e4%be%9b%e5%85%b6%e4%bb%96%e5%9c%b0%e6%96%b9%e8%b0%83%e7%94%a8angularjs-directive-expose-api
status: publish
post_type: post

# 使用angularjs directive生成api方法供其他地方调用angularjs directive expose api

有些时候我们需要directive生成api，可以在其他地方(controller)调用 ![image1419911269](/wp-content/uploads/2014/12/image1419911269.png) 下面介绍下简单的步骤： 

### 使用directive的双向绑定绑定controller里的变量

html: `<div expose="exposedApi"></div>` js: 
    
    
    directive('expose',function(){
      return {
        restrict: "A",
        scope: {
          api: "=expose"
        }
      };
    

这个时候controller离的exposedApi变量和directive里的api是双向绑定的 

### 给directive里的api增加可调用的方法
    
    
    directive('expose',function(){
      return {
        restrict: "A",
        scope: {
          api: "=expose"
        },
        controller: function($scope){
          $scope.number = 0;
          $scope.api={
            count:function(){
              $scope.number ++;
            }
          };
        },
        template: '<div class="well">' +
                  '<p>count: {{number}}</p>' +
                  '</div>'
      };
    

### 调用directive里的方法
    
    
    controller("ctrl",function($scope){
      $scope.count = function(){
        $scope.exposedApi.count();
      };
    })
    

### Demo:

[http://shengoo.github.io/angularjs-practice](http://shengoo.github.io/angularjs-practice/directive/exposeapi.html)

### 完整代码：
    
    
    <!DOCTYPE html>
    <html ng-app="app">
    <head lang="en">
      <meta charset="UTF-8">
      <title></title>
      <link rel="stylesheet" href="../bower_components/bootstrap/dist/css/bootstrap.css" />
      <script src="../bower_components/angular/angular.js"></script>
    </head>
    <body ng-controller="ctrl">
    <div class="container">
    <div expose="exposedApi"></div>
    <a ng-click="count()" class="btn btn-primary">click</a>
    <div expose="exposedApi2"></div>
    <a ng-click="count2()" class="btn btn-primary">click</a>
    </div>
    <script>
    angular.module("app",[])
    .controller("ctrl",function($scope){
      $scope.count = function(){
        $scope.exposedApi.count();
      };
      $scope.count2 = function(){
        $scope.exposedApi2.count();
      };
    })
    .directive('expose',function(){
      return {
        restrict: "A",
        scope: {
          api: "=expose"
        },
        controller: function($scope){
          $scope.number = 0;
          $scope.api={
            count:function(){
              $scope.number ++;
            }
          };
        },
        template: '<div class="well">' +
                  '<p>count: {{number}}</p>' +
                  '</div>'
      };
    })
    </script>
    </body>
    </html>