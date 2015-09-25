title: 学习flexbox弹性布局
date: 2015-07-07 18:26:19
categories: css
tags: [css,flexbox,弹性布局]
---

##基础概念

伸缩容器：一个设有“display:flex”或“display:inline-flex”的元素

伸缩项目：伸缩容器的子元素

主轴、主轴方向：用户代理沿着一个伸缩容器的主轴配置伸缩项目，主轴是主轴方向的延伸。

主轴起点、主轴终点：伸缩项目的配置从容器的主轴起点边开始，往主轴终点边结束。

主轴长度、主轴长度属性：伸缩项目的在主轴方向的宽度或高度就是项目的主轴长度，伸缩项目的主轴长度属性是width或height属性，由哪一个对着主轴方向决定。

侧轴、侧轴方向：与主轴垂直的轴称作侧轴，是侧轴方向的延伸。

侧轴起点、侧轴终点：填满项目的伸缩行的配置从容器的侧轴起点边开始，往侧轴终点边结束。

侧轴长度、侧轴长度属性：伸缩项目的在侧轴方向的宽度或高度就是项目的侧轴长度，伸缩项目的侧轴长度属性是「width」或「height」属性，由哪一个对着侧轴方向决定。

![主轴，侧轴](http://7xix26.com1.z0.glb.clouddn.com/flex.png)

**父级元素**

*	display:flex

*	flex-flow
	*	row	横排
	*	column	竖排 
	*	row-reverse
	*	column-reverse
	*	wrap	允许折行
	
	**备注**
	
	flex-flow其实是flex-direction(取值有:row ,column, row-reverse, column-reverse) 与 flex-wrap（取值有:wrap, no-wrap, wrap-reverse）的缩写属性。

*	**主轴，侧轴**	
	
*	align-items
	*	侧轴方向排列方式
		*	flex-flow为row是，侧轴是Y轴
	*	flex-start	侧轴起点对奇
	*	center		侧轴居中
	*	flex-end	侧轴终点对齐
	*	stretch		填充侧轴

*	justify-content
	*	控制子元素之间多余的空白如何处理
	*	flex-start
	*	flex-end
	*	center	
	*	space-around
		
		所有的子元素均匀的分布在父元素上，表现为居中	
	
	*	space-between
		
		区别于space-around 首位都在住主轴上，其他子元素居中与父元素的宽上
	
*	align-content
	*	多行伸缩容器的对其
	*	**仅在伸缩容器在侧轴占有固定的空间时才有用**
	*	flex-start
	*	flex-end
	*	center
	*	space-around
		
		所有的子元素均匀的分布在父元素上，表现为居中	
	*	space-between
		
		区别于space-around 首位都在住主轴上，其他子元素居中与父元素的宽上	
	
**子元素**	
	
*	order
	*	改变布局顺序
	
*	flex
	*	让元素可以伸缩
		*	当flex-flow为row时，伸缩方向为width
		*	当flex-flow为column时，伸缩方向为height
	*	没有单位
	*	可以设置基准值
	*	设置负向伸缩值
	
	```
	.first {
		flex:1	200px;
	}
	.second {
		flex:2	300px;
	}
	.third {
		flex:1 2 400px;
	}
	2个参数：
	前面的数字为比例值，后面的为基准值
	
	```
	
	```
	.first {
		flex:1 1 400px;
	}
	.second {
		flex:2 3 600px;
	}
	.third {
		flex:1 2 400px;
	}
	3个参数：
	中间的参数表示加权比
	假设父元素在主轴的方向尺寸为 1100px，在这种情况下，上例中的子元素就会溢出 300px（在主轴方向总尺寸为 1400px），因为设置了负向伸缩值，加权综合为 400px × 1 + 600px × 3 + 400px × 2 = 3000px：
	first 将被移除溢出量的 400px/3000px = 2/15，也就是 40px，因此计算后的尺寸为 360px。
	second 将被移除溢出量的 600px × 3/3000px = 9/15，也就是 180px，因此计算后的尺寸为 420px。
	thrid 将被移除溢出量的 400px × 2/3000px = 4/15，也就是 80px，因此计算后的尺寸为 320px。
所以负向伸缩值越大元素越小！	
	
	```
---

参考资料

[伸缩布局 — 打开布局天堂之门](http://dev.oupeng.com/articles/flexbox-basics)

[Flexbox——快速布局神器](http://www.w3cplus.com/css3/flexbox-basics.html)



	




