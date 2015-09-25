title: angular.JS的controller之间如何正确的通信
date: 2015-07-02 09:44:04
categories: angularjs
tags: [angularjs,javascript,experience]
---
AngularJS中的controller是个函数，用来向视图的作用域（$scope）添加额外的功能，我们用它来给作用域对象设置初始状态，并添加自定义行为。

当我们在创建新的控制器时，angularJS会帮我们生成并传递一个新的$scope对象给这个controller,在angularJS应用的中的任何一个部分，都有父级作用域的存在，顶级就是ng-app所在的层级，它的父级作用域就是$rootScope。

每个$scope的$root指向$rootScope, $cope.$parent指向父级作用域。

cotroller之间的通信本质上是当前的controller所在的$scope如何跟其他controller上的$scope进行通信。

通常有3中解决方式：

*	利用作用域继承的原理，子控制器访问父级控制器中的内容。
*	使用angularJS中的事件，也就是使用$on,$emit,$broadcast进行消息传递
*	使用angularJS中的服务

##第一种方式
即作用域嵌套作用域，有一定的使用限制，需要作用域嵌套起来，在实际开发中这种场景相对比较少，但也不是没有，这种方式更简单直接。

angularJS中默认情况下，当前作用域中无法找到某个属性时，就会在父级作用域中进行查找，若找不到直至查找到$rootScope。 如果在$rootScope中也无法找到程序依旧运行，但视图不会更新。

**示例**

```
	//Javascript
	app.controller('ParentController', function($scope) { 
		$scope.person = {greeted: false};	});	app.controller('ChildController', function($scope) {	 	$scope.sayHello = function() {    	     $scope.person.name = 'Ari Lerner';    	};	});
	//HTML
	 <div ng-controller="ParentController">       <div ng-controller="ChildController">         <a ng-click="sayHello()">Say hello</a>       </div>       {{ person }}     </div>
	//result    {"greeted":true, "name": "Ari Lerner"}

```

##第二种方式
因为作用域是有层次的，所以可以利用作用域链传递事件。

传递事件有2种方式：
*	$broadcast: 触发的事件要通知整个事件系统（允许任意作用域处理这个事件）就要向下传播。
*	$emit: 如果要提醒一个全局模块，需要通知更高层次的作用域时（例如$rootscope）需要把事件向上传递。

作用域上使用$on进行事件监听。

**示例**

```
	app.controller('ParentController', function($scope) { 
		$scope.$on('$fromSubControllerClick', function(e,data){
			console.log(data); // hello
		});
	});
	app.controller('ChildController', function($scope) {
	 	$scope.sayHello = function() {
	 		$scope.$emit('$fromSubControllerClick','hello');
    	};
	});
	//HTML
	 <div ng-controller="ParentController">
       <div ng-controller="ChildController">
         <a ng-click="sayHello()">Say hello</a>
       </div>
     </div>
```

在这里想要说的另外一个问题就是事件传播的性能问题，$broadcast+$on的方式回通知所有的子作用域，这里就会有性能问题，所以推荐使用$emit+$on的方式,为了进一步提升性能，定义的事件处理函数要在作用域销毁时一起释放掉。

使用$emit+$on的方式需要我们将事件监听绑定在$rootScope上，例如：

```
angular
    .module('MyApp')
    .controller('MyController', ['$scope', '$rootScope', function MyController($scope, $rootScope) {

            var unbind = $rootScope.$on('someComponent.someCrazyEvent', function(){
                console.log('foo');
            });

            $scope.$on('$destroy', unbind);
        }
    ]);
```

但是这种方式有点繁琐，定义多个事件处理函数时整个人都不好了，所以我们来改进一下

利用装饰器来定义一个新的事件绑定函数：

```
angular
    .module('MyApp')
    .config(['$provide', function($provide){
        $provide.decorator('$rootScope', ['$delegate', function($delegate){

            Object.defineProperty($delegate.constructor.prototype, '$onRootScope', {
                value: function(name, listener){
                    var unsubscribe = $delegate.$on(name, listener);
                    this.$on('$destroy', unsubscribe);

                    return unsubscribe;
                },
                enumerable: false
            });


            return $delegate;
        }]);
    }]);
```

那么我们在控制器中定义事件处理函数时：

```
angular
    .module('MyApp')
    .controller('MyController', ['$scope', function MyController($scope) {

            $scope.$onRootScope('someComponent.someCrazyEvent', function(){
                console.log('foo');
            });
        }
    ]);
```

**个人强烈推荐此种做法**


##第三种方式
利用angularJS中service单例模式的特性，服务(service)提供了一种能在应用的整个生命周期内保持数据的方式，能够在控制器之间进行通信，且能保证数据的一致性。

一般我们都会封装server来为应用提供访问数据的接口，或者跟远程进行数据交互。

**示例**

```
var myApp = angular.module("myApp", []);
myApp.factory('Data', function() {
  return {
    name: "Ting"
  }
});
myApp.controller('FirstCtrl', function($scope, Data) {
  $scope.data = Data;

  $scope.setName = function() {
    Data.name = "Jack";
  }
});

myApp.controller('SecondCtrl', function($scope, Data) {
  $scope.data = Data;

  $scope.setName = function() {
    Data.name = "Moby";
  }
});
```





##参考资料

*	[whats the correct way to conmmunicate between controllers](http://stackoverflow.com/questions/11252780/whats-the-correct-way-to-communicate-between-controllers-in-angularjs/19498009#19498009)

*	[controller间共享数据](http://www.angularjs.cn/A07b)
*	[controller间如何通信](http://segmentfault.com/a/1190000000639592)


