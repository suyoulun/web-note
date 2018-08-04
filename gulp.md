# gulp #

- 模块化开发
- 基于 node.js ，类似的有 webpack

### 安装 node ###


> 检测是否安装 node.js

- 打开命令 win+R -> cmd

```
node -v
```

### 安装 gulp ###

```
npm install gulp -g(全局)
```

### 检测 gulp 版本 ###

```
gulp -v
```

node 没有 alert() 方法，只能通过 console.log() 方法打印


### 使用 gulp  ###

在文件夹下 `Shift+鼠标右键` 点击 `在此处打开命令窗口`


新建一个 `gulpfile.js` 文件 


在项目文件夹打开命令窗口


#### 下载 gulp 模块，在文件里引用 ####


> npm install gulp


#### 下载 压缩 模块 ####


> npm install gulp-uglify


#### 创建任务 ####

```javascript
[gulpfile.js]

//引入主模块
var gulp = require("gulp");
//引入压缩模块
var uglify = require("gulp-uglify");
//创建任务
//1.任务的名称
//2.具体执行什么操作
gulp.task("js", function(){
  //1.找到要压缩的文件 
  gulp.src("./1.js")
  
  //2.执行压缩 (.pipe :下一步)
  .pipe( uglify() )
  
  //3.生成文件到js目录下
  .pipe( gulp.dest("./js/") )
});

//默认执行 "js" 任务
gulp.task("default",["js"]);
```

#### 运行 ####


> gulp



### 压缩多个文件成一个文件 ###


#### 下载 模块 ####

> npm install gulp-connat

```
//引入模块
var concat = require("gulp-concat");

//什么时候合并？ 压缩完合并

[gulpfile.js]

//引入主模块
var gulp = require("gulp");
//引入压缩模块
var uglify = require("gulp-uglify");
//创建任务
//1.任务的名称
//2.具体执行什么操作
gulp.task("js", function(){
  //1.找到要(*所有)压缩的文件 
  gulp.src("./*.js")
  
  //2.执行压缩 (.pipe :下一步)
  .pipe( uglify() )
  
  //+ 合并成 all.js
  .pipe(concat("all.js"))
  
  //3.生成文件到js目录下
  .pipe( gulp.dest("./js") )
});

//默认执行 "js" 任务
gulp.task("default",["js"]);
```

### 实时压缩 ###

```
//1.监听什么文件  2.执行的任务
gulp.watch("./*.js",["js"]);
```

#### 运行 gulp ####

> gulp

#### 退出 运行 ####

> `Ctrl+C`



### 压缩css ###


安装模块
> npm install gulp-minify-css


```
var minifyCss = require("gulp-minify-css");

gulp.task("css",function(){
  gulp.src("./*.css")
  .pipe( minifyCss() )
  .pipe( concat("all.css") )
  .pipe( gulp.dest("./dest") )
});

gulp.task("default",["js","css"]);
gulp.watch("./*.css",["css"]);
```



### 压缩html ###


安装模块
> npm install gulp-minify-html


```
var minifyHtml = require("gulp-minify-html");

gulp.task("html",function(){
  gulp.src("./*.html")
  .pipe( minifyHtml() )
  .pipe( gulp.dest("./dest") )
});

gulp.task("default",["js","css","html"]);
gulp.watch("./*.html",["html"]);
```









