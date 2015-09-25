title: 常用Ionic 命令整理
date: 2015-08-04 14:59:09
categories: [ionic]
tags: [ionic,cmd]
---

*	添加crosswalk

```
	//查看ionic现有的浏览器插件
	ionic browser list
	
	//添加crosswald
	ionic browser add crosswalk@11.40.277.7
````

*	检查android SDK配置

```
	brew info android-sdk 
	
	正确设置ANDROID_HOME
```

*	编译

```
	ionic build android 
	
```


*	用IDEA打开编译后的Android项目
	*	此处需要配置IDEA的开发环境
	*	android的sdk目录
	*	设置Gradle
	*	SDK Setting
	*	更新JDK至少7.0以上
	
*	设置 build.gradle

	```
		jniLibs.srcDirs = ['libs']
	```
*	设置crosswald.engine

	```
	src/org/crosswalk.engine/xwalkcordovaResourceClient
		
		if ((url.startsWith("http:") || url.startsWith("https:")) && parentEngine.pluginManager.shouldAllowRequest(url)) {
	```



 *	安装到手机
 
 ```
 	//编译ionic项目
 	ionic prepare
 	
 	生成 Signed APK（生成正式版的apk）
 
 	//安装到真机
 	adb install -r platforms/android/android-armv7-release.apk
 ```
 
 
 ##chrome 测试app
 
 ```
 	chrome://inspect/#devices
 ```
 
 
 ----
 
##插件
	 
```
	sudo npm install -g ionic
	
	rm -rf cn.missfresh.wx
	
	ionic plugin rm cn.missfresh.alipay
	ionic plugin rm cn.missfresh.wx
	
	
	ionic plugin add http://git.missfresh.net/frontend/im-plugin.git
	
	ionic plugin add http://git.missfresh.net/frontend/alipay.git
	
	ionic plugin add http://git.missfresh.net/frontend/wechat-plugin.git
	
```
*	更新
	
	```
	
	ionic lib
	
	ionic lib update 
	
	
	ionic browser upgrade
	
	```
	

##重置插件

```
	ionic browser rm crosswalk
	ionic plugin list
	
	ionic plugin list | awk '{print $1}'
	
	ionic plugin list | awk '{print $1}'|xargs -I{} ionic plugin rm {}
	
	ionic platform rm ios
	
	ionic platform rm android
	
	ionic browser list	
	
	ionic browser add crosswalk
			
	ionic plugin
	
	rm -rf plugins/cn.missfresh.*
	
	rm -rf plugins/cn.*
	
	修改 package.json
	
	ionic state restore
	
	
```

##启动

```
ionic serve -d		关闭livereload
ionic serve -p 8080	修改启动服务端口     
```


##Nginx

*	vi /usr/local/etc/nginx/servers/as.conf	
	
	--修改配置
	
	--as.conf 为自定义配置文件
*	sudo nginx -s reload
	
	--重新载入配置	
