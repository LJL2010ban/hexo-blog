title: 服务定义的简短指南
date: 2015-07-07 22:15:59
categories: angularjs
tags: [angularjs,service,javascript]
---
service即服务，提供了一种能在应用的整个生命周期内保持数据的方法，能够在控制器之间进行通信，并且保持数据的一致性。

服务是一个单例对象，在每个应用中只会被实例一次（被$injector实例化的），并且是延迟加载（需要时才会被创建）。

服务提供了把特定功能相关联的方法集中在一起的接口。

angularjs自身提供了非常多的服务让我们使用，常用的有$http,$timeout,$interval,$q,$rootScope等等。下载了Dash应用的童鞋可以方便的看到dash文档整理好的资料清除的罗列了出来。

除了angularjs提供的以为，使用最多的还是自己根据业务需要自定义服务。而angularjs提供了5种方式来定义服务：

##factory()
**是创建和配置服务的最快捷方式**

此方式定义的服务返回一个包含服务函数跟服务数据的对象。angularjs中也有使用此方式实现的服务，例如:$http,$q.

```
//定义
angular.module('myApp.services')
  .factory('User', function($http) {
  	var backendUrl = 'http://localhost:3000';
  	var service = {
  	  user:{},
  	  setName: function(name) {
  	    service.user['name'] = name;
  	  },
  	  setEmail: function(email) {
  	    service.user['email'] = email;
  	  }
  	};
  });
  return service;
  
  //使用
  angular.module('myApp')
  .controller('MainCtrl', function($scope, User) {
    $scope.setName = User.setName;
  });
  
```
**注**
*	当我们仅仅是定义一些方法的集合、数据并且不需要处理很复杂的业务时，用factory()来定义服务是非常好的一个选择。
*	若想要在.config() 中对服务进行配置时，不能使用factroy()来定义服务。


##service()
该方式可以注册一个支持构造函数的服务，允许我们为服务对象注册一个构造函数。

```
//定义
angular.module('myApp.services')
  .service('User', function($http) {
  	var self = this;
  	this.user = {};
  	this.backendUrl = 'http://localhost:3000';
  	this.setName = function(name) {
  		self.user['name'] = name;
  	};
  });
  
//使用
angular.module('myApp')
.controller('MainCtrl', function($scope, User){
  $scope.setName = User.setName;
});

```
**注**

使用service()方式是处理复杂的业务逻辑的是不错的选择。

##provider()
所有的服务工厂都是由$provicde服务创建的，$provide服务负责在运行时初始化这些提供者。

提供者是一个具有$get()方法的对象，$injector通过调用$get()创建服务实例。

```
//定义
angular.module('myApp.services')
  .provider('User', function(){
    this.backendUrl = 'http://localhost:3000';
    this.setBackendUrl = function(url) {
      if(url) this.backendUrl = url;
    };
    //$get
    this.$get = function($http) {
      var self = this;
      var service = {
      	user: {},
      	setName: function(name){
      	  service.user['name'] = name;
      	}
      };
      return service;
    };
  });
//使用
angular.module('myApp)
.config(function(UserProvider){
  UserProvider.setBackendUrl('http://test.com/api');
});

angular.module('myApp')
.controller('MainCtrl', function($scope, User){
  $scope.setName = User.setName;
});

```
**注**
使用$provide()实际创建了一个提供者，这个提供者在定义是没有Provider后缀，但是在config()使用时，需要加上xxxProvider.


##constant()
可以将一个已经存在的变量值注册为服务，并将其注入到应用的其他部分当中。

```
//定义
angular.module('myApp')
.constant('accessToken','guid-xx-xxxx-xxxx');

//使用
angular.module('myApp')
.controller('myController', function($scope,accessToken){
	$scope.accessToken = accessToken;
});
```
**注**
这个常量不能被装饰器拦截

##value()
如果服务的$get()方法返回的是个常量，就没有必要像上面那样定义那么复杂的完整服务。

```
angular.module('myApp').value('accessToken', 'guid-xx-xxx-xxx');

```

##constant()跟value()的区别
以constant方式创建的变量可以注意到配置函数中。value()不可以，一般用value()来注册对象或者函数。

---
参考资料：

[The short guide to service definitions](http://www.ng-newsletter.com/advent2013/#!/day/1)

[ Developer Guide / Services](https://docs.angularjs.org/guide/services)





