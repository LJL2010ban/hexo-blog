title: learn css part one
date: 2015-06-18 11:15:26
categories: css
tags: front-end
---
##说明

*	webkit引擎的浏览器有：Safari, Google Chrome,前缀是-webkit-
*	Gecko引擎浏览器：Mozilla,常指Firefox， 前缀 -moz-
*	Presto引擎浏览器：Opera，前缀 -o-
*	KHTML引擎浏览器：Konqueror， 前缀 -khtml-
*	Trident引擎浏览器：Internet Explorer, 前缀 -ms-


##定位

*	position
	
	*	默认值：static
	*	relative: 遵循正常文档流，但可通过top,right,bottom,left 偏移位置
	
*	z-index
	*	默认值: auto
	*	同级对象，写在后面的对象将会覆盖前面的

##布局 

*	display
	*	none: 隐藏，但是与visibility=hidden不同，不保留占用空间
	
	**说明**
	*	IE7及以下浏览器不支持table相关的参数值
	*	暂无浏览器支持ruby相关参数值
	*	IE8不支持CSS3新增属性值：compact | ruby | ruby-base | ruby-text | ruby-base-group | ruby-text-group | box | inline-box。
	*	IE9不支持compact | box | inline-box属性值。	
*	float
	*	属性值不为none时，忽略display属性值
	
*	visibility
	*	visible,hidden,collapse（隐藏表格的行或列）	*	可视状态下必须保证父级元素也为可视。
*	clip
	*	剪切对象可视区域（左上角为起始点）
	*	默认值auto,不剪切
	
	使用：
	
	```
	clip:rect(0 auto, 35px 10px); -- IE7以下
	or
	clip:rect(0, auto,35px,10px);
	```
	
##弹性布局
*	box-orient
	*	horizontal	子元素水平排列
	*	vertical	子元素纵向排列
	*	js中使用boxOrient
*	box-pack
	*	子元素排列方式
	*	start	
	*	center	全部居中
	*	end
	*	justify 两端对其
*	box-align
	*	子元素开始位置
	*	start
	*	center
	*	end
	*	baseline
	*	stretch (默认值)	 自适应父级元素尺寸
*	box-flex
	*	分配占用父级元素的剩余空间比例
*	box-flex-group
	*	定义子元素所在的组
*	box-ordinal-group
	*	定义子元素显示顺序
*	box-direction
	*	子元素显示顺序
	*	normal
	*	reverse ，反转
*	box-lines
	*	是否多行显示
	*	single, multiple

##外补白
*	margin，padding
	*	内联对象仅可以设置左右，设置上下间距时必须使元素为块级或者内联块级

##边框
*	border-radius
	
	圆角边框，2个参数以'/'分割，每个参数允许设置1~4个参数值，第1个参数表示水平半径，第2个参数表示垂直半径，如第2个参数省略，则默认等于第1个参数
	
	水平半径：如果提供全部四个参数值，将按上左(top-left)、上右(top-right)、下右(bottom-right)、下左(bottom-left)的顺序作用于四个角。
	
	如果只提供一个，将用于全部的于四个角。
	
	如果提供两个，第一个用于上左(top-left)、下右(bottom-right)，第二个用于上右(top-right)、下左(bottom-left)。
	
	如果提供三个，第一个用于上左(top-left)，第二个用于上右(top-right)、下左(bottom-left)，第三个用于下右(bottom-right)。
	
	垂直半径也遵循以上4点。

*	box-shadow
	
	阴影
	
	**语法**
	
	```
	box-shadow：none | \<shadow\> \[ , \<shadow\> \]\*
	
	\<shadow\> = inset? && [ \<length\>{2,4} && \<color\>? ]
	
	*	\<lenght\>: 第1个长度值用来设置对象的阴影水平偏移值。可以为负值
	*	\<lenght\>: 第2个长度值用来设置对象的阴影垂直偏移值。可以为负值
	*	\<lenght\>: 如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值
	*	\<lenght\>: 如果提供了第4个长度值则用来设置对象的阴影外延值。不允许负值
	```
	
	使用
	
	
	>外阴影常规效果
	
	>box-shadow:5px 5px rgba(0,0,0,.6);
	
	>外阴影模糊外延效果
	
	>box-shadow:5px 5px 5px 10px rgba(0,0,0,.6);
	
	>内阴影效果
	
	>box-shadow:2px 2px 5px 1px rgba(0,0,0,.6) inset;
	
	
	
*	**box-reflect**
	
	文字倒影
	
	**语法**
	
	```
	
	box-reflect：none | <direction> <offset>? <mask-box-image>?
	<direction> = above | below | left | right
	<offset> = <length> | <percentage>
	<mask-box-image> = none | <url> | <linear-gradient> | <radial-gradient> | 	<repeating-linear-gradient> | <repeating-radial-gradient>
	默认值：none
	
	none：无倒影
	<direction>　Demo: 简单图片倒影
	above：指定倒影在对象的上边
	below：指定倒影在对象的下边
	left：指定倒影在对象的左边
	right：指定倒影在对象的右边
	<offset>　Demo: 图片与倒影间隔
	<length>：用长度值来定义倒影与对象之间的间隔。可以为负值
	<percentage>：用百分比来定义倒影与对象之间的间隔。可以为负值
	<mask-box-image>　Demo: 更真实的图片倒影 文字倒影与渐变
	none：无遮罩图像
	<url>：使用绝对或相对地址指定遮罩图像。
	<linear-gradient>：使用线性渐变创建遮罩图像。
	<radial-gradient>：使用径向(放射性)渐变创建遮罩图像。
	<repeating-linear-gradient>：使用重复的线性渐变创建背遮罩像。
	<repeating-radial-gradient>：使用重复的径向(放射性)渐变创建遮罩图像。
	
	```
	

##背景
*	background
	*	允许指定多个image
*	background-attachment
	*	设置背景图片位置
	*	fixed,scroll(默认),local
*	background-origin
	*	指定背景图片显示位置
	*	padding-box		从padding区域开始显示
	*	border-box		从border区域开始显示
	*	content-box		从content区域开始显示

##颜色
*	opacity
	*	透明度
	
	**说明**
	
	IE使用filter实现
##文字
*	text-index
	
	对块级或者内联块级元素设置缩进
*	text-transform
	*	none
	*	capitalize	单词首字母转换成大写
	*	uppercase
	*	lowercase

*	text-decoration

	对文字修饰
	*	下划线，删除线
*	text-shadow
	*	文字阴影
*	text-fill-color
	*	文字填充颜色
	*	[demo](http://demo.doyoe.com/css3/text-fill-color/gradient-text.htm)
	
