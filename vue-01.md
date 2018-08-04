

# 基础搭建



**引入vue**

```html
<script src="https://cdn.bootcss.com/vue/2.5.13/vue.min.js"></script>
```



**示例**

```html
<div id="app"></div>

<script src="https://cdn.bootcss.com/vue/2.5.13/vue.js"></script>
<script>
/* ========== 全局组件 ========== */
Vue.component("global-component", {
  // 组件数据，必须是函数
  data: function () {
    return {}
  },

  // props 可以是数组或对象，用于接收来自父组件的数据
  props: [],

  // template 一个字符串模板作为 Vue 实例的标识 html
  template: '<div>这里是全局组件</div>',

})


/* ========== Vue 实例 ========== */
var app = new Vue({
  // 在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标
  el: '#app',

  // Vue 实例的数据对象
  data: {
    name: 'myName',
    a: 1
  },

  template: `<div>
      这里是模板内容
      <global-component></global-component>
      <local-component></local-component>
  </div>`,

  // beforeMount 在挂载开始之前被调用
  beforeMount () {
    console.log('Loading...')
  },

  // mounted   el被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。
  mounted: function () {
    console.log('Load the success')
    // axios.get().then().catch() // 调用 ajax
  },

  // methods 存函数。调用的时候执行
  methods: {
    plus: function () {
      this.a++
    }
  },

  // computed 存函数。实时计算，当数据变化的时候执行。
  // 所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。
  computed: {
    // 仅读取
    aDouble: function () {
      return this.a * 2
    },
    // 读取和设置
    aPlus: {
      get: function () {
        return this.a + 1
      },
      set: function (v) {
        this.a = v - 1
      }
    }
  },

  // wacth 存函数。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性
  watch: {
    a: function (val, oldVal) {
      // 监听 data.a
      console.log('new: %s, old: %s', val, oldVal)
    }
  },

  // 局部组件。将只在父组件模板中可用。# 注意加 s #
  components: {
    "local-component": {
      template: '<div>这里是局部组件</div>'
      // 其它参数请看全局组件
    }
  }
  
  //组件更新比如修改了文案
  updated: function () {},

})
</script>
```









## 选项 / 数据



### **el 绑定页面元素**

实例化 Vue ，其中`el`绑定一个元素，保存到实例 `app.$el` 下  

```html
<div id="app"></div>
<script>
  var app = new Vue({
    el: '#app'
  })
</script>

// 绑定的元素
console.log( app.$el === document.getElementById('app') )  ==> true
```





### data 数据



**实例的参数 data**

实例化 Vue 的数据参数在 data 对象，寄存在 `app.$data.name` 和 `app.name` 两者相等；

数据使用：在元素内使用双花括号，参数名对应 data 里的数据名

```html
<div id="app">{{ name }}</div>	<!-- 展示数据 -->
<script>
  var app = new Vue({
    el: '#app',
    data: {
      name: '数据'
    }
  })
</script>

// 实例化后数据的位置
console.log( app.$data.name === app.name )  ==> true
```

data 也可以使用外部的数据 `obj`

```js
var obj = { name: '数据' }	// 外部数据
var app = new Vue({
  el: '#app',
  data: obj		// 指向外部数据
})
```

 

**监听数据变化**

使用 `$watch` 监听的数据有变化时，触发回调

```js
  var app = new Vue({
    el: '#app',
    data: {
      name: '数据'
    }
  });
  
  // 监听 name 变化，执行回调  [新值] [旧值]
  app.$watch( 'name', function (newVal, oldVal) {
    console.log( newVal, oldVal )
  })
```



**v-once**

只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

```html
<div id="app" v-once>{{ name }}</div>	<!-- 只渲染一次 -->
<script>
  var app = new Vue({
    el: '#app',
    data: {
      name: '数据'
    }
  })
</script>
```



**v-html ， v-text**

更新元素的 `innerHTML` 。**注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译**。如果试图使用 `v-html` 组合模板，可以重新考虑是否通过使用组件来替代。

```html
<div id="app" v-html="name">
    <div v-html="html"></div>	// 会解析标签
    <div v-text="html"></div>   // 不会解析标签
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      html: '<h2>标题二</h2>'
    }
  })
</script>
```

