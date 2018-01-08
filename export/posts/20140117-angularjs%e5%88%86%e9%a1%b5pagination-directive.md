title: AngularJs分页pagination directive
link: http://www.sheng00.com/1051.html
author: admin
description: 
post_id: 1051
created: 2014/01/17 13:49:05
created_gmt: 2014/01/17 05:49:05
comment_status: open
post_name: angularjs%e5%88%86%e9%a1%b5pagination-directive
status: publish
post_type: post

# AngularJs分页pagination directive

### html
    
    
    <div ng-app="hello">
        <div ng-controller="pagingCtrl">
            <paging>
                <table class="table table-striped table-bordered table-hover">
                    <tr>
                        <th>id</th>
                        <th>name</th>
                    </tr>
                    <tr ng-repeat="item in data">
                        <td>{{item.id}}</td>
                        <td>{{item.name}}</td>
                    </tr>
                </table>
                <ul class="pagination" num-pages="tasks.pageCount" current-page="tasks.currentPage" on-select-page="selectPage(page)">
                    <li ng-class="{disabled: noPrevious()}"> <a ng-click="selectPrevious()">&laquo;</a>
    
                    </li>
                    <li ng-repeat="page in pages" ng-class="{active: isActive(page)}"> <a ng-click="selectPage(page)">{{page}}</a>
    
                    </li>
                    <li ng-class="{disabled: noNext()}"> <a ng-click="selectNext()">&raquo;</a>
    
                    </li>
                </ul>
            </paging>
        </div>
    </div>

### js
    
    
    var myModule = angular.module('hello', []);
    myModule.controller('pagingCtrl', function ($scope, $http) {
        $scope.data = [{
            id: 1,
            name: "a"
        }, {
            id: 2,
            name: "b"
        }];
        $scope.currentPage = 1;
        $scope.numPages = 5;
        $scope.pageSize = 10;
        $scope.pages = [];
        //get first page
        /*$http.get('url',
                    {
                        method: 'GET',
                        params: {
                            'pageNo': $scope.currentPage,
                            'pageSize': $scope.pageSize
                        },
                        responseType: "json"
                    }).then(function (result) {
                        $scope.data = result.data.Data;
                        $scope.numPages = Math.ceil(result.data.Total / result.data.PageSize);
                    });*/
        $scope.onSelectPage = function (page) {
            //replace your real data
            /*$http.get('url',
                    {
                        method: 'GET',
                        params: {
                            'pageNo': page,
                            'pageSize': $scope.pageSize
                        },
                        responseType: "json"
                    }).then(function (result) {
                        $scope.data = result.data.Data;
                        $scope.numPages = Math.ceil(result.data.Total / result.data.PageSize);
                    });*/
        };
    });
    
    myModule.directive('paging', function () {
        return {
            restrict: 'E',
            //scope: {
            //    numPages: '=',
            //    currentPage: '=',
            //    onSelectPage: '&'
            //},
            template: '',
            replace: true,
            link: function (scope, element, attrs) {
                scope.$watch('numPages', function (value) {
                    scope.pages = [];
                    for (var i = 1; i <= value; i++) {
                        scope.pages.push(i);
                    }
                    alert(scope.currentPage)
                    if (scope.currentPage > value) {
                        scope.selectPage(value);
                    }
                });
                scope.isActive = function (page) {
                    return scope.currentPage === page;
                };
                scope.selectPage = function (page) {
                    if (!scope.isActive(page)) {
                        scope.currentPage = page;
                        scope.onSelectPage(page);
                    }
                };
                scope.selectPrevious = function () {
                    if (!scope.noPrevious()) {
                        scope.selectPage(scope.currentPage - 1);
                    }
                };
                scope.selectNext = function () {
                    if (!scope.noNext()) {
                        scope.selectPage(scope.currentPage + 1);
                    }
                };
                scope.noPrevious = function () {
                    return scope.currentPage == 1;
                };
                scope.noNext = function () {
                    return scope.currentPage == scope.numPages;
                };
    
            }
        };
    });
    

### jsfiddle