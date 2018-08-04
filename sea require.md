## seaJS(CMD) ##

在 Sea.js 中，所有 JavaScript 模块都遵循 CMD（Common Module Definition） 模块定义规范。该规范明确了模块的基本书写格式和基本交互规则。

在 CMD 规范中，一个模块就是一个文件。



#### 参考文档

- [Seajs使用实例入门介绍](https://www.jianshu.com/p/ebdf2233e3fe)
- [seaJS 简要介绍和完整例子](http://blog.csdn.net/shenzhennba/article/details/51661544)
- [SeaJS之use函数](http://www.cnblogs.com/ada-zheng/p/3284660.html)
- [SeaJS从入门到原理](http://blog.csdn.net/sinat_17775997/article/details/52522767)
- [seajs学习（1）----什么是系统](http://blog.csdn.net/cpf506497746/article/details/8832254)
- [seajs学习（2）----CMD 模块定义规范](http://blog.csdn.net/cpf506497746/article/details/8832317)
- [seajs学习（3）----模块标识](http://blog.csdn.net/cpf506497746/article/details/8832350)
- [seajs学习（4）----require 书写约定](http://blog.csdn.net/cpf506497746/article/details/8832386)
- [seajs学些（5）----模块的加载启动](http://blog.csdn.net/cpf506497746/article/details/8832415)
- [seajs学习（6）----配置](http://blog.csdn.net/cpf506497746/article/details/8832421)
- [seajs学习（7）----文本插件](http://blog.csdn.net/cpf506497746/article/details/8832437)




原理：(通过回调函数来处理的)

	1.html文件：		seajs.use(1,2) 执行
	2.插件：			模块插件 创建一个 script 标签
	3.插件：			定义一个全局函数 define 用来获取模块里面所写的代码
	4.模块：			模块文件里 执行 define(传入一个函数)
	5.插件：			jeajs.use 执行上一步的函数，并且传入3个参数
	6.再执行模块里传入的参数过程中改变了 module 
	7.插件：			插件里：执行回调函数，插件的第二个参数
	8.html文件：		接收 module.exprots

```js
function seajs(url, cb) {
  // 创建标签
  var hm = document.createElement("script");
  // 让script标签的路径 = 穿进来的参数
  hm.src = url;
  var s = document.getElementsByTagName("script")[0];
  s.parentNode.insertBefore(hm, s);

  var require,
    exports,
    module = {};
  window.define = function (fn) {
    // fn = 以下代码
    /*
    function (require, exports, module) {
      // 这里是定义模块的地方
      function fn(dom) {
        return document.getElementById(dom)
      }
      module.exports = fn
    }
    */
    fn(require, exports, module);
    // console.log(module);

//     cb =
//     function (goudan) {
//       console.log(goudan);
//       console.log(goudan("box"));
//     }
    cb(module.exports);
    s.parentNode.removeChild(hm)
  }
}


/**
 * 为了让 sea.js 内部能快速获取到自身路径，推荐手动加上 id 属性
 * <script src="path/to/sea.js" id="seajsnode"></script>
 */
```





#### 项目文件

```
/*
 *	sea-module		seaJS文件夹
 *	static			静态资源文件夹
 */

sea-projest\
	sea-module\
		jquery\
			jquery.js
		sea.js
	static\
		main.js
		mokuai.js
	index.html
		
```



#### 启动模块

> index.html

```html
<script src="sea-module/sea.js"></script>
<script>
    seajs.use('./static/main.js')
</script>
```

> main.js

```js
define(function (require,exports,module) {
    alert('hellow seaJS')
})
```



#### seajs.use回调

> index.html

```html
<script>
  /* 单个模块调用 main.js */
    seajs.use('./static/main.js',function (main) {
        main()
    })
</script>
---------------------------------------------------------------
<script>
    /* 多个模块调用 [ main.js, mokuai.js ] */
    seajs.use(['./static/main.js','./static/mokuai.js'],function (main,mokuai) {
        main()
        mokuai()
    })
</script>
```

> main.js

```js
define(function (require,exports,module) {
    module.exports = function () {
        console.log('This is main.js')
    }
})
```

> mokuai.js

```js
define(function (require,exports,module) {
    module.exports = function () {
        console.log('This is mokuai.js')
    }
})
```



#### 模块间引用

`main.js` 引用 `mokuai.js`

> index.js

```html
<script>
    seajs.use('./static/main.js')
</script>
```

> main.js

```js
define(function (require,exports,module) {
    let mokuai = require('./mokuai.js')		// 引入模块
    mokuai()
})
```

> mokuai.js

```js
define(function (require,exports,module) {
    module.exports = function () {		// 输出接口
        console.log('This is mokuai.js')
    }
})
```



#### 别名设置

引入一个模块要写他的相对路径，我们可以给它取个别名，在seajs.use()上面加入这一段代码：

```html
<script>
    seajs.config({
        alias:{
            'changeText':'../static/changeText.js'
        }
    });
    seajs.use('./static/main.js');
</script>
```

通过config中alias给`'../static/changeText.js'`设置了别名`changeText`，现在main中引用changeText模块就可以直接写成这样了`var changeText = require('changeText')`。



#### 第三方文件引用

下载一个jquery源文件，按如下修改：

```js
define(function (require, exports, module) {
    jquery 源码
})
```

使其模块化，能被外部调用。

然后再设置别名：

```js
seajs.config({
     alias:{
          'jquery':'jquery/jquery',
          'main':'./static/main.js'
     }
});
seajs.use('./static/main.js');
```

在main中引入jquery，并使用：

```js
define(function (require, exports, module) {
    var $ = require('jquery');
    $(document).text('hello seaJS');
})
```









## requireJS(AMD)

由[CommonJS](http://www.cnblogs.com/xiaohuochai/p/6847939.html)组织提出了许多新的JavaScript架构方案和标准，希望能为前端开发提供统一的指引。AMD规范就是其中比较著名一个，全称是Asynchronous Module Definition，即**异步模块加载机制**，完整描述了模块的定义，依赖关系，引用关系以及加载机制。而AMD规范的作者亲自实现了符合AMD规范的requireJS。



#### 参考文档

- [后台小白前端入门－－RequireJS](https://www.jianshu.com/p/b8a6824c8e07)
- [AMD及requireJS](http://www.cnblogs.com/xiaohuochai/p/6847942.html)
- [requireJS 从概念到实战](http://www.cnblogs.com/HCJJ/p/6611669.html)
- [RequireJS进阶:配置文件的学习](https://segmentfault.com/a/1190000002401665)
- [RequireJs入门教程学习](http://www.zymseo.com/369.html)




#### 使用RequeryJS

引入require库

```html
1
/* 在html页面中引入require库 */
<script type="text/javascript" src="./js/require.js"></script>
2
/* 加载require.js以后，下一步就要加载我们自己的代码了。假定我们自己的代码文件是main.js，也放在js目录下面 */
<script src="js/require.js" data-main="./js/main"></script>
3
/* data-main属性的作用是，指定网页程序的主模块。在上例中，就是js目录下面的main.js，这个文件会第一个被require.js加载。由于require.js默认的文件后缀名是js，所以可以把main.js简写成main（data-main引入的main.js文件是异步加载的，所以在加载这个文件的同时也会加载其他js文件，其他文件要依赖这个main.js，所以可以将以上代码分开来写） */
<script type="text/javascript" src="./js/require.js"></script>
<script type="text/javascript" src="./js/main.js"></script>
```

加载主模块`main.js`












## CommonJS 的 Modules/Transport 和 Modules/Wrappings 规范有什么区别？

Modules/Wrappings 一般是指：

```
define(function(require, exports, module) {
   // 
})

```

define 可以换成 module.declare 等等词汇。表示模块书写格式，这些写就好。

但书写格式直接上线存在问题，比如不能直接压缩、不能合并等，因此在压缩、合并前，需要先做一些处理，这些处理就是 transport 操作，transport 后的代码格式称之为 Modules/Transport  规范，这一般是通过构建工具自动生成。典型的：

```
define(id, deps, factory)

```

以上是 CommonJS 社区里一部分人的理解。还有一部分觉得，模块在写的时候，就应该带上 id 、deps 等信息，比如：

```
define("a", ...)

define(["a", "b"], function(a, b) { ... }) // 这就是 AMD 的标准写法

```

在这部分人心中，不应该存在 Transport 规范，Transport 规范也应该是 Wrappings 规范的一种。

还有一批人的想法是，以上格式都是 Transport 格式，都应该由工具生成。真正的模块书写格式应该是：

```
var a = require("a")
exports.foo = ...

```

这部分代表喜欢用自动构建的方式来解决在浏览器上的运行问题，类似 coffee 这种方式。

SeaJS 里，推崇的 Modules/Wrappings 规范是 CMD 规范：

```
define(function(require, exports, module) {
   var a = require("a")
   exports.foo = ...
})

```

以上直接是由开发者手写的，写完后，可直接不经过任何构建工具就在浏览器上加载运行。
但 CMD 模块在正式上线前，依旧需要通过构建工具先转换为 Modules/Transport 格式：

```
define("id", ["dep-1", "dep-2"], function(require, exports, module) {
   // source code
})

```

转换成 Transport 格式后，才能进一步压缩、合并等。



































