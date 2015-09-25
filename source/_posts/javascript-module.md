title: Javascript模块化
date: 2015-09-12 12:02:20
categories: javascript
tags: javascript
---
现下比较流行的模块化分为几大大阵营，一个是以RequireJS引领的AMD规范，还有就是以SeaJS为首的CMD规范，另外就是NodeJS引领的CommonJS规范。


当然YUI阵营为主的使用的是比较传统的对象字面量模块的方式，这种方案带来的命名空间的分层，痛苦在于太多的命名空间需要去管理。


CommonJS区别于AMD跟CMD的一点是，CommonJS 用在服务器端同步加载，AMD跟CMD用在浏览器端并且异步加载。


对于依赖的模块，AMD 是提前执行，CMD 是延迟执行.


AMD 的 API 默认是一个当多个用，CMD 的 API 严格区分，推崇职责单一。比如 AMD 里，require 分全局 require 和局部 require，都叫 require。CMD 里，没有全局 require，而是根据模块系统的完备性，提供 seajs.use 来实现模块系统的加载启动。CMD 里，每个 API 都简单纯粹。

所有的模块化标准都基于一些默认规范：
*	模块引用 - require
*	模块定义	- define
*	模块表示 - module




##AMD	(异步模块定义，Asynchronous Module Definition)
	
具有代表性Javascript库是[RequireJS](http://requirejs.org/)跟[CurlJS](https://github.com/unscriptable/curl)
*	define
	
```
	define(
		module_id,
		[dependencies],
		factory
	)
```
	*	module_id 是模块名，命名规则是[CommonJS模块命名规范的超集](http://wiki.commonjs.org/wiki/Modules/1.1.1#Module_Identifiers)
	*	[dependencies] 是当前定义的模块所以来的模块数组。
	*	factory 当模块初始化要执行的函数或者对象， 如果是函数则被执行，如果是对象则输出对象。
		
define使用	

```
	define('product',['jquery'], function($){
		var product = {
			add: function(item){
				//add a prouct
			}
		};
	});
```
	
*	require
	
```
	require(
		[module_id],
		factory
	)
```
*	[module_id] 当前模块以来的模块数组
*	factory 当模块初始化要执行的函数或者对象， 如果是函数则被执行，如果是对象则输出对象。
	
require使用

```
require(['product'],function(product){
		// use product module
		product.add({
			id: 0
		});
	});
```


###AMD的优势

*	模块定义都被封装了起来，帮我们避免了全局命名空间的污染。
*	比其它替代方案（例如 CommonJS，我们马上会讨论到）效果更好。没有跨域、本地或调试带来的问题，也不依赖于服务器端工具。大多数 AMD 加载器都支持在浏览器中加载模块，而不须要一个构建的过程。
*	提供了一个“传输”方法来用在单个文件中包含多个模块。其它例如 CommonJS 这样的方式都尚没有对传输格式达成共识。
*	当需要时可以进行延迟加载。

##CMD (通用模块定义, Common Module Definition)
	
以[SeaJS](http://seajs.org/)为代表，在推行SeaJS过程中定义的一种规范。
**在 CMD 规范中，一个模块就是一个文件**
	
*	define

```
define(factory)

define(id?, deps?, factory)

//例如：
define(function(require,exports,module){
	//do something
});
```
*	factory 为函数时，表示是模块的构造方法。执行该构造方法，可以得到模块向外提供的接口。factory 方法在执行时，默认会传入三个参数：require、exports 和 module
	
*	require

```
require(id)

//例如
define(function(require,exports,module){
	var $ = require('$');
	// do something
});

```
*	exports

在factory内部，exports 是一个对象，用来向外提供模块接口。

```
define(function(require,exports){
	var product = {
		add: function(){
		
	};
	
	exports.product = product;
});
```



###参考资料
*	[使用 AMD、CommonJS 及 ES Harmony 编写模块化的 JavaScript](http://justineo.github.io/singles/writing-modular-js/)
*	[CMD模块定义规范](https://github.com/seajs/seajs/issues/242)
*	[AMD定义规范](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))
*	[AMD 和 CMD 的区别有哪些](http://www.zhihu.com/question/20351507)