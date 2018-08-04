# 包学会之浅入浅出Vue.js：开学篇

> 蔡述雄，现腾讯用户体验设计部QQ空间高级UI工程师。智图图片优化系统首席工程师，曾参与《众妙之门》书籍的翻译工作。目前专注前端图片优化与新技术的探研。

2016年，乃至接下来整个2017年，如果你要问前端技术框架什么最火，那无疑就是前端三巨头：**React、Angular、Vue**。没错，什么jQuery，seaJs，gulp等都逐渐脱离了热点。面试的时候不吹上一点新技术，好像自己就不是搞前端的似的。当然，希望大家都是抱着好学的心来开始一门学艺的，不管怎样，求求你，请接着看下去吧~

本系列文将会通过很多一目了然的例子和一个实战项目——组件库，来帮助大家学习Vue，一步一步来，毕竟这篇文章还有接下来的[【升学篇】](https://cloud.tencent.com/developer/article/1020338)和[【结业篇】](https://cloud.tencent.com/developer/article/1020416)呢。

## 什么是Vue.js

不管你想不想了解，你只需要大概知道，Vue就是和jQuery一样是一个前端框架，它的==中心思想就是数据驱动==，像远古时代的老前辈==jQuery是结构驱动==，什么意思呢，以前我们写代码时常用**$('.dom').text('我把值改变了')**，这种写法先要获得结构，然后再修改数据更新结构，而Vue的做法直接就是**this.msg="我改变了"**，然后msg就会同步到某个结构上，视图管理抽象为数据管理，而不是管理dom结构了。不懂没关系，慢慢来。

还有一点必须要知道的是，**Vue是国人写的，技术文档也妥妥的是中文**，想到这我就有学习的动力。

## 搭建环境

工欲善其事必先利其器，我们的学习计划从学会搭建Vue所需要的环境开始，node和npm的环境不用说是必须的，现在前端流程化很热门，基本上新的技术都会在这套流程的基础上做开发，我们只需要站在巨人的XX上装*就可以了。我假设你的机子上已经有了最新的node和npm了，那我们就只需要执行以下命令：

```
$ npm install -g vue-cli
```

构建完了之后，随便进入一个我们事先准备好的目录，比如demo目录，然后在目录中做初始化操作：

```
$ vue init webpack myProject
```

webpack参数是指myProject这个项目将会在开发和完成阶段帮你自动打包代码，比如将js文件统一合成一个文件，将CSS文件统一合并压缩等。要是不知道webpack的话，建议先了解下为好，当然不了解也不影响我们接着往下走。

init的过程中会问你给项目定义一些描述，版本之类的信息，可以不管，一直输入y确定跳过，完成之后出现以下界面，红框部分会提示你接下来要做的操作，按照它的提示继续敲代码就对了。

![img](https://mc.qcloudimg.com/static/img/f1aea419de92a62ee1e64cf1a3da0033/image.png)

```
cd myProject
npm install
npm run dev
```

npm install 是安装项目所需要的依赖，简单理解就是安装一些必要的插件，需要等一段时间；

npm run dev 是开始执行我们的项目了，一旦执行这个命令之后，等一小会，浏览器应该会自动帮你打开一个tab为`http://localhost:8080/#/`的链接，这个链接就是我们本地开发的项目主页了，如果没有，说明出错了。请移步到评论区回复吧。。。

(PS：开发完成后执行npm run build会编译我们的源代码生成最终的发布代码，在dist目录下)

![img](https://mc.qcloudimg.com/static/img/873285e43241696140f6e73c83f9ae39/image.png)

看看Vue都给我们生成一些什么文件，这其中我们需要关注的是以下文件

![img](https://mc.qcloudimg.com/static/img/883d3ceeba7b42ef30052bf0be488d26/image.png)

==package.json保存一些依赖信息，config保存一些项目初始化配置，build里面保存一些webpack的初始化配置，index.html是我们的首页，除了这些，最关键的代码都在src目录中，index在很多服务器语言中都是预设为首页，像index.htm，index.php等；打开build目录中的`webpack.base.conf.js`，会看到这样的代码==

![img](https://mc.qcloudimg.com/static/img/3d8d0974f3b7559e2089ff31ae11579b/image.png)

说明我们的入口js文件在src目录中的main.js，接下来我们就分析下这些初始化代码先；

## 跟着代码走

Vue的核心架构，按照官方解释和个人理解，主要在于组件和路由两大模块，只要理解了这两大模块的思想内容，剩下API使用就只是分分钟的事情了。所以在我的系列文中，会围绕组件和路由教大家开发一个前端组件库，这个过程也是我个人学习的练手项目，个人觉得一步步做下来之后，对Vue的理解就可以算是出师了，胜过读10遍书籍文档，那是后话了，先让我们看看最基本的Vue生成的默认代码吧！

```
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
})
```

先是第一句

```
import Vue from 'vue'
```

这句很好理解，就像你要引入jQuery一样，vue就是`jquery-min.js`，然后Vue就是$；然后又引入了`./App`文件，也就是目录中和`main.js`同级的`App.vue`文件；在Vue中引入文件可以直接用import，文件后缀名可以是`.vue`，这是Vue自己的文件类型，之前说的webpack会将js和css文件打包，同样的道理，在webpack中配置vue插件后（项目默认配置），webpack就可以将.vue类型的文件整合打包，这和nodeJs中require差不多的道理。

说回App.vue这个文件，这是一个视图（或者说组件和页面），想象一下我们的index.html中什么也没有，只有一个视图，这个视图相当于一个容器，然后我们往这个容器中放各种各样的积木（其他组件或者其他页面），App.vue中的内容我们后面说；

```
import router from './router'
```

这句代码引入一段路由配置，同样的后边说（很快就说到的不用急）

接下来的 new Vue实例化，其实就相当于平时我们写js时候常用的init啦，然后声明el：`'#app'`，意思是将所有视图放在id值为app这个dom元素中，components表明引入的文件，即上述的`App.vue`文件，这个文件的内容将以`<App/>`这样的标签写进去`#app`中，总的来说，这段代码意思就是将`App.vue`放到`#app`中，然后以`<App/>`来指代我们的`#app`。

```
import Vue from 'vue'
import App from './App'/*引入App这个组件*/
import router from './router'/*引入路由配置*/

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',/*最后效果将会替换页面中id为app的div元素*/
  router,/*使用路由*/
  template: '<App/>',/*告知页面这个组件用这样的标签来包裹着,并且使用它*/
  components: { App }/*告知当前页面想使用App这个组件*/
})
```

## 单页面组件

好了，现在打开我们的App.vue文件，在Vue中，官网叫它做组件，单页面的意思是结构，样式，逻辑代码都写在同一个文件中，当我们引入这个文件后，就相当于引入对应的结构、样式和JS代码，这不就是我们做前端组件化最想看到的吗，从前的asp、php也有这样的文件思想。

```
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

node端之所以能识别`.vue`文件，是因为前面说的webpack在编译时将`.vue`文件中的html，js，css都抽出来合成新的单独的文件。

单页面组件会在后面的实战中完整体现，这里先不做过多描述；

看到我们文件内分为三大部分，分别是`<template><script><style>`，很好理解结构，脚本，样式；script就像node一样暴露一些接口，可以看到我们的template标签中除了一张图片之外就只有一行代码：`<router-view></router-view>`

```
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
  </div>
</template>
```

回看我们的浏览器页面中，图片是有了，可下面的文本和链接的代码写在哪里了呢？这里就要开始涉及路由了。

![img](https://mc.qcloudimg.com/static/img/5adcaca2d1d12b21ebad766c2e287ec7/image.png)

## 路由

这里补充下路由的大致概念：传统的php路由是由服务器端根据一定的url规则匹配来返回给前端不同的页面代码，如以下地址

<https://isux.tencent.com/about> 和 <https://isux.tencent.com/recruit>

注意这里只有about和recruit，这些不带`xxx.html`的地址其实是服务器端经过一层封装指定到某些文件上去。同样的道理，前端也可以根据带锚点的方式实现简单路由（不需要刷新页面）

<https://zhitu.isux.us/index.php/preview/install#mac>

其中#mac就是我们的锚点路由，注意开始我们在浏览器中打开的地址：

`http://localhost:8080/#/，`

路由让我们可以访问诸如`http://localhost:8080/#/about/` 或者 `http://localhost:8080/#/recruit`这些页面的时候不带刷新，直接展示。现在回到我们刚才打开的`App.vue`文件中看这行代码

`<router-view></router-view>`

这句代码在页面中放入一个路由视图容器，当我们访问`http://localhost:8080/#/about/`的时候会将about的内容放进去，访问`http://localhost:8080/#/recruit`的时候会将recruit的内容放进去

![img](https://mc.qcloudimg.com/static/img/f2296800e7441159f370fe20d2843804/image.png)

如此看来，无论我们打开`http://localhost:8080/#/about/` 还是`http://localhost:8080/#/recruit`页面中的图片都是公用部分，变得只是路由器里面的内容，那么路由器的内容谁来控制呢？

前面说的`src/main.js`中有一句引入路由器的代码。

`import router from './router'`

现在就让我们打开router目录下的js文件。

```
import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'
import About from '@/components/about'
import Recruit from '@/components/recruit'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
},
    {
      path: '/about',
      name: 'about',
      component: About
},
    {
      path: '/recruit',
      name: 'recruit',
      component: Recruit
}
  ]
})
```

==前面先引入了路由插件`vue-router`，然后显式声明要用路由 `Vue.use(Router)`== 。注意到Hello，About等都是页面（也可以是组件），接着注册路由器，然后开始配置路由。

路由的配置应该一目了然，给不同的path分配不同的页面（或组件，页面和组件其实是一样的概念），name参数不重要只是用来做识别用的。看到这里就可以明白，前面说的红色框的内容，其实就是Hello里面的内容，打开components目录下的Hello.vue就能明白了。

![img](https://mc.qcloudimg.com/static/img/5adcaca2d1d12b21ebad766c2e287ec7/image.png)

到这里就可以完成路由的配置，我个人习惯喜欢把页面放在pages目录下，组件放在components目录下，可能有人会问如果要访问`http://localhost:8080/#/about/me`的话要如何配置呢，很简单只要给路由加多一个子路由配置 `children` ，如下：

```
{
      path: '/blog',
      name: 'blog',
      component: Blog,
      children: [
        {
          path: '/',
          component: page1
        },
        {
          path: 'info',
          component: page2
        }
      ]
    }
```

访问/blog的时候会访问Blog页面，Blog里面放个路由器就可以了，然后访问`http://localhost:8080/#/blog/`的时候会往路由容器中放置page1的内容，访问`http://localhost:8080/#/blog/info`的时候会往路由容器中放置page2的内容

```
//blog.vue
<template>
    <div>公用部分</div>
    <router-view></router-view>
</template>
```

## 小结

贯穿我们刚才学习的过程，从初始化到页面展示，Vue的页面架构流程大概是这样的

![img](https://mc.qcloudimg.com/static/img/d63005a5d785358289fab9f0ea997aff/image.png)

总结下前面讲的内容先：

1. 搭建环境
2. 代码逻辑
3. 单页面组件（简单带过）
4. 路由
5. 子路由

以上的流程就是我们刚开始接触Vue时候的简单介绍，在之前就说过学习Vue能掌握组件和路由的基本概念之后，对于我们后续了解他的工作机制有着很大的帮助，**本篇章我们只是简单介绍了单页面组件，在下一篇文章中，我们将通过一个实战的项目，来充分了解组件化在Vue构建中的重要性。**

时间不早了，我也该回去睡觉了，消化一下，我们下一篇文章见~~~

文末附上所有相关代码和官方文档地址~~~

<http://cn.vuejs.org/v2/guide/>



附件：

**[src.zip](https://ask.qcloudimg.com/raw/yehe-133f028/qiwgf9qoup.zip)

原创声明，本文系作者授权云+社区-专栏发表，未经许可，不得转载。

如有侵权，请联系 zhuanlan_guanli@qq.com 删除。







# 包学会之浅入浅出Vue.js：升学篇

> 蔡述雄，现腾讯用户体验设计部QQ空间高级UI工程师。智图图片优化系统首席工程师，曾参与《众妙之门》书籍的翻译工作。目前专注前端图片优化与新技术的探研。

上一篇[《包学会之浅入浅出Vue.js：开学篇》](https://www.qcloud.com/community/article/430630001490779316?fromSource=gwzcw.60069.60069.60069)中，我们初步了解单页面组件这个概念，现在通过一个项目，来进一步解析组件的应用吧，Go~

## 需求背景

组件库是做UI和前端日常需求中经常用到的，把一个按钮，导航，列表之类的元素封装起来，方便日常使用，调用方法只需直接写上`<qui-button></qui-button>`或者`<qui-nav></qui-nav>`这样的代码就可以，是不是很方便呢，接下来我们将要完成以下页面：

![img](https://blog-10039692.file.myqcloud.com/1490871464533_919_1490871464762.png)

这是我们组件库的首页，包含三个子页面，按钮页面、列表页面、导航页面；点击进去子页面会由路由来配置。先看我们的目录结构：

![img](https://blog-10039692.file.myqcloud.com/1490871479139_3267_1490871479277.png)

pages目录存放我们的页面，包括首页和三个子页面；components目录存放我们的具体组件，包括按钮组件，箭头组件，列表组件和导航组件（组件和页面其实是一样的文件类型，只是由于功能不一样，我们就叫不同的称呼）

先看路由配置的代码吧！

## 路由配置

```
import Vue from 'vue'
import Router from 'vue-router'
// 引用页面模板->供路由使用
import index from '../pages/index.vue'
import pageQuiButton from '../pages/pageQuiButton.vue'
import pageQuiList from '../pages/pageQuiList.vue'
import pageQuiNav from '../pages/pageQuiNav.vue'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'index',
      component: index
    },
    {
      path: '/btn',
      name: 'btn',
      component: pageQuiButton
    },
    {
      path: '/list',
      name: 'list',
      component: pageQuiList
    },
    {
      path: '/nav',
      name: 'nav',
      component: pageQuiNav
    }
  ]
})
```

有了上一篇的分析之后，这里应该很容易看出来几个路由地址

首页：`http://localhost:8080/#/`

按钮子页：`http://localhost:8080/#/btn`

列表子页：`http://localhost:8080/#/list`

导航子页：`http://localhost:8080/#/nav`

具体每一页的内容分别对应每一页的.vue文件，不知大家是否还记得入口页`App.vue`，这个文件承载着一些公用的元素，还有就是一个路由容器，我们的首页`index.vue`到时候也是挂载在路由容器中的，看看`App.vue`的代码

## 入口页App.vue

```
<template>
  <div id="app">
    <h1 class="page-title"><a href="#/">开发组件库</a></h1>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'app'
}
</script>

<style scoped>                             <--
  @import './assets/css/App.css';
</style>
```

简单分析一下入口页的代码，**h1标签是一个公用元素**，也就是说到时候每个子页面都会带着这个h1，他的作用就是方便我们快速回到首页，子页面的内容会注入到`router-view`中。这里值得关注的地方是style标签，我们可以在style标签里面直接写样式，也可以**直接引入一个样式文件，==scoped关键字表示这个样式是私有的==**，也就是说，即使两个组件写着一样的`#app{}`样式也不会冲突，程序会加上**命名空间**，这也就是为什么在script标签中有个name参数。

## 首页index.vue

```
<template>
  <div class="mod-module mod-parallel">
    <div class="img-list type-full">
      <div class="img-box">
        <p class="img-item">
          <a class="page-link" href="#/btn">按钮</a>
        </p>
      </div>
      <div class="img-box">
        <p class="img-item">
          <a class="page-link" href="#/list">列表</a>
        </p>
      </div>
      <div class="img-box">
        <p class="img-item">
          <a class="page-link" href="#/nav">导航</a>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
 @import './css/index.css';
</style>
```

首页的代码也是非常简单，和我们平时写html差不多，就是几个跳转链接跳到对应的子页面，程序运行的时候，会将`<template>`标签里面的内容都注入到App.vue页面中的`router-view`标签中，从而实现无刷新的路由跳转。

从下面的内容开始，我们的知识将会深入一些。我们先不急着看其他几个子页面，因为子页面里面只是引用对应的组件，所以我们先从组件开始入手。

## 按钮组件quiButton.vue

```
<template>
  <button class="qui-btn">
    <span>{{msg}}</span>
  </button>
</template>

<script>
  export default {
        data:function(){
            return {
                msg:'下载'
            }
        }
  }
</script>
<style scoped>
  @import './css/reset.import.css';
  @import './css/qui-btn.import.css';
</style>
```

按钮组件很简单，就是一个正常的button标签，script标签中暴露这个组件的data属性（data是Vue的属性值，不是乱写的~~）。当按钮组件被初始化的时候，**msg自定义属性会被绑定到<span>标签中的{{msg}}中**，两个花括号用来绑定属性，这种写法学过模版化前端代码的人应该都比较熟悉。这里需要注意一个地方，**如果不是组件的话，正常data的写法可以直接写一个对象，比如data：{ msg ： ' 下载 ' }，但由于组件是会在多个地方引用的，JS中直接共享对象会造成引用传递，也就是说修改了msg后所有按钮的msg都会跟着修改，所以这里用function来每次返回一个对象实例。**

这就是一个非常简单的按钮组件，结构、样式+文案。

这时候问题来了，按钮中的文案我希望可以异化，不能每次都初始化一个叫做“下载”文案的按钮吧，希望可以以属性的方式来使用，比如这样子写就可以改变我们的按钮文案：

```
<qui-btn msg="确定" class="small"></qui-btn>
```

没问题，属性的接口暴露只需要写在props里面就可以了，如下所示修改下script标签的内容：

```
<script>
  export default {
    props: {
      msg: {
        default: '下载'
      }
    }
  }
</script>
```

把属性写在props里面，就可以暴露给其他页面调用了，在组件中，**props是专门用来暴露组件的属性接口的**，这里给了一个默认值`‘下载’`，后面我们要使用的话，只需要`<btn msg="确认"></btn>` 就可以修改按钮的默认文案了。

我们在上一篇文章的开头就讲了Vue是数据驱动模式的，当我在btn结构写上`msg="确认"`的时候，对应script里面的msg属性就会自动修改了。

## 按钮事件

按钮总少不了点击事件吧，那在Vue中怎么绑定事件呢，用methods属性，看下代码：

```
<template>
  <button class="qui-btn" v-on:click="btnClickEvent">
    <span>{{msg}}</span>
  </button>
</template>

<script>
  export default {
    props: {
      msg: {
        default: '下载'
      }
    },
    methods: {    //绑定事件的关键代码
      btnClickEvent: function(){
        alert(this.msg);
      }
    }
  }
</script>
```

methods属性中可以写任何的自定义函数，写完之后绑定的方式也很简单，在button上写关键字`v-on:click`，把对应的事件写上就可以了，以上代码实现的就是点击按钮弹出按钮中的文案，`v-XXX`是Vue里的一些关键字，叫做指令，我们后面会慢慢学到更多的指令；`v-on:click`可以缩写为`@click`，当然还有其他的事件比如`v-on:tab`等等；

## 使用按钮组件pageQuiButton.vue

现在我们大致做了一个按钮组件了，那么怎么调用它呢，去到我们的pageQuiButton子页面。

```
//pageQuiButton.vue
<template>
  <div id="pageQuiButton">
    <!--使用-->
    <qui-btn msg="确定" class="small"></qui-btn>
  </div>
</template>
<script>
  import quiBtn from '../components/quiButton.vue' /*引用*/
  export default {
    name: 'pageQuiButton',
    components: {
      'qui-btn': quiBtn /*注册自定义标签*/
    }
  }
</script>
```

从script开始解析，首先引入我们的组件赋值给变量quiBtn，使用时候直接将quiBtn作为对象的一部分写进**components属性**，这是Vue用来存储引用组件的关键字，同时对应我们自定义的标签 `"qui-btn"`，完成这些操作之后，我们就可以在template中使用自定义的按钮组件`<qui-btn>`上面也说了用msg属性来自定义按钮的文案。完成之后，我们就可以在页面中看到具体效果，点击按钮弹出对应的文案。

![img](https://blog-10039692.file.myqcloud.com/1490872991423_9914_1490872991543.png)

上述我们将按钮事件写成默认的`alert(this.msg)`，如果有些按钮想要异化怎么办。之前说了msg属性可以支持自定义，那么按钮的点击事件如何支持自定义呢？

```
//pageQuiButton.vue
//监听子组件的事件
<qui-btn v-on:btnClickEvent="doSth" msg="我可以点击" ></qui-btn>
```

上面的代码在引用组件的时候，注册了一个事件，这个btnClickEvent事件是之前我们在按钮组件中绑定到按钮的click事件中的，然后我们给这个事件一个自定义的方法doSth，同时，在script中声明这个自定义的方法如下：

```
//pageQuiButton.vue
//页面中引用子组件并监听子组件的事件
<script>
  import quiBtn from '../components/quiButton.vue'
  export default {
    name: 'pageQuiButton',
    components: {
      'qui-btn': quiBtn
    },
    methods: {
      doSth: function(){
        alert('你点击了组件的click:btnClickEvent');
      }
    }
  }
</script>
```

专业一点的说，这种做法叫做监听，由引用方（暂且叫做父组件）监听子组件的内置方法；同时在子组件中，需要触发这个事件，以下是在子组件中的关键代码：

```
//quiButton.vue
//子组件中的代码
<script>
  export default {
    props: {
      msg: {
        default: '下载'
      }
    },
    methods: {
      btnClickEvent: function(){
        alert("先弹出默认的文案");
        this.$emit('btnClickEvent');//关键代码父组件触发自定义事件
      }
    }
  }
</script>
```

==这里的关键代码就是`$emit`，也叫触发机制，父组件监听，子组件触发。==如果觉得绕，以下描述可能会比较好理解：**小B（子组件）有一个电话号码（子组件注册的事件），有一天小B把电话号码告诉了小A（父组件），让小A打电话给他，于是小A就拨打了小B的电话号码（监听），这时候整个沟通流程没有结束，必须要小B接听了电话（触发），两人之间才算完成了打电话这件事情。**

完成这步之后，引用方（父组件）就可以给不同子组件调用不同的事件处理了：

```
<qui-btn v-on:btnClickEvent="doSth1" msg="确定" ></qui-btn>
<qui-btn v-on:btnClickEvent="doSth2" msg="取消" ></qui-btn>
<script>
/*这里只是简单展示*/
    methods: {
      doSth1: function(){
        alert('111');
      },
      doSth2: function(){
        alert('222');
      }
    }
</script>
```

## 给按钮加图标

有时候单纯的文案异化还不够，比如一些按钮是图标+文字类型的，而且图标还可能不一样，那应该怎么办呢？

![img](https://blog-10039692.file.myqcloud.com/1490873116729_7495_1490873116848.png)

如果按钮组件的结构除了开发时候预设的那些dom结构之外，允许我们在调用的时候添加一些自己想要的结构，那是不是解决了呢，是的，Vue早就为我们考虑了这一点，他就是**slot**标签。

下面给我们的按钮组件加上一段结构

```
//quiButton.vue
<template>
  <button class="qui-btn" v-on:click="btnClickEvent">
    <slot name="icon"></slot><!--重点在这里-->
    <span>{{msg}}</span>
  </button>
</template>
```

加入了关键字slot并赋予一个name值之后，我们再看看引用如何使用

```
//pageQuiButton.vue
<qui-btn msg="下载" class="with-icon">
  <img slot="icon" class="ico" src="xxx.png" />
</qui-btn>
```

==img上有个关键字`slot="icon"`对应组件中的`name="icon"`，渲染的时候，会将img整个替换掉组件中的对应name的`<slot>`标签，其实很好理解，slot的翻译是插槽的意思，相当于把img这块内容插到一个名叫icon的插槽里面去。==

## 中场休息一下

学到这里，我们已经学会了用props给按钮自定义文案，用on和emit给按钮自定义点击触发，用slot给按钮添加一些自定义结构。**当你回头去翻文档的时候，你会发现props，事件，slot这三样刚好就是学习组件通讯中最最最关键的三个环节。将这三个环节以实际案例解析出来后，好像也没有那么难了吧~！**

上述我们已经讨论了如何制作一个按钮组件，以及如何使用我们的按钮组件。

![img](https://blog-10039692.file.myqcloud.com/1490873224108_8909_1490873224225.png)

接下来我们通过制作一个导航组件，来了解Vue中对于for循环的巧妙使用。

## 导航组件quiNav.vue

![img](https://blog-10039692.file.myqcloud.com/1490873272900_1173_1490873273020.png)

我们将完成这样一个导航组件，点击导航中的tab，可以给当前tab加上一个active类，同时切换底部的黄色滑条，并且输出当前tab的文案，同时支持自定义事件。

由于在现实项目中，我们导航的tab个数是不定的，所以制作组件的时候，我们希望可以暴露一个属性来支持导航的tab个数，而tab的长相和应用其实是一样的，那么这时候我们可以用一个for循环来输出每一个tab。先看看关键代码：

```
//quiNav.vue
<template>
  <div class="qui-nav nav-type-1">
    <a v-for="(item, index) in items" ><!--关键代码v-for-->
      <span class="nav-txt">{{item.text}}</span>
    </a>
  </div>
</template>

<script>
  export default {
    data:function(){
      return {
        items:[
          {
            text: '首页',
            active : true
          },
          {
            text: '列表',
            active : false
          },
          {
            text: '关于',
            active : false
          },
          {
            text: '招聘',
            active : false
          }
        ]
      }
    }
    }
  }
</script>
```

该段代码的关键地方在于a标签上`v-for`关键字（还记得我们在前面说过的v-on绑定事件吗，v-XXX关键字是Vue预留的）可以把它理解为js中的for in 循环，items是我们在data里面定义的对象（还记得为什么data要写在function中返回吗？）。`v-for="(item,index) in items"`暴露了item和index两个接口，这是Vue提供的，代表items中的每一项以及该项对应的下标，接着我们就可以在标签中使用绑定`｛｛item.text｝｝`了。

这段代码理解了之后，我们再延伸一个动态添加class的概念。我们希望每个tab都有默认的class类名(比如`nav-item`类)，在点击每个tab的时候，当前tab添加active类，其他的tab删除这个active类。在Vue怎么实现呢？

## 动态类名

```
//quiNav.vue
<template>
  <div class="qui-nav nav-type-1">
    <a v-for="(item, index) in items" :class="[commonClass,item.active ? activeClass : '']" >
      <span class="nav-txt">{{item.text}}</span>
    </a>
  </div>
</template>

<script>
  export default {
    data:function(){
      return {
        commonClass:'nav-item',
        activeClass:'active',
        items:[
            ...//数据
        ]
      }
    }
  }
</script>
```

在template中添加了一句关键代码

```
:class="[commonClass,item.active ? activeClass : '']"
```

`:class`给组件绑定一个class属性（类似jQuery中的attr方法），这里的写法是缩写，他的全拼应该是v-bind:（又一个v-XXX写法）。注意到最前面有个冒号，`：class=XXX`和`class=XXX`的区别在于不带冒号的是静态的字符串绑定，带冒号的是动态的变量绑定。我们给class绑定了一个数组，这个数组带有变量，先看commonClass，这个变量在data中定义了，然后数组的第二个元素是一个JS的三元运算符：`item.active?activeClass:''`，当每个item中的active值为true时，绑定activeClass变量对应的类，如果为false，则为空。最后的结果是当item.active为true时候，tab的class值为`'nav-item active'`，当为false，就只有`'nav-item'`。

上面的代码可以理解的话，那么我们切换tab的active类，就转换为修改每个item里面的active的值（再次体现数据驱动）。

那么问题来了，怎么去修改每个item里面的active值呢？没错，给每个tab绑定一个点击事件，当点击事件触发的时候，修改当前tab对应item的active值。于是代码变成了如下：

```
<template>
  <div class="qui-nav nav-type-1">
    <a v-for="(item, index) in items" :class="[commonClass,item.active ? activeClass : '']" v-on:click="navClickEvent(items,index)" >
      <span class="nav-txt">{{item.text}}</span>
    </a>
  </div>
</template>

<script>
  export default {
    data:function(){
      return {
        commonClass:'nav-item',
        activeClass:'active',
        items:[
          {
            text: '首页',
            active : true
          },
          ......
        ]
      }
    },
    methods:{
      navClickEvent:function(items,index){
        /*默认切换类的动作*/
        items.forEach(function(el){
          el.active = false;
        });
        items[index].active = true;
        /*开放用户自定义的接口*/
        this.$emit('navClickEvent',items,index);
      }
    }
  }
</script>
```

我们利用for循环给每个a标签绑定了一个click事件，对应methods中定义的navClickEvent，接收两个参数items和index（你也可以传人item和index，看个人代码喜好），然后当点击的时候，把items中的每个item.active置为false，把当前的tab的active值置为true，这样就可以动态切换active类了。最后再触发一次自定义事件（参考按钮制作自定义事件）。

以上就是我们导航组件的内容了，回想下我们做了啥？**for循环输出每个tab，为每个tab绑定动态的class类名，同时在点击事件中动态切换类（底部的小黄条其实是利用active类做的CSS）**

## 小结

回顾下我们这一篇章都学了什么内容。

1. 页面路由的配置
2. 按钮组件自定义属性props
3. 按钮组件自定义事件 $on $emit
4. 按钮组件自定义子块slot
5. for循环实现导航组件
6. 动态类名

上述内容已经基本上涵盖了组件的重要知识点，主要是父组件（页面）和子组件之间的调用和通讯（数据交互绑定），好好消耗一下我们会发现，其实Vue的总体逻辑思想和jQuery是一样的，毕竟最后都回归到javascript，只是由于代码设计角度的不同，我们可能看到和以前调用jQuery时候的写法不一致，但其实都有对方的影子在里面，相信理解了Vue的代码思想之后，以后我们学习React等其他类似的框架的时候，也会比较得心应手了。

下一篇文章[《包学会之浅入浅出Vue.js：结业篇》](https://www.qcloud.com/community/article/560608001490929432?fromSource=gwzcw.60073.60073.60073)中，我们将会学习如何用多个组件来组成一个大的组件，也就是真正意义上的父子组件之间的关系。再忍耐一下，就可以出山了，新领域的大门就在前面，让我们大步往前跨吧。

文末附上所有相关代码和官方文档地址~~~

<http://cn.vuejs.org/v2/guide/>



附件：

**[scrp.zip](https://ask.qcloudimg.com/raw/yehe-133f028/f9fh94onaf.zip)

原创声明，本文系作者授权云+社区-专栏发表，未经许可，不得转载。

如有侵权，请联系 zhuanlan_guanli@qq.com 删除。





# 包学会之浅入浅出Vue.js：结业篇

> 蔡述雄，现腾讯用户体验设计部QQ空间高级UI工程师。智图图片优化系统首席工程师，曾参与《众妙之门》书籍的翻译工作。目前专注前端图片优化与新技术的探研。

在第一篇[《包学会之浅入浅出Vue.js：开学篇》](https://cloud.tencent.com/developer/article/1020337)和上一篇[《包学会之浅入浅出Vue.js：升学篇》](https://cloud.tencent.com/developer/article/1020338)的学习中，我们首先了解了Vue环境的搭建以及两个重要思想——路由和组件的学习，通过组件库中的按钮组件和导航组件，相信大家也开始了解相应的知识点，接下来我们会详细分析下如何完成由多个组件组成一个复用组件的开发流程。

下面先看看我们的需求

## 列表组件quiList.vue

本节我们主要要完成这样一个列表功能，每一行的列表是一个组件，列表内可能出现按钮组件或者箭头组件，点击按钮组件可以自定义事件，同时可以根据不同的参数来决定当前列表是带按钮的列表or带箭头的列表。

 ![img](https://blog-10039692.file.myqcloud.com/1490929795562_1084_1490929795668.png)

首先看看quiList.vue

```
//quiList.vue
<template>
  <div class="qui-list">
    <span class="list-tips">{{tipsText}}</span>
    <qui-btn v-on:btnClickEvent="btnClickEvent" :msg=msg class="small"></qui-btn>
  </div>
</template>

<script>
  import quiButton from '../components/quiButton.vue'
  export default{
    props:{
      msg: {
        default: '下载'
      },
      tipsText: {
        default: '默认的文案'
      }
    },
    components: {
      'qui-btn': quiButton
    }，
    methods:{
      btnClickEvent:function(){
          alert('按钮点击事件')
      }
    }
  }
</script>
```

上面的知识点基本上就是我们之前学过的，只不过记住**quiList本身是一个组件，而在这个组件里面，我们又引入了按钮组件quiButton**，也就是组件内引用组件，实际上就是组件的嵌套，注意到这里`：msg=msg`的使用，这里冒号表示绑定的是一个变量msg，然后这个属性通过props暴露出去(本身在按钮中就暴露了msg给列表组件使用)，借用下面一张图理解下：

![img](https://blog-10039692.file.myqcloud.com/1490929888497_8898_1490929888715.png)

至于点击事件，也是我们之前学习过的事件的绑定。现在引入一个新问题，**是否有一个参数，可以决定列表组件的右侧是放置按钮组件呢？还是箭头组件。**

## 动态组件

Vue中提供了一些特定关键字：is和特定的结构`<component>`来生成动态组件，让我们修改下script里面的内容先：

```
<script>
  import quiButton from '../components/quiButton.vue'
  import quiArrow from '../components/quiArrow.vue'
  export default{
    props:{
      msg: {
        default: '下载'
      },
      tipsText: {
        default: '默认的文案'
      },
      currentView:{
        default: 'qui-btn'
      }
    },
    components: {
      'qui-btn': quiButton,
      'qui-arrow': quiArrow
    },
    methods: {
      clickEvent: function () {

      }
    }
  }
</script>
```

首先我们先Import多一个箭头组件，在components中添加一个自定义标签`‘qui-arrow’`，注意到我们多了一个currentView的自定义属性，默认值是`qui-btn`，现在再看看template标签里面写什么：

```
<template>
  <div class="qui-list">
    <span class="list-tips">{{tipsText}}</span>
    <component :is="currentView" v-on:btnClickEvent="clickEvent" :msg=msg class="small"  keep-alive></component>
  </div>
</template>
```

==我们把`qui-btn`标签去掉了，取而代之的是一个component标签，这是Vue自带的一个标签，可以把它当作一个容器，这个容器可以用来装按钮，也可以用来装箭头。决定这个容器装的是哪个组件的关键代码在于：`is="currentView"`，当currentView的值为`qui-btn`的时候，这个容器就是按钮组件，当它是`qui-arrow`的时候，就是箭头组件。而我们刚才给这个变量定义的默认值是`qui-btn`。==

==`keep-alive`关键字保持这个组件在内存中是常驻的，由于动态组件可能需要动态切换，这样保持组件活跃可以减少组件变化时候的内存消耗。==

可以看到我们的component上还保留着按钮的点击事件和msg信息，这些没有关系，只要箭头组件中不出现同样的变量就不会发生冲突。

```
<qui-list tipsText="自定义文案，默认右边是按钮" msg="弹层"></qui-list>
<qui-list v-on:btnClickEvent="test"></qui-list>
<qui-list ref="child1" tipsText="最右边是箭头" currentView="qui-arrow"></qui-list>
```

使用列表组件的时候，只需要给暴露出来的currentView指定一个值，就可以决定右侧是按钮还是箭头了。注意最后一个`qui-list`上有一个ref的属性，这个属性代表组件集合，当页面中有很多组件的时候，可以通过几种方法来获取对应的某个组件的信息：

```
console.log(this.$children[0].msg);//通过数组获取
console.log(this.$refs.child1.msg);//通过对象集合获取
```

其实关于动态组件，不一定要用：`is+component`来实现，在Vue中有一个指令叫做`v-if / v-else / v-else-if`，统称判断指令，配合展示指令v-show，可以根据指定的值来决定对应的组件是否应该展示，另外这种做法我不展示了，就当做一个作业吧，有兴趣的还是建议实战一下，毕竟我们也只是教大家入门学习，后面还是希望大家能够自己去扩展学习。

## 生命周期

这里简单讲一下什么是组件的生命周期，上面我们通过refs来获取组件对象的信息，那么在什么时候或者说哪个时机点去做这件事呢，组件从引用到调用到销毁（比较少操作）有以下几个关键回调函数：

```
<script>
  export default {
    components: {
      'qui-list': quiList
    },
    beforeCreate:function(){},//组件实例化之前
    created:function(){},//组件实例化了
    beforeMount:function(){},//组件写入dom结构之前
    mounted:function(){//组件写入dom结构了
      console.log(this.$children);
      console.log(this.$refs);
    },
    beforeUpdate:function(){},//组件更新前
    updated:function(){},//组件更新比如修改了文案
    beforeDestroy:function(){},//组件销毁之前
    destroyed:function(){}//组件已经销毁
  }
</script>
```

所以要想使用refs的内容，就需要在组件写入dom之后才能开始调用哦！

## 我还需要学什么

目前为止，我们三篇文章已经学了大部分的关于组件和路由的知识，当然这并不是Vue的全部，只是相对于其他的知识点，这些可以算是一个垫脚石，看懂了这些，对后面其他API的应用，帮助很大。下面我列举一些其他的，后续大家可以去官网查看资料的一些关键点，其实都不难，只要有一些小小的项目demo实践，你会发现Vue也不过如此。

### 过渡

过渡其实就是CSS3动画，transition这些，只是写CSS3变成好像在写JS一样，有点类似于greenSock的一些思想。

### 指令

目前为止我们学习了一些常用指令，像v-on，v-bind，v-for，还有几个常用的像刚才提到的判断指令和v-show指令，还有v-model指令（主要用于input等表单组件）。当知道指令作用的时候，学习起来其实并不难。

### Render

渲染这个方法是我觉得应该用心去学习的，它可以方便我们写出更好的面向对象的组件，而学习它的成本在于这个接口更接近于原生JS代码的使用。如果有需要，后续也可以写一篇关于Render的文章。

## 总结

三篇系列文暂时在这里告一段落，有些童靴可能到这里还是觉得没有学会Vue，对不起，可能是我的标题太夸张了，也可能因为我的例子还不够清晰，文笔也还不好理解。不过没关系，回顾我们的学习历程，你可以按照这个知识点的学习过程，去找更多的文章，毕竟“熟读唐诗三百首，不会作诗也会吟”嘛。当然，学习过程中我们自己更多的练习和尝试才能锻炼巩固知识。至于浅入之后是浅出还是深出，还是要靠大家自己去定义了！

文末附上所有相关代码和官方文档地址~~~

<http://cn.vuejs.org/v2/guide/>



附件：

**[src.zip](https://ask.qcloudimg.com/raw/yehe-133f028/hrww6bzjaa.zip)