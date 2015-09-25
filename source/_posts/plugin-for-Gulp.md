title: gulp插件开发手札
date: 2015-06-19 14:27:15
categories: Tools
tags: [gulp,plugin,tool]
---
gulp

一个比grunt使用更为简单的自动化构建工具，Gulp通过流和代码优于配置策略来尽量简化任务编写的工作。

这里不在赘述gulp的基本使用法。请参考：

*	[gulp getting-started](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
*	[gulp高级技巧](http://segmentfault.com/a/1190000000711469)
*	[gulp vs grunt](http://segmentfault.com/a/1190000002491282)


**需求**

项目中使用了gulp，以及一些插件，其中有压缩，md5后缀等等，我们的项目仅在移动端运行，考虑到性能，需要延迟加载js文件，因为压缩后的js文件体积相对比较，想通过创建script标签的形式，等页面ready了再去加载js。因为使用了md5，所以每次压缩完的文件名都不一样，而动态加载的脚本需要知道压缩后的文件名称，不想每次手都修改。

**插件功能**

所以要实现的功能就是，在js进行压缩，合并以后，处理首页html.

首先要知道如何开发一个gulp插件

*	[gulp插件开发规范(英文)](https://github.com/gulpjs/gulp/blob/master/docs/writing-a-plugin/guidelines.md)
*	[gulp插件开发规范(中文)](http://www.u396.com/gulp-plugin-guildlines.html)

因为是个小功能，所以我也就没有单独封装成模块，而是封装成一个单独函数方便使用：

```
function asyncLoad() {
  console.log("Starting 'async load'...");
  return through.obj(function(file,enc,cb){
    if(file.isNull()) {
      cb(null,file);
    }
    if (file.isBuffer()) {
      var data = Buffer.concat([file.contents]).toString();
      data = data.replace('<link rel="stylesheet" href="', '<link rel="stylesheet" href="' + statics + '/');
      data = data.replace('<img src="./img/icon.png" style="width:80px" alt=""/>', '<img src="' +statics + '/img/icon.png" style="width:80px" alt=""/>');
      data = data.replace('<script src="js/ionic.all','<script src="load.js" id="asyncLoading" data-asyncLoading="'+ statics +'/js/ionic.all');
      data = data.replace('</head>', '<script type="text/javascript" src="http://tajs.qq.com/stats?sId=45760313" charset="UTF-8"></script>\n</head>');
      file.contents = new Buffer(data);
    }
    if (file.isStream()) {
        console.log('async load error');
    }
    cb(null, file);
  });
}
```
说明：

*	需要安装through2模块： npm install throuth2  --save-dev
*	Node中buffer的使用
	*	[node的buffer介绍](http://blog.chinaunix.net/uid-26672038-id-4173346.html)
	*	[浅析nodejs的buffer类](https://cnodejs.org/topic/5189ff4f63e9f8a54207f60c)

**使用**

使用方式跟普通的gulp插件调用方式一样

```
gulp.task('usemin', function(cd) {
  return gulp.src('./www/index.html')
    .pipe(usemin({
      css: [minifyCss(), 'concat', rev()],      
      js: [rev()]
    }))
    .pipe(asyncLoad())
    .pipe(gulp.dest('./dest/'));
});
```

总结：

功能很简单，就是需要知道如何开发gulp插件，参考上面的模板，然后参看了一些gulp官网上的插件是如何写的，基本上就完了，同事需要知道nodejs如何操作buffer就可以了。















