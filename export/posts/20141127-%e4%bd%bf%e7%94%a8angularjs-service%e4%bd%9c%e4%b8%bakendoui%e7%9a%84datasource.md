title: 使用AngularJS service作为KendoUI的datasource
link: http://www.sheng00.com/1837.html
author: admin
description: 
post_id: 1837
created: 2014/11/27 20:08:45
created_gmt: 2014/11/27 12:08:45
comment_status: open
post_name: %e4%bd%bf%e7%94%a8angularjs-service%e4%bd%9c%e4%b8%bakendoui%e7%9a%84datasource
status: publish
post_type: post

# 使用AngularJS service作为KendoUI的datasource

angular.module("app", ["kendo.directives"])
    .controller("news", function($scope,newsService) {
      var dataSource = new kendo.data.DataSource({
        transport: {
          read: dataSourceRead
        }
      });
      
      function dataSourceRead(options){
        //todo: show loading
        newsService.getByCategory($scope.selectedCategory.value)
          .then(
            function(response){
              options.success(response);
              //todo: hide loading
            },
            function(response){
              options.error(response);
              //todo: handle errors.
            });
      }
     
      $scope.newsListViewOptions = {
        dataSource: dataSource
      };
    })
    .service('newsService', function($q, $http) {
     
      this.getByCategory = function(category){
        var url = "your url";
     
        var request = $http({
          method: "jsonp",
          url: url
        });
     
        return( request.then( handleSuccess, handleError ) );
      };
      
      function handleError( response ) {
        //if no message return from server
        if (
          ! angular.isObject( response.data ) ||
          ! response.data.message
          ) {
     
          return( $q.reject( "An unknown error occurred." ) );
     
        }
     
        return( $q.reject( response.data.message ) );
     
      }
     
     
      function handleSuccess( response ) {
        return( response.data );
      }
     
    });