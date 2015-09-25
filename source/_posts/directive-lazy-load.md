title: 'directive:lazy-load'
date: 2015-06-19 09:55:20
categories: angularjs
tags: [angularjs,directive]
---
#自定义指令:图片延迟加载


###前言

web App跟web毕竟是不同，考虑到用户在使用web app时的数据流量，已经首次加载速度，所以对于页面的一些图片采用延迟加载还是很必要的，下面记录下自己开发延迟加载指令的过程。

###实现思路

图片肯定有所以来的容器元素，容器元素在屏幕上的可视范围内的图片要加载进来，所以需要监听容器的滚动事件，计算出当前滚动的位置跟图片的位置判断是否加载图片。

我在开发该指令时，因为项目中已经有个在图片未加载完成是显示loading条的指令，所以我直接在此基础上进行扩展，目的是对使用该指令的图片进行延迟记在，页面上基本不用改动。

##指令开发

*	容器指令

	只是用来标记图片所在的容器
	
	```
	myApp.directive('yxjImageContainer', function($compile){
  		return {
	    	restrict: 'AC',
	    	controller: ['$scope', '$element', function($scope,$element){
    	  		$element.data('yxjImageContainer', $element);
    		}]
  		};
	});
	```

*	图片延迟加载指令

	**实现思路**
	
	*	找到容器元素
	
	```
	var container = element.inheritedData('yxjImageContainer');
	```
	*	需要知道容器的滚动距离
	
	```
     	//获取容器的滚动距离
        var _getContainerScrollTop = function() {
          if(container.scrollTop && container.scrollTop()) {
            return container.scrollTop();
          }
          var first = container[0];
          if (first && first.pageYOffset !== undefined) {
            return first.pageYOffset;
          }
          else if (first && first.scrollTop) {
            return first.scrollTop;
          }
          return document.documentElement.scrollTop || 0;
        };
	```
	*	容器的高度
	
	```
		 var _getContainerInnerHeight = function() {
          if(container.innerHeight) {
            return container.innerHeight;
          }

          var first = container[0];
          if(first && first.innerHeight) {
            return first.innerHeight;
          } else if(first && first.clientHeight) {
            return first.clientHeight;
          }
          return document.documentElement.clientHeight || 0;
        };
	```
	*	图片元素所在位置
	
	```
    	//获取元素top
        var _getElementOffset = function() {
          if(element.offset){
            return element.offset().top;
          }
          var box = element[0].getBoundingClientRect();
          return box.top + _getContainerScrollTop() - document.documentElement.clientTop;
        };
	```
	*	监听容器的滚动事件，判断当前图片元素是否需要加载
	
	```
        var _onViewChange = function(bool) {
          var height = _getContainerInnerHeight(),
              scroll = _getContainerScrollTop(),
              eleOffset = container[0] === $window ? _getElementOffset() : _getElementOffsetContainer(),
              windownBottom = container[0] === $window ? height + scroll: height;

          var remaining = eleOffset - windownBottom,
              shouldLoad = remaining <= offset;
          if(shouldLoad && !loaded) {
            _renderImage();
          }
        };
        
        container.on('scroll', _onViewChange);
	```
	*	加载图片并显示，取消容器的滚动事件
	
	```
	//加载图片
        var _renderImage = function() {
          loaded = true;
          var imageDom = angular.element(element[0].querySelector('img'));
          imageDom[0].src = attrs['ngSrc'];

          imageDom.on('load', function() {
            element.removeClass('loading');
            imageDom.css('visibility', 'visible');
          }).on('error', function() {
            element.addClass('loading');
            imageDom.css('visibility', 'hidden');
          });
          container && container.off('scroll', _onViewChange);
        };
	```

**完整demo** [gthub](https://github.com/yuanxj1024/angular-lazy-load-driective)


###遇到的问题
*	angular中操作dom
	
	angular中支持jqLite；通过document.getXXX()等方法获取的元素需要使用angular.element()装换成angular中的对象
	
	[angular.element](https://docs.angularjs.org/api/ng/function/angular.element)
	
	
###参考资料

*	很强大的一个[image-lazy-load](https://github.com/afklm/ng-lazy-image)
