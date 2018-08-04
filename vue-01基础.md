<script src="https://cdn.bootcss.com/vue/2.5.13/vue.js"></script>

## 起步

- 引入js标签

  ```html
  <script src="https://cdn.bootcss.com/vue/2.5.13/vue.js"></script>
  ```

  ​


## 显示数据

直接在html显示数据

```html
<div id="app">
    {{ message }}
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue!'
        }
    });
</script>
```






## 指令

- v-html , v-text

  > 显示方式 v-html == innerHTML ，v-text == innerText
  >
  > ```html
  > <div id="app">
  >     <p v-html="html"></p>	<!--绑定innerHTML-->
  >     <p v-text="html"></p>	<!--绑定innerText-->
  > </div>
  > <script>
  >     var app = new Vue({
  >         el: '#app',
  >         data: {
  >             html: '<h4>这里是文本</h4>'
  >         }
  >     });
  > </script>
  > ```
  >
  > ​ 


- v-once

  > 只在页面上渲染一次
  >
  > ```html
  > <div id="app" v-once></div>
  > ```
  >
  > ​



- v-bind

  > **缩写**：`:`
  >
  >  ​



- v-on

  > **缩写**：`@`
  >
  >  ​

- v-bind:key

  > ​

  ​



## 数据双向绑定

元素属性与data数据的绑定

处理数据与显示

```html
<div id="app">
    <span v-bind:title="message">	<!-- 此标签的title属性 绑定了数据message -->
    	鼠标悬停几秒钟查看此处动态绑定的提示信息！
    </span>

    <a :href="link">点击跳转链接</a>	<!-- 此标签的href属性 绑定了数据link -->

    <p>link：{{ link }}</p>	<!-- 显示link内容 -->
    <input v-model="link" type="text">	<!-- 表单元素的value值 绑定了数据link，当修改value值时则同时修改数据link值 -->
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            message: '页面加载于 ' + new Date().toLocaleString(),
            link: 'https://www.baidu.com'
        }
    })
</script>
```



## 绑定表单元素

- 文本框

  > text的value 绑定 数据content值
  >
  >  ```html
  > <div id="app">
  >     <p>{{ content }}</p>
  >     <input v-model="content" type="text">
  > </div>
  > <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             content: '请输入内容'
  >         }
  >     })
  > </script>
  >  ```
  >
  > ​

- 单选框

  > radio元素的value绑定了数据content值，选中radio其一则其value赋值给content
  >
  > ```html
  > <div id="app">
  >     <input type="radio" name="box" value="1" v-model="content">
  >     <input type="radio" name="box" value="2" v-model="content">
  >     <input type="radio" name="box" value="3" v-model="content">
  >     {{ content }}
  > </div>
  > <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             content: ''
  >         }
  >     })
  > </script>
  > ```
  >
  > ​

- 多选框

  >  两种情况：单个/多个绑定
  >
  >  ```html
  >  <div id="app">
  >     <!-- 单个勾选框，逻辑值 true/false -->
  >     <input type="checkbox" v-model="flag">
  >     {{ flag }}
  >     <br>
  >     <!-- 多个勾选框，绑定到同一个数组 -->
  >     <input type="checkbox" name="box" value="1" v-model="content">
  >     <input type="checkbox" name="box" value="2" v-model="content">
  >     <input type="checkbox" name="box" value="3" v-model="content">
  >     {{ content }}
  >  </div>
  >  <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             flag: false,
  >             content: []     // 多个绑定时必须是数组
  >         }
  >     })
  >  </script>
  >  ```
  >
  >  ​

- 选择列表

  >  两种情况：单选/多选
  >
  >  ```html
  >  <div id="app">
  >     <!-- 单选列表 -->
  >     <select v-model="content">
  >         <option>A</option>
  >         <option>B</option>
  >         <option>C</option>
  >     </select>
  >     {{ content }}
  >     <br>
  >     <!-- 多选列表 (绑定到一个数组) -->
  >     <select v-model="content2" multiple>
  >         <option>A</option>
  >         <option>B</option>
  >         <option>C</option>
  >     </select>
  >     {{ content2 }}
  >  </div>
  >  <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             content: '',
  >             content2: []	// 多选列表必须是数组
  >         }
  >     })
  >  </script>
  >  ```
  >
  >  ​




