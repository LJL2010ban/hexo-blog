title: 腾讯X5浏览器调试
date: 2015-07-22 11:15:09
categories: Tools
tags: [tool,front-end,chrome,debug,webapp]
---

朋友分享出来的一篇文章，当真实用的紧：[微信、手Q、Qzone之x5内核inspect调试解决方案](http://bbs.mb.qq.com/thread-243399-1-1.html) ，迫不及待的按照攻略来了一遍，就赶紧拿出来分享了，详细不步骤里面说的很清楚，我来说说mac下配置遇到的一些问题。

*	python版本
	
	mac os 自带的python版本是2.7 ，上面攻略中需要使用python3.4,所以需要升级Python,升级攻略参考:[如何将Mac OS X10.9下的Python2.7升级到最新的Python3.3](http://www.cnblogs.com/nokiaguy/p/3456590.html),升级到3.4步骤一致
	
	**注意**
	本人安装python 3.4完成以后，不能使用python命令，需要使用python3.4， 想要使用python需要自己去做个软连接
	
*	安装过程
	
	整个安装过程很顺利，唯独到了安装chrome inspector的时候遇到了问题，教程中也有人遇到了问题，所以本人编译时用的命令是：
	
	```
	sudo python inspector.py --adb /usr/local/bin/adb
	```
	
*	结果截图

	![启动图](http://7xix26.com1.z0.glb.clouddn.com/x51.png)
	
	![调试图](http://7xix26.com1.z0.glb.clouddn.com/x52.png)
	