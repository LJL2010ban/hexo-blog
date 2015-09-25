title: 使用chrome浏览器在Android上调试web页面
date: 2015-07-13 17:51:18
categories: Tools
tags: [debug,tool,chrome]
---
在移动开发中，移动版页面调试是个头疼的问题，强大google发明了如何使用chrome调试android上的web页面

##要求
*	首先是你的机器上已经安装了chrome 32（版本或以上）浏览器
*	一根连接安卓设备的usb连接线
*	手机上的android系统版本必须在4.0+并且安装了chrome for android 浏览器


步骤：

*	手机上开启开发者选项
*	连接上数据线
*	电脑打开chrome浏览器，地址栏输入：chrome://inspect, 回车,会出现类似下图：
	![chrome://inspect的结果](http://7xix26.com1.z0.glb.clouddn.com/inspect.png)

*	手机上打开chrome浏览器，输入一个地址，此处使用www.baidu.com
*	点击上图中**inspect**按钮，会弹出一个新层，如图:
	![inspect弹出层](http://7xix26.com1.z0.glb.clouddn.com/console.png)
	
*	后续步骤就跟在电脑上调试web页面一样的步骤了。


参考资料：

[Remote Debugging on Android with Chrome](https://developer.chrome.com/devtools/docs/remote-debugging)