## class示例

- class属性值

  > v-bind:class="greenClass"  （class属性绑定了数据里greenClass值）
  >
  > ```html
  > <style>
  >     .red{}
  >     .green{}
  > </style>
  > <div id="app" class="red" :class="greenClass"><!--若有class则追加-->
  >     app
  > </div>
  > <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             redClass: 'red',
  >             greenClass: 'green'
  >         }
  >     })
  > </script>
  > ```
  >
  >   结果：
  >
  > ```html
  > <div id="app" class="red green">    app    </div>
  > ```
  >
  >  

- 添加多个class

  >  v-bind:class="[classname1, classname2, ... ]"
  >
  >  ```html
  >  <div id="app" class="red" :class="[ greenClass, pinkClass ]">
  >     app
  >  </div>
  >  <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             redClass: 'red',
  >             greenClass: 'green',
  >             pinkClass: 'pink'
  >         }
  >     })
  >  </script>
  >  ```
  >
  >  结果：
  >
  >  ```html
  >  <div id="app" class="red green pink">   app   </div>
  >  ```
  >
  >  ​

- 控制class

  > v-bind:class="{ classname1: true, classname2: false }"
  >
  >  json格式时则判断逻辑值是否添加
  >
  > ```html
  > <div id="app" :class="{ red: redClass, green: greenClass, pink: pinkClass }">
  >     app
  > </div>
  > <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             redClass: false,	// 不添加
  >             greenClass: true,	// 添加
  >             pinkClass: false	// 不添加
  >         }
  >     })
  > </script>
  > ```
  >
  > 结果：
  >
  > ```html
  > <div id="app" class="green">    app    </div>
  > ```
  >
  >  

- 结合checkbox

  >  checkbox控制class添加删除
  >
  >  ```html
  >  <style>
  >     .red{color:red}
  >     .green{background:green}
  >     .pink{border:5px solid pink}
  >  </style>
  >  <div id="app" :class="{ red: redClass, green : greenClass , pink : pinkClass }">
  >     app
  >     <input type="checkbox" v-model="redClass">		<!--绑定data里redClass的值-->
  >     <input type="checkbox" v-model="greenClass">	<!--绑定data里greenClass的值-->
  >     <input type="checkbox" v-model="pinkClass">		<!--绑定data里pinkClass的值-->
  >  </div>
  >  <script>
  >     new Vue({
  >         el: '#app',
  >         data: {
  >             redClass: true,
  >             greenClass: false,
  >             pinkClass: false
  >         }
  >     })
  >  </script>
  >  ```
  >
  >  ​




## 条件渲染

#### v-if

> 条件渲染：根据表达式的值的真假条件渲染元素
>
> v-if = 'true' (逻辑值｜表达式｜data数据值)
>
> ```html
> <div id="app">
>     <div v-if="show">v-if 111</div>
>     <input type="checkbox" v-model="show">
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show: true
>         }
>     })
> </script>
> ```
>
> ​

#### v-else

> 搭配 v-if 使用，v-if为false时显示
>
> ```html
> <div id="app">
>     <div v-if="show">v-if</div>
>     <div v-else="">v-else</div>
>     <input type="checkbox" v-model="show">
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show: true
>         }
>     })
> </script>
> ```
>
>  

#### v-else-if

> 当前面 v-if或v-else-if 都为false，此v-else-if为true时 加载渲染
>
> ```html
> <div id="app">
>     <label>
>         <input type="checkbox" v-model="show">
>         v-if: {{ show }}
>     </label>
>     <label>
>         <input type="checkbox" v-model="show2">
>         v-else-if: {{ show2 }}
>     </label>
>     <div v-if="show">v-if</div>		<!-- true时加载，false继续向下判断 -->
>     <div v-else-if="show2">v-else-if</div>	<!-- true时加载，false继续向下判断 -->
>     <div v-else>v-else</div>	<!-- 前面if都为false时加载 -->
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show: true,
>             show2: false
>         }
>     })
> </script>
> ```
>
> ​

