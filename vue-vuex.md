## 基本环境



**目录树**

```
|---  src/
    |---  components/
        |---  HeroesListState.vue
        |---  HeroesListGetters.vue
        |---  HeroesListMutations.vue
        |---  HeroesListActions.vue
    |---  store/
        |---  index.js
    |---  App.vue
    |---  main.js
```



**使用Vuex**

在main.js 引用 vuex 模块，创建一个新的状态管理并注入到 vue 实例当中

```js
/* ===== src/store/index.js ===== */

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)    // 在一个模块化的打包系统中，必须显式地通过 Vue.use() 来安装 Vuex

export const store = new Vuex.Store({
    state: {    // 唯一数据源
        heroes: [
            {name: '刘备', age: '80'},
            {name: '张飞', age: '60'},
            {name: '关羽', age: '70'},
            {name: '赵云', age: '50'},
        ]
    }
})


/* ===== src/main.js ===== */

import Vue from 'vue'
import App from './App'
import {store} from './store/index.js'    // 引入vuex配置

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  store,        // 注入vue实例中
  render: h => h(App)
})
```





## 核心概念



### 状态管理文件

```js
/* ===== src/store/index.js ===== */

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export const store = new Vuex.Store({
    // 唯一数据源
    state: {
        heroes: [
            {name: '刘备', age: '80'},
            {name: '张飞', age: '60'},
            {name: '关羽', age: '70'},
            {name: '赵云', age: '50'},
        ]
    },

    // 获取数据
    getters: {
        getHeroes (state) {
            return state.heroes.map( val => {
                return {
                    name: `<${val.name}>`,
                    age: val.age
                }
            })
        }
    },

    // 事件触发 操作数据
    mutations: {
        countAge: (state, payload) => {
            state.heroes.forEach(function (val) {
                val.age -= -payload.amount
            })
        }
    },

    // 提交的是 mutation，而不是直接变更状态
    // 可异步操作数据
    actions: {
        asyncCountAge: (context, payload) => {
            setTimeout( ()=>{
                context.commit('countAge', payload)
            },1000)
        }
    }
})
```







### 获取状态数据



#### state

==$store.state==

```vue
<template>
    <div>
        <h4>heroesList-state</h4>
        <ul>
            <li v-for="hero in heroes">
                <p>{{ hero.name }}</p>
                <span>{{ hero.age }}</span>
            </li>
        </ul>
        {{ name }}
        {{ age }}
    </div>
</template>

<script type="text/javascript">
    import { mapState } from 'vuex'
    export default {
        computed: {
            heroes () {
                return this.$store.state.heroes
            },

            // 辅助函数
            ...mapState({
                name: state => state.heroes,
                age: 'heroes'    // 等同于  age: state.heroes
            })
        }
    }
</script>
```





#### getters

==$store.getters==

```vue
<template>
    <div>
        <h4>heroesList-getters</h4>
        <ul>
            <li v-for="hero in heroes">
                <p>{{ hero.name }}</p>
                <span>{{ hero.age }}</span>
            </li>
        </ul>
        <span v-for="hero in mapheroes">{{ hero.name }}</span>
    </div>
</template>

<script type="text/javascript">
    import { mapGetters } from 'vuex'
    export default {
        computed: {
            heroes () {
                return this.$store.getters.getHeroes
            },

            // 辅助函数
            ...mapGetters({
                mapheroes: 'getHeroes'
            })
        }
    }
</script>
```





### 事件处理数据



#### mutations

```vue
<template>
    <div>
        <h4>mutations</h4>
        <button @click="countAge({amount: 1})">加一岁</button>
        <button @click="mapCountAge({amount: 1})">map 加一岁</button>
    </div>
</template>

<script>
    import {mapMutations} from 'vuex'
    export default {
        methods: {
            countAge (payload) {
                // this.$store.commit('countAge', payload)

                this.$store.commit({
                    type: 'countAge',
                    ...payload
                })
            },

            // 辅助函数
            ...mapMutations({
                mapCountAge: 'countAge'
            })
        }
    }
</script>
```





#### actions

```vue
<template>
    <div>
        <h4>actions</h4>
        <button @click="asyncCountAge({amount: -1})">减一岁</button>
        <button @click="mapAsyncContAge({amount: -1})">map 减一岁</button>
    </div>
</template>

<script>
    import {mapActions} from 'vuex'
    export default {
        methods: {
            asyncCountAge (payload) {
                this.$store.dispatch({
                    type: 'asyncCountAge',
                    ...payload
                })
            },

            // 辅助函数
            ...mapActions({
                mapAsyncContAge: 'asyncCountAge'
            })
        }
    }
</script>
```







### 模块 mudule







### 辅助函数

```vue
import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'

export default {
  computed: {
		...mapState(),
		...mapGetters()
  },
  methods: {
		...mapMutations(),
    ...mapActions()
  }
}
```

