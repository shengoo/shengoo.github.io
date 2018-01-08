title: angularjs directive
link: http://www.sheng00.com/2001.html
author: admin
description: 
post_id: 2001
created: 2014/12/22 17:01:23
created_gmt: 2014/12/22 09:01:23
comment_status: open
post_name: angularjs-directive
status: publish
post_type: post

# angularjs directive

在AngularJS中，Dom操作应该在directive里进行，而不应该在controllers, services或者其他任何地方。 

### directives命名

  * 使用不重复的前缀 
    * 防止和其他人重复
    * 易读
  * 不要用ng-作为你的directive的前缀
  * 常见情况：两个单词 
    * AngularUI project 用的是 "ui-"

### 什么时候用directives?

  * 可复用的HTML控件 `<my-widget>`

  * 可复用的HTML行为 `<div ng-click="...">`

  * 包装一个jQuery插件 `<div ui-date></div>`

  * 你需要和DOM交互的绝大多数情况

## 创建一个directive

### 先给你的directive创建一个module

`angular.module('MyDirectives',[]);`

### 在你的app里加入directive module的依赖

`angular.module('app',['MyDirectives']);`

### 注册你的directive
    
    
    angular.module('MyDirectives')
    .directive('myDirective', function(){
      // TODO: 
    });
    

### 在HTML里使用你的directive

`<div my-directive>...</div>`

## Restrict参数

### 'A'

attributes `<div my-directive></div>`

### 'E'

element `<my-directive></my-directive`

### 'C' 'M'

rarely used 'C': classes 'M' : comments 

### 组合

`restrict: 'AE'`

## 隔离的scope

### directive默认是没有scope的，我们可以给它一个scope
    
    
    scope: {
      someParam: '='
    }
    

或者 `scope: true` **这个scope不会继承其他scope**

### scope参数

scope参数是从HTML的属性（attribute）传进来的 
    
    
    scope: {
      param1: '=', // 双向绑定（directive和controller）
      param2: '@', // 单向绑定
      param3: '&'  // 单向行为
    }
    
    
    
    <div my-directive
      param1="someVariable"
      param2="My name is {{name}}"
      param3="doSth()"
    >