#### 表单复加载机制

> 当`v-if`,`v-else`都有表单元素时，切换时会把表单value加载到显示的表单value中
>
> ```html
> <div id="app">
>     <div v-if="show">
>         输入框1：
>         <input type="text" placeholder="文本框1">	<!-- value值共用 -->
>     </div>
>     <div v-else>
>         输入框2：
>         <input type="text" placeholder="文本框2">	<!-- value值共用 -->
>     </div>
>     <input type="checkbox" v-model="show">{{ show }}
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show: true
>         }
>     })
> </script>
> ```
>
> 解决办法：
>
> ```html
> <input type="text" placeholder="文本框1" :key='key1'> <!-- 给元素加标识 -->
> <input type="text" placeholder="文本框2" :key='key2'>
> ```
>
> ​



#### v-show

> 根据表达式之真假值，切换元素的 `display` 行内CSS 属性
>
> ```html
> <div id="app">
>     <input type="checkbox" v-model="show">  <!-- 绑定数据 -->
>     <div v-show="show">v-show</div>     <!-- 根据数据show控制v-show模块的display -->
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show: true  /* 数据逻辑值 */
>         }
>     })
> </script>
> ```
>
> ​



#### v-for

> 基于源数据多次渲染元素或模板块
>
> ```html
> <div id="app">
>     <ul>
>         <li v-for="(item,index) in news">  <!-- 多次渲染li元素 -->
>             内容对象：   {{ item }}
>             索引值：     {{ index }}
>             内容对象.title：  {{ item.title }}
>             内容对象.content：{{ item.content }}
>         </li>
>     </ul>
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             news: [
>                 {title:'a',content:'This a news No.1!'},
>                 {title:'b',content:'This a news No.2!'},
>                 {title:'c',content:'This a news No.3!'}
>             ]
>         },
>         methods: {
>
>         }
>     })
> </script>
> ```
>
> ​



## 绑定事件

#### v-on

> 简写：`@`
>
> ​
>
> 1、点击事件 执行函数
>
> ```html
> <div id="app">
>     <!-- v-on:click 简写 @click -->
>     <input type="button" value="点击事件" @click="fn()">
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         methods: {  // 保存函数
>             fn: function () {
>                 alert("Hello Vue!");
>                 console.log(this);
>             }
>         }
>     })
> </script>
> ```
>
> console.log
>
> ```
> Vue$3 {_uid: 0, _isVue: true, $options: {…}, _renderProxy: Proxy, _self: Vue$3, …}
> ```
>
>  
>
> ​
>
>  2、点击事件 => 执行函数 或  表达式
>
> ```html
> <div id="app">
>     <!-- 点击 执行函数 -->
>     <input type="button" value="切换显示状态" @click="showFn()">
>
>     <!-- 点击 给数据show赋值(表达式) -->
>     <input type="button" value="切换显示状态" @click="show = !show">
>     
>     <p v-show="show">显示内容</p>
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             show : true		// 控制显示或隐藏
>         },
>         methods: {  // 存函数
>             showFn: function () {
>                 this.show = !this.show
>             }
>         }
>     })
> </script>
> ```
>
> 

#### 事件

