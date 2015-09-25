title: 用hexo在github上建立blog
date: 2015-06-11 20:56:58
categories: [experience]
tags: [experience,github,hexo]
---

#用hexo在github上建立blog

同事@icepy是个极客，看到他一直在用github pages建立的blog，感觉很不错，刚好又赶上自己的blog因为域名解析问题暂时无法访问，所以就开始着手利用自己的github账号创建一个。

*	**准备资料**
	
	*	[github pages](https://pages.github.com/)
	*	安装指引	
		*	[指引1](http://blog.fens.me/hexo-blog-github/)
		*	[指引2](http://ibruce.info/2013/11/22/hexo-your-blog/)
		
	*	[hexo](https://github.com/hexojs/hexo) - node.js开发的静态文件生成插件
	*	主题安装
	*	[MarkDown语法](http://www.appinn.com/markdown/)
	
	
*	问题

	根据以上教程安装配置，基本没啥大问题，以下是自己遇到的一些问题：
	
	*	github上建立新库时，一定要注意跟自己github用户名保持一致，我自己的英文名，姓名姓名缩写跟全拼都被别人给占去了，伤心呀
	
	*	hexo的全局配置文件，一定要仔细阅读一下，我就是因为域名配置错误，修改了n次依然有问题后，直接删掉github库重新搞了一次
	
	*	使用主题时注意顶部菜单的连接地址，如果要加上categories
	
	```
	/themes/主题名称/_config.yml 参考：
	menu:
  		Home: /
  		Archives: /archives
  		About: /categories/About/
	```
	
	*	写文章的时候，注意tags:跟categories: 的冒号后面要跟一个空格，否则编译时会报错。
	
	*	命令移动文件
		
		```
		当前在hexo创建的blog目录下:
		cp -r public/* ~/Documents/GitHubFiles/yuanxj1024.github.io
		```
	
[github 个人blog](http://yuanxj1024.github.io)









