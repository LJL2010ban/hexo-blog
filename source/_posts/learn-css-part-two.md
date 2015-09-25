title: learn css part two
date: 2015-06-23 15:54:29
categories: css
tags: [front-end,animation]
---
##文字
*	text-index
	
	对块级或者内联块级元素设置缩进
*	text-transform
	*	none
	*	capitalize	单词首字母转换成大写
	*	uppercase
	*	lowercase

*	text-decoration

	对文字修饰(下划线，删除线)
*	text-shadow
	*	文字阴影
*	text-fill-color
	*	文字填充颜色
	*	[demo](http://demo.doyoe.com/css3/text-fill-color/gradient-text.htm)
*	text-stroke
	*	文字描边
*	letter-spacing
	*	文字间距
*	word-spacing
	*	单词间距
*	word-wrap
	*	换行
	*	normal | break-word
*	white-space
	*	normal
	*	pre
	*	nowrap: 强制在同一行显示所有文本
	*	pre-wrap: 碰到边界换行
	*	pre-line: 碰到边界换行

##列表
*	list-style
*	list-style-image
*	list-style-position
	*	outside
	*	inside
*	list-style-type

##用户界面	
*	box-sizing
	*	content-box (默认)
		
		padding和border不被包含在定义的width和height之内,实际宽度= width + border+ padding
		
	*	border-box
		padding和border包含在定义的width和height之内


##2D变换-transform
*	transform
	
	可用属性
	*	none
	*	matrix(<number>,<number>,<number>,<number>,<number>,<number>)：
以一个含六值的(a,b,c,d,e,f)变换矩阵的形式指定一个2D变换，相当于直接应用一个[a,b,c,d,e,f]变换矩阵
	*	translate(<length>[, <length>]):指定对象的2D translation（2D平移）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
	*	rotate(<angle>):指定对象的2D rotation（2D旋转），需先有transform-origin属性的定义
	*	scale(<number>[, <number>])：指定对象的2D scale（2D缩放）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认取第一个参数的值
	*	skew(angle[,angle]):指定对象skew transformation（斜切扭曲）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
*	transform-origin
	*	设置原点坐标，默认50% 50%
	
##3D转换-transform
*	transform
	*	rotateX(0deg)	元素围绕x轴进行度数旋转
	*	rotateY(120deg)	元素围绕Y轴进行度数旋转
	*	translate3d(x,y,z)

##过渡-transition
*	transition

	transition：[ transition-property ] || [ transition-duration ] || [ transition-timing-function ] || [ transition-delay ]
	
	```
	取值：
	[ transition-property ]：检索或设置对象中的参与过渡的属性
	
	[ transition-duration ]：检索或设置对象过渡的持续时间
	
	[ transition-timing-function ]：检索或设置对象中过渡的动画类型

	[ transition-delay ]：检索或设置对象延迟过渡的时间
	```

##动画-animation
*	animation

	语法
	
	```
	animation：[[ animation-name ] || [ animation-duration ] || [ animation-timing-function ] || [ animation-delay ] || [ animation-iteration-count ] || [ animation-direction ]] [ , [ animation-name ] || [ animation-duration ] || [ animation-timing-function ] || [ animation-delay ] || [ animation-iteration-count ] || [ animation-direction ]]*
	```
	取值
	
	```
	[ animation-name ]：检索或设置对象所应用的动画名称
	
	[ animation-duration ]：检索或设置对象动画的持续时间
	
	[ animation-timing-function ]：检索或设置对象动画的过渡类型
		*	linear	线性
		*	ease	平滑
		*	ease-in	由慢到快
		*	ease-out	由快到慢
		*	ease-in-out	慢-快-慢
	
	[ animation-delay ]：检索或设置对象动画延迟的时间
	
	[ animation-iteration-count ]：检索或设置对象动画的循环次数
		*	infinite	无限循环
	
	[ animation-direction ]：检索或设置对象动画在循环中是否反向运动
		*	normal	
		*	alternate	反向
	
	[ animation-play-state ]：检索或设置对象动画的状态。
	
	[ animation-fill-mode ]：检索或设置对象动画时间之外的状态
		*	none
		*	forwards	设置为动画结束时的状态
		*	backwards	设置为动画开始时的状态
		*	both	结束或开始的状态
	```
	使用
	*	@keyframes name  定义动画
	*	动画内 0% ~100% 定义关键帧
	*	动画元素使用animtion: name 
	
	

	