```
    <!-- 方法处理器 -->
    <button v-on:click="doThis"></button>

    <!-- 内联语句 -->
    <button v-on:click="doThat('hello', $event)"></button>

    <!-- 缩写 -->
    <button @click="doThis"></button>

    <!-- 停止冒泡 -->
    <button @click.stop="doThis"></button>

    <!-- 阻止默认行为 -->
    <button @click.prevent="doThis"></button>

    <!-- 阻止默认行为，没有表达式 -->
    <form @submit.prevent></form>

    <!--  串联修饰符 -->
    <button @click.stop.prevent="doThis"></button>

    <!-- 键修饰符，键别名 -->
    <input @keyup.enter="onEnter">

    <!-- 键修饰符，键代码 -->
    <input @keyup.13="onEnter">



    <!-- 阻止单击事件冒泡 -->
    <a v-on:click.stop="doThis"></a>

    <!-- 提交事件不再重载页面 -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- 修饰符可以串联  -->
    <a v-on:click.stop.prevent="doThat"></a>

    <!-- 只有修饰符 -->
    <form v-on:submit.prevent></form>

    <!-- 添加事件侦听器时使用事件捕获模式 -->
    <div v-on:click.capture="doThis">...</div>

    <!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
    <div v-on:click.self="doThat">...</div>

    <!--只触发一次-->
    vue2.1新增
    <a v-on:click.once="doThis"></a>

全部的按键别名：
    @keyup.enter=""
    .tab
    .delete (捕获 “删除” 和 “退格” 键)
    .esc
    .space
    .up
    .down
    .left
    .right

    2.1.0 新增
    .ctrl
    .alt
    .shift
    .meta
```













## 修饰符

#### v-model.lazy

#### v-model.trim

> v-model.lazy = '$data' ：失去焦点后触发
>
> v-model.trim = '$data' ：去首尾空格
>
> ```html
> <div id="app">
>     失去焦点触发
>     <input type="text" v-model.lazy="a">
>     {{ a }}
>     <br>
>     去首尾的空格
>     <input type="text" v-model.trim="b">
>     {{ b }}
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             a: '',
>             b: ''
>         }
>     })
> </script>
> ```
>
> ​



## filters

> 过滤函数组
>
> 包含 Vue 实例可用过滤器的哈希表
>
> 使用方法： {{ 数据 | 过滤器 }}
>
> ```html
> <div id="app">
>     <!-- {{ 数据 | 过滤器 }}  显示过滤器返回的值 -->
>     {{ inp | fn }} <br>			 <!-- 不带参数 -->
>     {{ inp | fn('单位') }} <br>	<!-- 带参数 -->
>     <input type="text" v-model="inp">
> </div>
> <script>
>     new Vue({
>         el: '#app',
>         data: {
>             inp: ''
>         },
>         methods: {  // 自定义函数组
>         },
>         filters: {  // 过滤器
>             fn: function (val, txt) {    // [value值]，[自定义参数]
>                 // console.log(arguments);
>                 // console.log(val);	// 原值
>                 return val + (txt?txt:'abc')    // 返回值
>             }
>         }
>     })
> </script>
> ```
>
> ​



## computed

>  保存在`computed`里的函数对数据 侦听 和 实时计算

#### computed 与 methods 的区别

>  ```html
>  <div id="app">
>     数量：<input type="text" v-model="inp1">
>     单价：<input type="text" v-model="inp2">
>     <p>computed： 总价：{{ fn }}</p>    <!-- 当数据变化时 执行 -->
>     <p>methods： 总价：{{ fn2() }}</p>  <!-- 当调用时 执行 -->
>  </div>
>  <script>
>     new Vue({
>         el: '#app',
>         data: {
>             inp1: 1,
>             inp2: 1
>         },
>         methods: {      // 存函数，调用的时候执行
>             fn2: function () {
>                 return this.formatMul(5, this.inp1, this.inp2)
>             },
>             /**
>              * 格式化乘法  针对浮点数相乘
>              * [小数值], [计算参数1], [计算参数2]
>              */
>             formatMul: function (dec, num1, num2) {
>                 // Math.pow(x,y)  方法可返回 x 的 y 次幂的值
>                 return Math.floor(num1*Math.pow(10,dec))*Math.floor(num2*Math.pow(10,dec))/Math.pow(10,dec*2)
>             }
>         },
>         computed: {     // 实时计算，当数据变化的时候执行
>             fn: function () {
>                 return this.formatMul(10, this.inp1, this.inp2)
>             }
>         }
>     })
>  </script>
>  ```
>
>  

#### getter, setter

