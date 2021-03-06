---
layout: post
title: "Angular 控制器之间的数据传递"
date:   2015-08-05
subtitle: ""
author: "RryLee"
tags:
    - angular
---

这篇文章主要分享几个 Angular 中控制器之间数据传递的方法。

首先是从父控制器传递到子控制器，可以使用 $broadcast 这个方法。下面是 js 的代码：

    angular.module('app', [])
        .controller('ParentCtrl', ['$scope', function($scope) {
            $scope.message = 'Parent Controller';
            $scope.click = function() {
                $scope.$broadcast('update', $scope.message);
            }
        }])
        .controller('ChildCtrl', ['$scope', function($scope) {
            $scope.message = 'Child Controller';
            $scope.$on('update', function(event, message) {
               $scope.message = message;
            });
        }]);

---

在子控制器中使用 $on 即可接受到父作用域的数据。[Codepen](http://codepen.io/RryLee/pen/YXBGyp) 可以查看 demo 演示。

相反，我们从子控制器传递数据到父控制器也是可以的，虽然一般 angular 都是向下传播，但是某些时候我们会希望使数据向上传播，我们就可以在子控制器中使用 $emit 这个方法

    angular.module('app', [])
        .controller('ParentCtrl', ['$scope', function($scope) {
            $scope.alert = {msg: 'alert1'};
            $scope.$on('update', function(event, alert) {
                $scope.alert = alert;
            });
        }])
        .controller('ChildCtrl', ['$scope', function($scope) {
            $scope.click = function() {
            $scope.alert.msg = $scope.msg;
                $scope.$emit('update', $scope.alert);
            }
        }]);

---

完整实例请看 [codepen](http://codepen.io/RryLee/pen/MwLjex).

最后是两个不属于上下级关系的控制器中间的数据传递，通过 $rootScope 和 $broadcast 来完成。

    angular.module('app', [])
        .controller('OneCtrl', ['$scope', '$rootScope', function($scope, $rootScope) {
            $scope.message = 'This is OneCtrl';
            $rootScope.$on('update', function(event, message) {
                $scope.message = message;
            });
        }])
        .controller('TwoCtrl', ['$scope', '$rootScope', function($scope, $rootScope) {
            $scope.message = 'update';
            $rootScope.click = function() {
                $rootScope.$broadcast('update', $scope.message);
            }
        }]);

---

[codepen](http://codepen.io/RryLee/pen/BNMLWr)，不过最后这种做法会污染全局空间，不推荐，至于为什么。。。听说的，反正数据都不要跟全局作用域扯上关系就最好了。
