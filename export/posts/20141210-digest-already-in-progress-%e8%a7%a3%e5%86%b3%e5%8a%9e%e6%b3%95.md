title: $digest already in progress 解决办法
link: http://www.sheng00.com/1918.html
author: admin
description: 
post_id: 1918
created: 2014/12/10 14:14:40
created_gmt: 2014/12/10 06:14:40
comment_status: open
post_name: digest-already-in-progress-%e8%a7%a3%e5%86%b3%e5%8a%9e%e6%b3%95
status: publish
post_type: post

# $digest already in progress 解决办法

## 常见原因

除了简单的不正确调用 `$apply` 或 `$digest`,有些情况下，即使没有犯错，也有可能得到这个错误。 

### 可能出错的代码
    
    
    function MyController($scope, thirdPartyComponent) {
      thirdPartyComponent.getData(function(someData) {
        $scope.$apply(function() {
          $scope.someData = someData;
        });
      });
    }

### 改成这样就可以了 
    
    
    function MyController($scope, thirdPartyComponent) {
      thirdPartyComponent.getData(function(someData) {
        $timeout(function() {
          $scope.someData = someData;
        }, 0);
      });
    }