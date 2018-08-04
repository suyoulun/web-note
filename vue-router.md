- [Vue-router 官方文档笔记](http://blog.csdn.net/heliumlau/article/details/61649491)





```js
import Vue from 'vue'
import Router from 'vue-router'

/** =============== 模版 =============== */
const App = {
  template: `<div>
        <h2>主页面</h2>
        <ul>路由
          <li><router-link to="/">index</router-link></li>
          <li><router-link to="/about">about</router-link></li>
          <li><router-link to="/about/us">about/us</router-link></li>
        </ul>
        <ul>地址冒号匹配传值
          <li><router-link to="/urlData/data">urlData/data</router-link></li>
          <li><router-link to="/urlData/abcd">urlData/abcd</router-link></li>
        </ul>
        <ul>类get/post传值
          <li><router-link :to="{ path:'/Url', query:{ id: 123, data: name } }">明文传值query</router-link></li>
          <li><router-link :to="{ name:'u', params:{ id: 123 } }">密文传值params</router-link></li>
        </ul>
        <ul>跳转网址
          <button @click="$router.go(-1)">后退</button>
          <button @click="$router.go(1)">前进</button>
          <li><router-link to="/re">地址重定向 re==>about</router-link></li>
          <li><router-link :to="{path: '/re', query:{id: 111} }">地址重定向 明文传值</router-link></li>
          <li><router-link :to="{name: 're', params:{id: 222} }">地址重定向 密文传值</router-link></li>
        </ul>
        <router-view></router-view><!-- 模块视图 -->
    </div>`,
  data: function () {
    return {
      name: 'abc'
    }
  }
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

const urlData = {
  template: '<div>匹配传值 {{ $route.params }}</div>'
}
const Url = Vue.component('Url', {
  template: '<div> 明文值：{{ $route.query }}，密文值：{{ $route.params }}</div>'
})
const c = Vue.component('c', {
  template: '<div>cPage</div>',
  // 模板加载之前触发
  beforeRouteEnter (to, form, next) {
    console.log(arguments)
    next() // 执行加载
  }
})

/** =============== 路由 =============== */
const router = new Router({
  // mode: 'hash',
  mode: 'history',
  
  routes: [
    {path: '/', component: index},
    {
      path: '/about',
      component: about,
      // 子路由
      children: [
        {path: 'us', component: us}
      ]
    },
    // 匹配传值
    {path: '/urlData/:data', component: urlData},
    // 明文密文传值
    {path: '/Url', name: 'u', component: Url},
    // 路由重定向 redirect
    // {path: '/re', redirect: '/about'},
    // {path: '/re', redirect: {name: 'u'} }
    {
      path: '/re',
      name: 're',
      redirect: function (to) {
        console.log(arguments)
        console.log(to.hash) // 哈希值
        console.log(to.query) // 明文传值
        console.log(to.params) // 密文传值
        return {name: 'u'}
      }
    },
    // 路由别名 alias
    // /a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，
    // 但是路由匹配则为 /a，就像用户访问 /a 一样
    {path: '/a', alias: '/b', component: about},
    // 路由钩子函数 beforeEnter 在访问之后与加载之前触发
    {
      path: '/c',
      component: c,
      beforeEnter (to, form, next) {
        console.log(arguments)
        console.log(to) // 跳转来源
        console.log(form) // 跳转目标
        console.log(next) // 跳转函数
        next() // 执行加载，否则不加载
      }
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

