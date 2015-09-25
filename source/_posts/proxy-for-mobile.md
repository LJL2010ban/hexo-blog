title: 使用gas&charles为移动端搭建测试环境
date: 2015-07-01 20:49:35
categories: Tools 
tags: [tool,webapp,gasmark,charles]
---
移动端开发时调试并不想web端那么方便，移动端有自己的特有的一些使用场景，比如说支付，特定页面认证，微信登录等等。

所以今天想大家推荐2个调试时用起来很顺手的工具，Gas Mask和Charles poxy.

**工具**

*	gas mark
*	charles

###Gas配置过程
Gas Mask是个简单(而且免费)的hosts文件管理工具，方便的编辑hosts并在不同的hosts配置间切换。

1.	请确保以上软件已经安装完成
2.	配置想要代理的域名
	*	启动gas mark, 'crate -> local'命名为'Host File'，格式如下：
	
	![新建](http://7xix26.com1.z0.glb.clouddn.com/gas1.png)
	
	```
	//默认内容
	127.0.0.1		localhost
	255.255.255.255	broadcasthost
	::1				localhost
	fe80::1%lo0		localhost

	127.0.0.1 as-vip.missfresh.cn
	127.0.0.1 as.staging.missfresh.cn 
	127.0.0.1 as-school.missfresh.cn 
	```	
	![配置](http://7xix26.com1.z0.glb.clouddn.com/gas3.png)
	

###Charles 
Charles通过将自己设置成系统的网络访问代理服务器，使得所有的网络访问请求都通过它来完成，从而实现了网络封包的截取和分析。

Charles是收费软件，可以免费试用30天。试用期过后，未付费的用户仍然可以继续使用，但是每次使用时间不能超过30分钟，并且启动时将会有10秒种的延时。

Charles的主要功能有：
*	Session
*	Recording
*	Request & Response
*	Chart
*	Import
*	Export
*	SSL Certificates
*	Load Testing
*	Web Interface
*	Protocol Buffers
*	Command-line Options

####代理请求，捕获跟踪
而我们常用的功能主要是捕获请求，查看请求跟响应过来的数据，以及网络环境模拟.

*	设置代理端口,暂定为8888
	
	![设置代理端口](http://7xix26.com1.z0.glb.clouddn.com/charles1.png)
	![设置代理端口](http://7xix26.com1.z0.glb.clouddn.com/charles6.png)

*	设置监听的请求
	
	![设置监听请求](http://7xix26.com1.z0.glb.clouddn.com/charles2.png)

*	手机设置代理
	
	![手机代理](http://7xix26.com1.z0.glb.clouddn.com/charles4.png)
	
*	手机代理设置成功后，charles回提示，点击Allow
	![charle允许接入](http://7xix26.com1.z0.glb.clouddn.com/charles3.png)

*	访问被代理的地址，charles上会有记录
	![访问记录](http://7xix26.com1.z0.glb.clouddn.com/charles7.png)

####模拟网络
这个功能非常好，charles可以模拟不同的网络，比如2G,3G，还能自定义设置网络速度，可以用来模拟慢网速。

*	开启网速模拟

	![开启](http://7xix26.com1.z0.glb.clouddn.com/charles10.png)
*	配置

	![配置](http://7xix26.com1.z0.glb.clouddn.com/charles11.png)

参考文献：
*	[iOS开发工具-网络封包分析工具Charles](http://blog.devtang.com/blog/2013/12/11/network-tool-charles-intr/)

**软件下载**
*	[gas mark](http://www.macupdate.com/app/mac/29949/gas-mask/)
*	[charles](http://www.macupdate.com/app/mac/12462/charles/)(自行破解)




