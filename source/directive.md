title: directive
date: 2015-07-13 14:33:58
categories:
tags:
---

##定义指令

*	写法一
	
	```
	angular.module('myApp', [])
	  .directive('myDirective', function($timeout) {
	  	//定义指令
	  });
	```

*	写法二
	
	```
	angular.module('myApp', [])
	  .directive('myDirective', ['$timeout', function($timeout){
	  	//定义指令
	  }]);
	```












参考资料:
*	[AngularJs学习笔记--directive](http://www.cnblogs.com/lcllao/archive/2012/09/09/2677190.html)
*	[Creating Custom Directives](https://docs.angularjs.org/guide/directive)