result：

```html
<div id="app">
    <div><h2>标题二</h2></div>  ==>  标题二
    <div><h2>标题二</h2></div>  ==>  <h2>标题二</h2>
</div>
```



### computed  计算属性





## 指令



### v-bind 绑定



### v-on 事件



## 组件



### 全局组件





### 局部组件





# Vue + webpack



1. 安装 `node` 环境，

   在命令窗口下检查版本： `node -v`

   ​

2. 安装 `vue` ，

   命令窗口： `npm install vue-cli -g(全局安装)`

   安装目录： `C:\Users\Allen\AppData\Roaming\npm`

   ​

3. 新建vue项目文件夹，在文件夹下构建 项目

   命令窗口： `vue init webpack`



4. 安装依赖组件（项目目录下）

   命令窗口： `npm install`

   安装完成后有一个配置文件 `package.json` ，具体内容请往后看



5. 项目文件内容

   ```
   项目目录
   ｜--  build\        存放命令
   ｜--  config\       配置目录
   ｜--  dist\         编译后的代码
   ｜--  src\          写vue代码的
   ｜--  static\       存放 img js css 目录

   【/src/main.js】   运行的主文件
   【/src/App.vue】   vue模板（ <template> <script> <style> ）

   【/index.html】    承载src目录下的 所有代码
   ```

   ​

6. 命令

   ```
   运行项目
   # node run dev

   打包项目
   # node run build
   	编译到dist目录下
   ```

   ​

7. 配置文件 `package.json`

   ```json
   {
     "name": "webpack",        // 项目名
     "version": "1.0.0",       // 版本号
     "description": "A Vue.js project",    // 描述
     "author": "suyoulun <rianin5683@163.com>",    // 作者
     "private": true,
     "scripts": {
       "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",     // # npm run dev 运行的路径
       "start": "npm run dev",
       "unit": "jest --config test/unit/jest.conf.js --coverage",
       "e2e": "node test/e2e/runner.js",
       "test": "npm run unit && npm run e2e",
       "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
       "build": "node build/build.js"      // # node run build 打包工具文件
     },
     "dependencies": {     // 实际项目中需要用到的（生产环境）
       "vue": "^2.5.2",
       "vue-router": "^3.0.1"
       // vuex
     },
     "devDependencies": {      // 开发项目需要用到的（开发环境）
       "autoprefixer": "^7.1.2",
       "babel-core": "^6.22.1",
       "babel-eslint": "^8.2.1",
       "babel-helper-vue-jsx-merge-props": "^2.0.3",
       "babel-jest": "^21.0.2",
       "babel-loader": "^7.1.1",
       "babel-plugin-dynamic-import-node": "^1.2.0",
       "babel-plugin-syntax-jsx": "^6.18.0",
       "babel-plugin-transform-es2015-modules-commonjs": "^6.26.0",
       "babel-plugin-transform-runtime": "^6.22.0",
       "babel-plugin-transform-vue-jsx": "^3.5.0",
       "babel-preset-env": "^1.3.2",
       "babel-preset-stage-2": "^6.22.0",
       "babel-register": "^6.22.0",
       "chalk": "^2.0.1",
       "chromedriver": "^2.27.2",
       "copy-webpack-plugin": "^4.0.1",
       "cross-spawn": "^5.0.1",
       "css-loader": "^0.28.0",
       "eslint": "^4.15.0",
       "eslint-config-standard": "^10.2.1",
       "eslint-friendly-formatter": "^3.0.0",
       "eslint-loader": "^1.7.1",
       "eslint-plugin-import": "^2.7.0",
       "eslint-plugin-node": "^5.2.0",
       "eslint-plugin-promise": "^3.4.0",
       "eslint-plugin-standard": "^3.0.1",
       "eslint-plugin-vue": "^4.0.0",
       "extract-text-webpack-plugin": "^3.0.0",
       "file-loader": "^1.1.4",
       "friendly-errors-webpack-plugin": "^1.6.1",
       "html-webpack-plugin": "^2.30.1",
       "jest": "^22.0.4",
       "jest-serializer-vue": "^0.3.0",
       "nightwatch": "^0.9.12",
       "node-notifier": "^5.1.2",
       "optimize-css-assets-webpack-plugin": "^3.2.0",
       "ora": "^1.2.0",
       "portfinder": "^1.0.13",
       "postcss-import": "^11.0.0",
       "postcss-loader": "^2.0.8",
       "postcss-url": "^7.2.1",
       "rimraf": "^2.6.0",
       "selenium-server": "^3.0.1",
       "semver": "^5.3.0",
       "shelljs": "^0.7.6",
       "uglifyjs-webpack-plugin": "^1.1.1",
       "url-loader": "^0.5.8",
       "vue-jest": "^1.0.2",
       "vue-loader": "^13.3.0",
       "vue-style-loader": "^3.0.1",
       "vue-template-compiler": "^2.5.2",
       "webpack": "^3.6.0",
       "webpack-bundle-analyzer": "^2.9.0",
       "webpack-dev-server": "^2.9.1",
       "webpack-merge": "^4.1.0"
     },
     "engines": {
       "node": ">= 6.0.0",
       "npm": ">= 3.0.0"
     },
     "browserslist": [
       "> 1%",
       "last 2 versions",
       "not ie <= 8"
     ]
   }
   ```

   ​