```js
computed: {

    all: {
        get: function () {
            
        },
        set: function (val) {
            
        }
    }

}
```







## 组件



#### Vue.component	

> 注册或获取**全局组件**。注册还会自动使用给定的`id`设置组件的名称



- 组件的父子级关系

  > 组件的父子级的关系是由引用关系决定的，例子如下

  ​


- 全局组件

  ```html
  <!--
      * 组件的父子级的关系是由引用关系决定的
      * 如下：在 实例#app 中引用 module组件，则#app为父级 module为子级
  -->
  <div id="app">
      <module></module>  <!-- 引用全局组件module -->
  </div>
  <script>
      // Vue.component( [组件名], [组件内容] )  : 全局组件
      Vue.component('module',{
          // template  : 定义html内容
          template: '<h4>这里是组件module的html内容</h4>'
      });
      // 实例 Vue （必须）
      new Vue({
          el: '#app'
      })
  </script>
  ```

   结果：

  ```html
  <div id="app"><h4>这里是组件module的html内容</h4></div>
  ```

  ​



- 全局组件之间的引用

  ```html
  <div id="app">
      <module1></module1>  <!-- 引用全局组件module1 -->
  </div>
  <script>
      // 全局组件1
      Vue.component('module1',{
          // template  : 定义html内容
          // 引用全局组件module2成为相对父级
          template: '<div> <h3>这里是全局组件module1的html内容</h3> <module2></module2> </div>'
      });

      // 全局组件2
      Vue.component('module2',{
          // template  : 定义html内容
          template: '<h4>这里是全局组件module2的html内容</h4>'
      });
      
      // 实例 Vue （必须）
      new Vue({
          el: '#app'
      })
  </script>
  ```

  结果：

  ```html
  <div id="app">
      <div>
          <h3>这里是全局子组件module1的html内容</h3>
          <h4>这里是全局子组件module2的html内容</h4>
      </div>
  </div>
  ```

  ​

#### components

局部组件，仅在其作用域中可用的组件

```html
<div id="app">
    <module></module>  <!-- 引用module局部组件 -->
</div>
<script>
    // 实例 Vue （必须）
    new Vue({
        el: '#app',
        components: {   // 局部子组件
            module: {
                template: '<h4>局部组件</h4>'
                // style: '',
                // script: ''
            }
        }
    })
</script>
```

结果：

```html
<div id="app"><h4>局部组件</h4></div>
```

 

#### 组件之间数据的引用

1、组件的template引用数据和函数

```html
<div id="app">
    <module></module>
</div>
<script>
    Vue.component('module',{
        // 在html结构里引用数据和添加事件
        // template 只能获取自身组件的数据和函数
        template: '<button @click="a()"> {{ name }} </button>',
        data: // 组件的data 必须是一个函数
            function () {
                return {
                    name: '全局组件name'
                }
            },
        methods: {  // 组件的函数
            a: function () {
                console.log(this.name);		// 打印结果
            }
        }
    });

    new Vue({
        el: '#app',
        data: {
            name: '局部组件name'
        }
    })
</script>
```

结果：

```html
全局组件name
```



2、父组件 向 子组件 传递数据

> 如下：父组件的数据`name`在`<module2 v-bind:abc="name"></module2>`传递给子组件，子组件用`v-bind:abc`接收后保存在`props`中（`abc`为自定义数据名）。`props`中定义接收的自定义数据名，此数据名如 data数据名 使用方法相同。

```html
<div id="app2">     <!--父组件-->
    <input type="text" v-model="name">
    <!-- 父组件向子组件传递数据  :自定义名='传递的数据名' ，在props接收 -->
    <module2 v-bind:abc="name"></module2>     <!--子组件-->
    <!-- v-bind:abc  自定义接收数据名
         name        父级的数据名  -->
</div>
<script>
    Vue.component('module2',{
        template: '<div> {{ abc }} </div>',     // 使用props接收到数据绑定在abc的值
        props: // 接收父组件传递的数据
            ['abc'],    // Array或json格式
        data: // 子组件的data 必须是一个函数，并返回json
            function () {
                return {

                }
            },
        methods: {}
    });

    new Vue({
        el: '#app2',
        data: {
            name: '123'
        }
    })
</script>
```



