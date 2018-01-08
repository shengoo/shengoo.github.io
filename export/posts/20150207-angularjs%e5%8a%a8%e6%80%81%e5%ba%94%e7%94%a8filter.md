title: AngularJS动态应用filter
link: http://www.sheng00.com/2065.html
author: admin
description: 
post_id: 2065
created: 2015/02/07 00:59:19
created_gmt: 2015/02/06 16:59:19
comment_status: open
post_name: angularjs%e5%8a%a8%e6%80%81%e5%ba%94%e7%94%a8filter
status: publish
post_type: post

# AngularJS动态应用filter

有的时候我们在动态生成页面内容的时候，需要动态应用filter，这里和大家分享一下方法 

### 假如我们有这样一组数据
    
    
    [
      {val:"text"},
      {val:"upper text",filter:"uppercase"},
      {val:new Date(),filter:"date",formatter:"yyyy-MM-dd"}
    ]
    

数据的值和格式都是动态的 这时候我们需要再写一个filter去动态应用数据的格式 

### 动态应用filter和filter格式的filter
    
    
    angular.module("app",[])
    .filter('use_filter', function ($filter) {
      return function (value, filterName, formatter) {
        return filterName ?
                (formatter ?
                    $filter(filterName)(value, formatter) :
                    $filter(filterName)(value)) :
                value;
      };
    });
    

### 使用的时候：

`{{item.val| use_filter:item.filter:item.formatter}}`

### 全部代码：
    
    
    <!DOCTYPE html>
    <html ng-app="app">
    <head lang="en">
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">
        <script src="http://cdn.staticfile.org/angular.js/1.3.0-beta.13/angular.js"></script>
    </head>
    <body ng-controller="ctrl">
    <div class="container">
        <ul>
            <li ng-repeat="item in data">
                <span>{{item| json}}</span>{{item.val| use_filter:item.filter:item.formatter}}
            </li>
        </ul>
    </div>
    <script>
    angular.module("app",[])
    .controller("ctrl",function($scope){
        $scope.data = [
            {val:"text"},
            {val:"upper text",filter:"uppercase"},
            {val:new Date(),filter:"date",formatter:"yyyy-MM-dd"}
        ];
    })
    .filter('use_filter', function ($filter) {
        return function (value, filterName, formatter) {
            return filterName ?
                    (formatter ?
                        $filter(filterName)(value, formatter) :
                        $filter(filterName)(value)) :
                    value;
        };
    });
    </script>
    </body>
    </html>
    

### 直接运行代码：

  * {{item| json}}{{item.val| use_filter:item.filter:item.formatter}}