## 代码规范

`test\.eslintrc.js` 规定了代码写法

**注释** 

- 注释标识符和内容之间必须有空格 `// 注释` `/* 注释 */`
- 对象属性的冒号后面必须有空格 `el: '#app'`
- 函数声明括号之间必须有空格 `function () {}`
- 定义的变量必须使用
- 不能加分号
- 缩进2个空格
- 逗号后面加空格





## 路由



### 单文件示例

**路由跳转**

把 实例、模板、路由 写在一个文件里时 `main.js`，

- `首先`引入插件 `vue`(VueJS) `vue-router`(路由) ，同时并启用 `Vue.use(Router)` 。
- 模板：实例下的模板为 `App` ，模板里 `<router-view></router-view>` 配合路由加载不同的模板（如 `index` `about` ），其中 `about` 下也有一个子路由 `us` 。`<router-link to="/">index</router-link>` 会转成a标签来点击，to 定义哈希值。哈希值路由加载的模板如下

		`http://localhost:8080/#/           ==>	index`
		`http://localhost:8080/#/about      ==>	about`
		`http://localhost:8080/#/about/us   ==>	us`

- 配置路由 `phth`(路由) `component`(模块名) `children`(子路由)

```js
import Vue from 'vue'
import Router from 'vue-router'

/** =============== 模版 =============== */
const App = {
  template: `<div id="app">
        <h2>主页面</h2>
        <router-link to="/">index</router-link>
        <router-link to="/about">about</router-link>
        <router-link to="/about/us">about/us</router-link>
        <router-view></router-view>
    </div>`
}
const index = {
  template: `<div>index模版</div>`
}
const about = {
  template: `<div>about模版 <router-view></router-view> </div>`
}
const us = {
  template: `<div>us模版</div>`
}

/** =============== 路由 =============== */
const router = new Router({
  routes: [
    {path: '/', component: index},
    {
      path: '/about',
      component: about,
      children: [
        {path: 'us', component: us}
      ]
    }
  ]
})

// 使用路由插件
Vue.use(Router)

// 设置为 false 以阻止 vue 在启动时生成生产提示。
Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  // components: { App },
  // template: '<App/>'
  render: h => h(App)
})
```



**传递数据**

1 . 地址匹配传值。 `http://localhost:8080/#/Url/data`

在路由 `paht: ':data'` 规定匹配规则，模板 `template` 使用双花括号 `{{ $route.params }}` 接收；

```js
const App = {
  template: `<div id="app">
        <router-link to="/Url/hello">Url:id</router-link>	<-- 地址传值
        <router-view></router-view>
    </div>`
}
const Url = {
  template: `<div> {{ $route.params }} </div>`		<-- 显示值
}

const router = new Router({
  routes: [
    {path: '/Url/:id', component: Url}		<-- 匹配地址，冒号接收值
  ]
})

结果：
{ "id": "hello" }
```



