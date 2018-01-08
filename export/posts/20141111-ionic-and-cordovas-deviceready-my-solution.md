title: Ionic and Cordova's DeviceReady - My Solution
link: http://www.sheng00.com/1506.html
author: admin
description: 
post_id: 1506
created: 2014/11/11 17:09:06
created_gmt: 2014/11/11 09:09:06
comment_status: open
post_name: ionic-and-cordovas-deviceready-my-solution
status: publish
post_type: post

# Ionic and Cordova's DeviceReady - My Solution

Folks know that I’ve been madly in love with the?[Ionic framework](http://ionicframework.com/)?lately, but I’ve run into an issue that I’m having difficulty with. I thought I’d blog about the problem and demonstrate a solution that worked for me. To be clear, I think my solution is probably?wrong. It works, but it just doesn’t?_feel_?right. I’m specifically sharing this blog entry as a way to start the discussion and get some feedback. On the slim chance that what I’m showing?_is_?the best solution… um… yes… I planned that. I’m brilliant. 

## The Problem

So let’s begin by discussing the problem. Given a typical Ionic app, your Angular code will have a .run method that listens for the ionicPlatform’s ready event. Here is an example from the “base” starter app (<https://github.com/driftyco/ionic-app-base/blob/master/www/js/app.js>):  
    
    
    // Ionic Starter App
    
    // angular.module is a global place for creating, registering and retrieving Angular modules
    // 'starter' is the name of this angular module example (also set in a attribute in index.html)
    // the 2nd parameter is an array of 'requires'
    angular.module('starter', ['ionic'])
    
    .run(function($ionicPlatform) {
      $ionicPlatform.ready(function() {
        // Hide the accessory bar by default (remove this to show the accessory bar above the keyboard
        // for form inputs)
        if(window.cordova && window.cordova.plugins.Keyboard) {
          cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);
        }
        if(window.StatusBar) {
          // Set the statusbar to use the default style, tweak this to
          // remove the status bar on iOS or change it to use white instead of dark colors.
          StatusBar.styleDefault();
        }
      });
    })

The ionicPlatform.ready event is called when Cordova’s deviceready event fires. When run on a desktop, it is fired when on window.load. Ok, so in my mind, this is where I’d put code that’s normally in a document.ready block. So far so good. Now let’s imagine you want to use a plugin, perhaps the Device plugin. Imagine you want to simply copy a value to $scope so you can display it in a view. If that controller/view is the first view in your application, you end up with a race condition. Angular is going to display your view and fire off ionicPlatform.ready asynchronously. That isn’t a bug of course, but it raises the question. If you want to make use of Cordova plugin features, and your application depends on it immediately, how do you handle that easily? One way would be to remove ng-app from the DOM and bootstrap Angular yourself. I’ve done that… once before and I see how it makes sense. But I didn’t want to use that solution this time as I wanted to keep using ionicPlatform.ready. I assumed (and I could be wrong!) that I couldn’t keep that and remove the ng-app bootstraping. So what I did was to add an intermediate view to my application. A simple landing page. I modified the stateProvider to add a new state and then made it the default. In my ionicPlatform.ready, I use the location service to do a move to the previously default state. 
    
    
    .run(function($ionicPlatform,$location,$rootScope) {
      $ionicPlatform.ready(function() {
        // Hide the accessory bar by default (remove this to show the accessory bar above the keyboard
        // for form inputs)
        if(window.cordova && window.cordova.plugins.Keyboard) {
          cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);
        }
        if(window.StatusBar) {
          // org.apache.cordova.statusbar required
          StatusBar.styleDefault();
        }
    
    	  $location.path('/tab/dash');
    	  $rootScope.$apply();
      });
    })

This seemed to do the trick. My controller code that’s run for the views after this was able to use Cordova plugins just fine. How about a real example? 

## The Demo

One of the more recent features to land in Ionic is?[striped-style tabs](http://ionicframework.com/docs/components/#striped-style-tabs). This is an Android-style tab UI and it will be applied automatically to apps running on Android. The difference is a bit subtle when the tabs are on the bottom: ![](/wp-content/uploads/2014/11/b1021.png) But when moved to the top using tabs-top, it is a bit more dramatic. ![](http://www.sheng00.com/wp-content/uploads/2014/11/05a5_tabsontop.png) Ok… cool. But I wondered – how can I get tabs on top?_just_?for Android? While I’m not one of those people who believe that UI elements have to be in a certain position on iOS versus Android, I was curious as to how I’d handle this programmatically. Knowing that it was trivial to check the Device plugin, and having a way now to delay the view until my plugins were loaded, I decided to use the approach described above to ensure I could access the platform before that particular view loaded. Here is the app.js file I used, modified from the tabs starter template. 
    
    
    // Ionic Starter App
    
    // angular.module is a global place for creating, registering and retrieving Angular modules
    // 'starter' is the name of this angular module example (also set in a attribute in index.html)
    // the 2nd parameter is an array of 'requires'
    // 'starter.services' is found in services.js
    // 'starter.controllers' is found in controllers.js
    angular.module('starter', ['ionic', 'starter.controllers', 'starter.services'])
    
    .run(function($ionicPlatform,$location,$rootScope) {
      $ionicPlatform.ready(function() {
        // Hide the accessory bar by default (remove this to show the accessory bar above the keyboard
        // for form inputs)
        if(window.cordova && window.cordova.plugins.Keyboard) {
          cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);
        }
        if(window.StatusBar) {
          // org.apache.cordova.statusbar required
          StatusBar.styleDefault();
        }
    
    	  $location.path('/tab/dash');
    	  $rootScope.$apply();
      });
    })
    
    .config(function($stateProvider, $urlRouterProvider) {
    
      // Ionic uses AngularUI Router which uses the concept of states
      // Learn more here: https://github.com/angular-ui/ui-router
      // Set up the various states which the app can be in.
      // Each state's controller can be found in controllers.js
      $stateProvider
    
        // setup an abstract state for the tabs directive
      	.state('home', {
    		url:"/home",
    		templateUrl:'templates/loading.html',
    		controller:'HomeCtrl'
    	})
        .state('tab', {
          url: "/tab",
          abstract: true,
          templateUrl: function() {
    		  if(window.device.platform.toLowerCase().indexOf("android") >= 0) {
    			  return "templates/tabs_android.html";			  
    		  } else {
    			  return "templates/tabs.html";
    		  }
    	  },
        })
    
        // Each tab has its own nav history stack:
    
        .state('tab.dash', {
          url: '/dash',
          views: {
            'tab-dash': {
              templateUrl: 'templates/tab-dash.html',
              controller: 'DashCtrl'
            }
          }
        })
    
        .state('tab.friends', {
          url: '/friends',
          views: {
            'tab-friends': {
              templateUrl: 'templates/tab-friends.html',
              controller: 'FriendsCtrl'
            }
          }
        })
        .state('tab.friend-detail', {
          url: '/friend/:friendId',
          views: {
            'tab-friends': {
              templateUrl: 'templates/friend-detail.html',
              controller: 'FriendDetailCtrl'
            }
          }
        })
    
        .state('tab.account', {
          url: '/account',
          views: {
            'tab-account': {
              templateUrl: 'templates/tab-account.html',
              controller: 'AccountCtrl'
            }
          }
        });
    
      // if none of the above states are matched, use this as the fallback
      $urlRouterProvider.otherwise('/home');
    
    });