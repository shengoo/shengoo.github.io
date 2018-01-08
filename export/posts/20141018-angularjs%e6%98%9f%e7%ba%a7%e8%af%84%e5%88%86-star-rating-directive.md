title: angularjs星级评分 star rating directive
link: http://www.sheng00.com/1481.html
author: admin
description: 
post_id: 1481
created: 2014/10/18 10:44:26
created_gmt: 2014/10/18 02:44:26
comment_status: open
post_name: angularjs%e6%98%9f%e7%ba%a7%e8%af%84%e5%88%86-star-rating-directive
status: publish
post_type: post

# angularjs星级评分 star rating directive

### directive
    
    
    var app = angular.module("app", []);
    app.controller('ctrl',function($scope){
      $scope.max = 5;
      $scope.ratingVal = 2;
      $scope.readonly = false;
      $scope.onHover = function(val){
        $scope.hoverVal = val;
      };
      $scope.onLeave = function(){
        $scope.hoverVal = null;
      }
      $scope.onChange = function(val){
        $scope.ratingVal = val;
      }
    
    });
    app.directive('star', function () {
      return {
        template: '<ul class="rating" ng-mouseleave="leave()">' +
            '<li ng-repeat="star in stars" ng-class="star" ng-click="click($index + 1)" ng-mouseover="over($index + 1)">' +
            '\u2605' +
            '</li>' +
            '</ul>',
        scope: {
          ratingValue: '=',
          max: '=',
          readonly: '@',
          onHover: '=',
          onLeave: '='
        },
        controller: function($scope){
          $scope.ratingValue = $scope.ratingValue || 0;
          $scope.max = $scope.max || 5;
          $scope.click = function(val){
            if ($scope.readonly && $scope.readonly === 'true') {
              return;
            }
            $scope.ratingValue = val;
          };
          $scope.over = function(val){
            $scope.onHover(val);
          };
          $scope.leave = function(){
            $scope.onLeave();
          }
        },
        link: function (scope, elem, attrs) {
          elem.css("text-align", "center");
          var updateStars = function () {
            scope.stars = [];
            for (var i = 0; i < scope.max; i++) {
              scope.stars.push({
                filled: i < scope.ratingValue
              });
            }
          };
          updateStars();
    
          scope.$watch('ratingValue', function (oldVal, newVal) {
            if (newVal) {
              updateStars();
            }
          });
          scope.$watch('max', function (oldVal, newVal) {
            if (newVal) {
              updateStars();
            }
          });
        }
      };
    });
    

### css:
    
    
    .rating {
      color: #a9a9a9;
      margin: 0;
      padding: 0;
    }
    ul.rating {
      display: inline-block;
    }
    .rating li {
      list-style-type: none;
      display: inline-block;
      padding: 1px;
      text-align: center;
      font-weight: bold;
      cursor: pointer;
    }
    .rating .filled {
      color: #ffee33;
    }
    

### html:
    
    
    <div ng-app="app">
    <div class="well" ng-controller="ctrl">
      <div star rating-value="ratingVal" max="max" on-hover="onHover" on-leave="onLeave" readonly="{{readonly}}"></div>
      <div>
        Max: <input type="number" name="input" ng-model="max" min="0" max="99" required>
        <p>current value: {{ratingVal}}</p>
        <p>hover on : {{hoverVal?hoverVal:"none"}}</p>
        <p>readonly : <input type="checkbox"
           ng-model="readonly"></p>
      </div>
    </div>
    </div>
    

### github page

<http://shengoo.github.io/angularjs-practice/directive/star/star.html>

### jsfiddle:

### code pen:

See the Pen [angularjs star rating directive](http://codepen.io/shengoo/pen/gbLRZJ/) by Qing Sheng ([@shengoo](http://codepen.io/shengoo)) on [CodePen](http://codepen.io).