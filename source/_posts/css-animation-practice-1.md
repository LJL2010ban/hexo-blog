title: css动画学习-立方体
date: 2015-06-26 09:41:34
categories: css
tags: [css3,animation]
---
**思路**
一个正方体有6个面，所以我们需要个div中包含6个div，在3d模式下，z轴偏移出部分距离，然后6个面分别围绕x轴，Y轴旋转90deg,或者180deg即可，若使立方体旋转起来，让容器旋转起来就ok了。


##实现步骤
1.	容器.container
	*	容器的position设置为absolute,方便将容器定位，留给3d足够的显示空间
	*	设置perspective为400px,给3d足够的视图距离
	
	```
	定义和用法
	perspective 属性定义 3D 元素距视图的距离，以像素计。该属性允许您改变 3D 元素查看 3D 元素的视图。
	当为元素定义 perspective 属性时，其子元素会获得透视效果，而不是元素本身。
	注释：perspective 属性只影响 3D 转换元素。
	```
2.	创建立方体div.square包含6个div

	```
	emmet语法:
	div.square>div{$}*6
	```
3.	设置容器.square样式
	*	transform-origin 设置原点为50%
	*	transform-style: preserve-3d 设置3d显示模式
	*	设置6个面的position为absolute,因为6个面要进行3d移动定位
4.	设置正前方的面
	*	这个面很简单，直接在z轴上偏移出来即可
	
	```
	transform: translateZ(100px);
	
	```
5.	设置右侧的面
	*	这个面向Z轴偏移的同时，在Y轴上旋转90度
	*	**Y轴旋转以逆时针为正向**
	*	**X轴旋转顺时针针为正向**	
6.	设置正前方正后方的面
	*	Y轴旋转180度，z轴偏移100px
7.	设置左侧的面
	*	Y轴旋转-90度，z轴偏移100px
8.	设置上方的面
	*	X轴旋转90度，z轴偏移100px
9.	设置下方的面
	*	X轴旋转-90度，z轴偏移100px

##旋转
让立方体旋转需要使用动画
*	使用@keyframes创建关键帧
*	例如：
	
```
	@keyframes rotate{
			0%{
		    transform:rotateX(0deg) rotateY(0deg);
			}
			50%{
		    transform:rotateX(180deg) rotateY(360deg);
			}
			100%{
		    transform:rotateX(-360deg) rotateY(-360deg);
			}
		}
		
```

##演示
[在线demo](http://runjs.cn/detail/00oeh2lf)