2 . 明文传值。 `http://localhost:8080/#/url?id=123`

路径链接 `<router-link :to="{ path: '/url', query: {id: 123} } >"` ， `path` 为路由地址 `query`为传值；在子组件 `$route.query` 接收。

```js
const App = {
  template: `<div id="app">
  <router-link :to="{ path: '/url', query: {id: 123} }">url?id=123</router-link>		<-- :to
  <router-view></router-view>
</div>`
}
const modultA = {
  template: `<div> {{ $route.query }} </div>`		<-- 显示值
}

const router = new Router({
  routes: [
    {path: '/url', component: modultA}		<-- 匹配地址
  ]
})

结果：
{ "id": 123 }
```



3 . 密文传值。 `http://localhost:8080/#/url`

路径链接 `<router-link :to="{ name: '/url', params: {id: 123} } >"` ， `name` 为路由地址 `params`为传值；在子组件 `$route.params` 接收。

```js
const App = {
  template: `<div id="app">
  <router-link :to="{name: 'u', params: {id: 123} }">url</router-link>		<-- :to
  <router-view></router-view>
</div>`
}
const modultA = {
  template: `<div> {{ $route.params }} </div>`		<-- 显示值
}

const router = new Router({
  routes: [
    {path: '/url', name: 'u', component: modultA}		<-- 匹配地址
  ]
})

结果：
{ "id": 123 }
```



**路由重定向**  redirect



**路由别名**  alias



**路由钩子函数**  beforeEnter



**模块函数**  beforeRouteEnter







**引用模块**    import    components



**模块传参**    props



**v-for渲染**

```vue
<li v-for="item in nav">
  <router-link :to=" '/link' + item.path ">    // 路径拼接
    {{item.title}}
  </router-link>
</li>
```



**当前高亮css **    router-link-active





## Vuex

package.json

```
"vuex": "latest"
```



```
npm install
```



引用 vuex 自写文件

```js
/* main.js */

import Vue from 'vue'
import App from './App'
import router from './router'
// 引入 vuex
import store from './vuex/index'	<-- 引用vuex(配置?)

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  store,		<-- 固定写法
  render: h => h(App)
})
```



vuex 自写文件

```js
/* vuex\index.js */

import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

// 定义数据
const state = {
  name: 77,
  age: 22
}

// 主要来操作 state 里的数据
const mutations = {
  addAge () {
    state.age++
  },
  minusAge () {
    state.age--
  }
}

// 用来调用 mutations 里的方法
// 可进行异步操作
const actions = {
  // 默认接收一个参数
  addAgePro (arg) {
    arg.commit('addAge')
    console.log(arg)
  }
}

// 相当于 computed 作用于 state 过滤操作
const getters = {
  filt (state) {
    return state.age.filter(i => {})
  }
}

/* eslint-disable no-new */
export default new Vuex.Store({
  // 用来保存数据
  state,
  mutations,
  actions,
  getters
})
```



在 App 模板里使用 vuex 数据

```vue
<template>
  <div id="app">
    <p>vuex数据：{{ $store.state }}</p>
    <p>mapState - name：{{ name }}</p>
    <p>mapState - age：{{ age }}</p>
    <button @click="a()">点击</button>
    <button @click="addAge()">age ++</button>
    <button @click="minusAge()">age --</button>
    <button @click="addAgePro()">age ++ pro</button>
    <button @click="minusAge()">age -- pro</button>
    <router-view/>
  </div>
</template>

<script>
// mapState 数据
// mapMutations 操作数据的方法
import {mapState, mapMutations, mapActions, mapGetters} from 'vuex'
export default {
  name: 'App',
  computed: {
    ...mapState([
      'name', 'age'
    ])
  },
  methods: {
    a () {
      console.log('name: %s, age: %s', this.name, this.age)
    },
    ...mapMutations([
      'addAge', 'minusAge'
    ]),
    ...mapActions([
      'addAgePro'
    ]),
    ...mapGetters([
      'filt'
    ])
  }
}
</script>
```