3、子组件 向 父组件 传递数据

> 方法：自定义事件

```html
<div id="app3"> <!--父组件-->
    <!-- @自定义事件=函数 -->
    <module3 @change="aFn"></module3> <!--子组件-->
    {{ childData }}
</div>
<script>
    Vue.component('module3',{
        // html模板里 绑定数据name  绑定事件click=btn
        template: '<div> <input v-model="name"><button @click="btn">button</button> </div>',
        data: function () {
            return {
                name: 'Allen'
            }
        },
        methods: {
            btn: function () {
                // [事件名称], [传递的数据1], ...[传递的数据n]
                this.$emit('change',this.name)// 向父组件传递数据
            }
        }
    });

    new Vue({
        el: '#app3',
        data: {
            childData: null
        },
        methods: {
            aFn: function (data) {
                console.log(arguments);  // 接收
                this.childData = arguments[0]
            }
        }
    })
</script>
```





#### 插槽slot



```html
<div id="app">
    <module>
        <div>123</div>  <!-- 当此标签注释时，会替换Vue.component的对应位置<slot>内容 -->
        <div slot="header">html内容</div>  <!-- slot对应<slot>的name属性 -->
    </module>
</div>
<script>
    Vue.component('module',{
        template:
            `<div>
                <slot>div123的替换内容</slot>
                <slot name="header"><p>这里是组件slot</p></slot>
             </div>`
        /*  <slot></slot>
                当组件中没有内容的时候显示（替换内容）
                当命名的时候 显示的内容是 html里的内容 不是Vue.component的内容
                当命名的时候 必须用slot标签一一对应 否则没有对应 则不显示内容
         */
    });

    new Vue({
        el: '#app'
    })
</script>
```







## 过渡动画



#### 过渡类名

1. `v-enter`：定义进入过渡的开始状态。在元素被插入时生效，在下一个帧移除。
2. `v-enter-active`：定义过渡的状态。在元素整个过渡过程中作用，在元素被插入时生效，在 `transition/animation` 完成之后移除。这个类可以被用来定义过渡的过程时间，延迟和曲线函数。
3. `v-enter-to`: **2.1.8版及以上** 定义进入过渡的结束状态。在元素被插入一帧后生效 (于此同时 `v-enter` 被删除)，在 `transition/animation` 完成之后移除。
4. `v-leave`: 定义离开过渡的开始状态。在离开过渡被触发时生效，在下一个帧移除。
5. `v-leave-active`：定义过渡的状态。在元素整个过渡过程中作用，在离开过渡被触发后立即生效，在 `transition/animation` 完成之后移除。这个类可以被用来定义过渡的过程时间，延迟和曲线函数。
6. `v-leave-to`: **2.1.8版及以上** 定义离开过渡的结束状态。在离开过渡被触发一帧后生效 (于此同时 `v-leave` 被删除)，在 `transition/animation` 完成之后移除。




#### CSS 过渡 transform

```html
<style>
    /* 进入过渡的开始状态 */
    .fade-enter,
    .fade-leave-to{
        opacity: 0;
        transform: translateX(30px);
    }
    /* 过渡的状态。过渡的过程时间，延迟和曲线函数 */
    .fade-enter-active,
    .fade-leave-active{
        transition: 1s;
    }
</style>
<div id="app">
    <button @click="show = !show">按钮</button>
    <transition name="fade">        <!--动画标签-->
        <p v-if="show">p标签</p>
    </transition>
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            show: true
        }
    })
</script>
```



#### CSS 动画 animation

```html
<style>
    .bounce-enter-active{
        animation: bounce-in .5s;
    }
    .bounce-leave-active{
        animation: bounce-in .5s reverse;  /* reverse：反向动画 */
    }
    @keyframes bounce-in {
        0% { transform: scale(0); }
        50% { transform: scale(1.5); }
        100% { transform: scale(1); }
    }
</style>
<div id="app2">
    <button @click="show = !show">按钮</button>
    <transition name="bounce">
        <p v-if="show">p标签</p>
    </transition>
</div>
<script>
    new Vue({
        el: '#app2',
        data: {
            show: true
        }
    })
</script>
```



#### 自定义过渡的类名

可以通过以下特性来自定义过渡类名：

- `enter-class`
- `enter-active-class`
- `enter-to-class` (2.1.8+)
- `leave-class`
- `leave-active-class`
- `leave-to-class` (2.1.8+)

优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 [Animate.css](https://daneden.github.io/animate.css/) 结合使用十分有用。

示例：

```html
<link rel="stylesheet" href="../animate_3.5.2.css">
<div id="app3">
    <button @click="show = !show">按钮</button>
    <transition
        name="custom-classes-transition"
        enter-active-class="animated tada"
        leave-active-class="animated bounceOut"
        :duration="3000"
    >
        <p v-if="show">p标签</p>
    </transition>
</div>
<script>
    new Vue({
        el: '#app3',
        data: {
            show: true
        }
    })
</script>
```



## 自定义指令





```html
<div id="app">
    <div v-allen>div标签</div>    <!--局部自定义指令-->
    <div v-zlname="a">zlname1</div>     <!--全局自定义指令-->
    <div v-zlname2="a">zlname2</div>    <!--全局自定义指令-->
</div>
<script>
    // 注册全局自定义指令
    Vue.directive('zlname',{
        bind: function (el, data) {
            console.log(arguments,el,data);
        }
    });
    // 注册全局自定义指令(简化写法)
    Vue.directive('zlname2',function (el, data) {
        console.log(arguments,el,data);
    });

    new Vue({
        el: '#app',
        data: {
            a: '123'
        },
        directives: {   // 自定义指令库
            allen: {    // 自定义指令名  v-allen
                bind: function () {     // 绑定时触发，只触发一次

                },
                inserted: function (el, data) {     // 主方法
                    console.log(arguments);
                    // console.log(el);    // 绑定的元素
                    // console.log(data);  // 数据
                },
                update: function () {   // 绑定的数据改变时触发

                },
                componentUpdated: function () {   // 当组件完成更新时触发

                },
                unbind: function () {   // 当元素解除绑定时触发，只触发一次

                }
            }
        }
    });
</script>
```





## 渲染函数



#### render函数

```html
<div id="app"></div>
<script>
    // html组件
    let module = Vue.component('module',{
        template: '<div>这是是index</div>'
    });

    new Vue({
        el: '#app',
        data: {},

        // render函数，默认接收一个参数，通过执行这个参数()并return
        render: function (h) {
            // 返回 执行参数 h([组件])
            return h(module)
        }
    });
</script>
```





## Vue生命周期

<img src="https://cn.vuejs.org/images/lifecycle.png" width="600"/>



| vue 1.0+      | vue 2.0       | Description                         |
| ------------- | ------------- | ----------------------------------- |
| init          | beforeCreate  | 组件实例刚被创建，组件属性计算之前，如data属性等          |
| created       | created       | 组件实例创建完成，属性已绑定，但DOM还未生成，`$el`属性还不存在 |
| befroeCompile | beforeMount   | 模板编译/挂载之前                           |
| compiled      | mounted       | 模板编译/挂载之后                           |
| ready         | mounted       | 模板编译/挂载之后（不保证组件已在document中）         |
| -             | beforeUpdate  | 组件更新之前                              |
| -             | updated       | 组件更新之后                              |
| -             | activeated    | for`keep-alive`，组件被激活时调用            |
| -             | deactivated   | for`keep-alive`，组件被移除时调用            |
| attached      | -             |                                     |
| detached      | -             |                                     |
| beforeDestory | beforeDestory | 组件销毁前调用                             |
| destoryed     | destoryed     | 组件销毁后调用                             |



参考文档：[Vue2.0 探索之路——生命周期和钩子函数的一些理解](https://segmentfault.com/a/1190000008010666)









