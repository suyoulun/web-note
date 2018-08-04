---

---

## 拖拽事件

在html页面中，默认可拖拽的元素有`<img>`、 `<a>` 、选中的文字进行操作，而H5新增API`drag`事件可以让其它元素也实行拖拽功能



#### 拖拽元素

我们先来看看给拖拽H5新增的事件有哪些：

| 拖拽元素事件      |                 |
| ----------- | --------------- |
| ondragstart | 拖拽的一瞬间触发        |
| ondrag      | 拖拽前、拖拽结束之间，连续触发 |
| ondragend   | 拖拽结束后触发         |



当我们需要在页面上指定一个元素可以拖拽的时候，则给拖拽的元素添加属性`draggable='true'`

```html
  <div id="div1" draggable="true">拖拽元素</div>
  <div id="div2">目标元素</div>
```



给`#div1` **拖拽元素** 添加拖拽事件

```js
  // 拖拽元素事件
  // ondragstart      拖拽开始瞬间触发一次
  // ondrag           拖拽开始至结束的过程中，连续触发
  // ondragend        拖拽结束时触发一次
  div1.ondragstart = function () {
    console.log('div1.ondragstart')
  }
  div1.ondrag = function () {
    console.log('div1.ondrag')
  }
  div1.ondragend = function () {
    console.log('div1.ondragend')
  }
```



#### 目标元素

给目标元素新增的H5-API

| 目标元素事件      |                                          |
| ----------- | ---------------------------------------- |
| ondragenter | 拖拽元素进入时触发一次                              |
| ondragover  | 拖拽元素停留时连续触发                              |
| ondragleave | 拖拽元素离开时触发一次                              |
| ondrop      | 拖拽元素在目标元素释放时触发一次<br />**注意：只有在`ondragover` 事件里阻止默认行为才能生效** |



给`#div2 `**目标元素** 添加监听拖拽事件

```js
  // 目标元素事件
  // ondragenter      拖拽元素进入时触发一次
  // ondragover       拖拽元素停留时连续触发
  // ondragleave      拖拽元素离开时触发一次
  // ondrop           拖拽元素在目标元素释放时触发一次
  div2.ondragenter = function () {
    console.log('div2.ondragenter')
  }
  div2.ondragover = function (e) {
    console.log('div2.ondragover')
    e.preventDefault()
  }
  div2.ondragleave = function () {
    console.log('div2.ondragleave')
  }
  div2.ondrop = function () {
    console.log('div2.ondrop')
  }
```





#### 火狐兼容

在火狐默认情况下，以上面的代码无法拖拽元素，此时我们需要给拖拽元素的`ondragstart`事件里给`event.dataTransfer`对象设置`setData(key,value)`才能使用拖拽。

```js
// 拖拽元素开始时设置
  div1.ondragstart = function (e) {
    e = e || event;
    // setData 设置数据 key(自定义名)和value(值) (key和value必须是字符串)
    e.dataTransfer.setData('key','1')
  }
```



既然设置了值，当然也可以获取。

```js
// 目标元素event对象上获取设置的数据
  div2.ondrop = function (e) {
    e = e || event;
    // getData 获取【拖拽元素】的数据，根据key，获取对应的value
    console.log( e.dataTransfer.getData('key') )
  }
```



我们再来看看完整的事件过程：把`#div1`拖拽到`#div2`结构里面

```html
<div id="div1" draggable="true">拖拽元素</div>
<div id="div2">目标元素</div>
<script>
    // 拖拽元素事件
    div1.ondragstart = function (e) {
        e = e || event;
        // setData 设置数据 key(自定义名)和value(值) (key和value必须是字符串)
        e.dataTransfer.setData('key','1')
    }
    div1.ondrag = function () {
        this.style.cssText = 'background: #99e'
    }
    div1.ondragend = function () {
        this.style.cssText = ''
    }

    // 目标元素事件
    div2.ondragenter = function () {
        this.innerHTML = '请拖动到此处'
    }
    div2.ondragover = function (e) {
        e = e || event;
        this.innerHTML = '释放鼠标添加到此处'
        e.preventDefault()
    }
    div2.ondragleave = function () {
        this.innerHTML = '请拖动到此处'
    }
    div2.ondrop = function (e) {
        e = e || event;
        this.appendChild(div1)
        // getData 获取【拖拽元素】的数据，根据key，获取对应的value
        console.log( e.dataTransfer.getData('key') )
    }
</script>


/*======================== 结果 ========================*/
<div id="div2">
    释放鼠标添加到此处
    <div id="div1" draggable="true" style="">拖拽元素</div>
</div>
```





#### 拖动时显示的图片

设置在拖动过程中显示的图片，大多数时候，我们不需要这个属性。默认的时候将使用被拖动的元素自身作为拖动状态的图片。拖动时展示的元素需要是可见元素。

`setDragImage(ele, x, y)` 方法有3个参数：`ele` 显示为拖动背景的元素；`x` `y` 为百分比偏移量

```html
<div id="div1" draggable="true">拖拽元素</div>
<img id="img" src="123.jpg" width=100>
<script>
    // 拖拽元素事件
    div1.ondragstart = function (e) {
        e = e || event;
        e.dataTransfer.setData('key','1')
        // setDragImage 设置在拖动过程中显示的图片
        e.dataTransfer.setDragImage(img,50,50)
    }
</script>
```





#### 读取文件信息

当我们把window外面的文件拖拽到元素里，我们也可以通过`event.dataTransfer.files`获取文件信息，最终返回一个对象。

```html
<div id="div2">目标元素</div>
<script>
    div2.ondragenter = function () {
        this.innerHTML = '释放鼠标'
    }
    div2.ondragleave = function () {
        this.innerHTML = '移动鼠标到此处'
    }
    div2.ondragover = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来触发ondrop事件
        e.stopPropagation();    // 阻止事件冒泡
    }
    div2.ondrop = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来获取文件信息
        e.stopPropagation();    // 阻止事件冒泡

        var files = e.dataTransfer.files
        console.log( files )	// 打印结果
    }
</script>

/*======================== 结果 ========================*/
FileList {0: File(43536), length: 1}
```

当拖入多个文件时`event.dataTransfer.files`返回的对象里保存文件信息格式如下：

```json
FileList {
  0 : File(43536) {name: "1.png", …}
  1 : File(36452) {name: "2.png", …}
  length : 1
  __proto__ : FileList
}
```

由以上信息可以分析：对象包含的文件信息是以序号来排列的，同时有个`length`属性。以下主要获取文件信息的属性有【文件名】【文件大小】【文件MIME类型】【最后修改时间】：

| 属性                                       | 值                                        | 描述                                       |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| event.dataTransfer.files.`length`        | 2                                        | 文件数量                                     |
| event.dataTransfer.files[0].`name`       | 1.png                                    | 文件名                                      |
| event.dataTransfer.files[0].`type`       | "image/png"                              | 文件MIME类型                                 |
| event.dataTransfer.files[0].`size`       | 43536                                    | 文件大小（字节）                                 |
| event.dataTransfer.files[0].`lastModified` | 1517106434732                            | 文件的最后修改时间（毫秒）                            |
| event.dataTransfer.files[0].`lastModifiedDate` | Sun Jan 28 2018 10:27:14 GMT+0800 (中国标准时间) | 文件的最后修改时间                                |
| event.dataTransfer.files[0].`webkitRelativePath` | ""                                       | 该特性是非标准的，请尽量不要在生产环境中使用它！<br /> 只读属性，包含 [`USVString`](https://developer.mozilla.org/zh-CN/docs/Web/API/USVString)，它规定了文件的路径，相对于用户在 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 元素中选择的目录，这个元素设置了 `webkitdirectory` 属性。 |

注：`event.dataTransfer.files[0].lastModifiedDate`有几个转换时间格式的方法

```
event.dataTransfer.files[0].lastModifiedDate.toLocaleDateString()	==>	  2018/1/28
event.dataTransfer.files[0].lastModifiedDate.toLocaleTimeString()	==>	  上午10:27:14
event.dataTransfer.files[0].lastModifiedDate.toLocaleString()	==>    2018/1/28 上午10:27:14
```



做个小实例，把(多个)文件拖入看看

```html
<div id="div2" style="width:800px; height:400px; margin:auto; border: 1px solid red;">目标元素</div>
<script>
    div2.ondragenter = function () {
        this.innerHTML = '释放鼠标'
    }
    div2.ondragleave = function () {
        this.innerHTML = '移动鼠标到此处'
    }
    div2.ondragover = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来触发ondrop事件
        e.stopPropagation();    // 阻止事件冒泡
    }
    div2.ondrop = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来获取文件信息
        e.stopPropagation();    // 阻止事件冒泡

        var files = e.dataTransfer.files
        this.innerHTML = '';
        this.innerHTML += 'files.length：' + files.length;

        [].forEach.call(files,function (val,index,arr) {
            this.innerHTML += '<br>' + files[index].name
            this.innerHTML += '<br>' + files[index].size
            this.innerHTML += '<br>' + files[index].type
            this.innerHTML += '<br>' + files[index].lastModified
            this.innerHTML += '<br>' + files[index].lastModifiedDate
            this.innerHTML += '<br>' + files[index].lastModifiedDate.toLocaleDateString()
            this.innerHTML += '<br>' + files[index].lastModifiedDate.toLocaleTimeString()
            this.innerHTML += '<br>-----<br>'
        },div2)
    }
</script>


/*======================== 结果 ========================*/
files.length：2
1.png
39706
image/png
1517037653365
Sat Jan 27 2018 15:20:53 GMT+0800 (中国标准时间)
2018/1/27
下午3:20:53
-----

2.png
43536
image/png
1517106434732
Sun Jan 28 2018 10:27:14 GMT+0800 (中国标准时间)
2018/1/28
上午10:27:14
-----
```





#### 读取文件内容

`FileReader` ：对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容

| 方法/属性/事件                     | description                              |
| ---------------------------- | ---------------------------------------- |
| `FileReader.readAsDataURL()` | 开始读取指定的[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容。一旦完成，`result`属性中将包含一个`data:` URL格式的字符串以表示所读取文件的内容。 |
| `FileReader.readAsText()`    | 开始读取指定的[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容。一旦完成，`result`属性中将包含一个字符串以表示所读取的文件内容。 |
| `FileReader.result`          | 文件的内容。该属性仅在读取操作完成后才有效，数据的格式取决于使用哪个方法来启动读取操作。 |
| `FileReader.onload`          | 处理`load`事件。该事件在读取操作完成时触发                 |

当我们读取了文件信息，此时还不能把文件引入到Web中，而是要通过`new FileReader()`对象来读取文件内容。使用方法：

```js
div.ondrop = function (e) {
  ...
  // 文件信息
  var file = e.dataTransfer.files[0]
  // 创建读取文件内容对象
  var reader = new FileReader();
  // 读取文件内容
  reader.readAsDataURL( file );
  // 读取完成 do Something
  reader.onload = function (){
     console.log( this.result )		// 文件内容
  }
}
```



完整的案例

```html
<div id="div2" style="width:800px; height:400px; margin:auto; border: 1px solid red;">目标元素</div>
<script>
    div2.ondragenter = function () {
        this.innerHTML = '释放鼠标'
    }
    div2.ondragleave = function () {
        this.innerHTML = '移动鼠标到此处'
    }
    div2.ondragover = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来触发 ondrop 事件
        e.stopPropagation();    // 阻止事件冒泡
    }
    div2.ondrop = function (e) {
        e = e || event;
        e.preventDefault();     // 阻止默认行为，来获取文件信息
        e.stopPropagation();    // 阻止事件冒泡

        var files = e.dataTransfer.files
        this.innerHTML = '';

        [].forEach.call(files, function (val, index, arr) {
            var reader = new FileReader();          // 创建文件内容读取对象
            reader.readAsDataURL( files[index] );   // 分析文件内容
            reader.onload = function () {
                console.log( this.result )          // 打印文件内容
                if ( /image/.test(this.result) ) {  // 文件类型若是 image 则添加 img 标签
                    var img = new Image();
                    img.src = this.result
                    div2.appendChild(img)
                }
            }
        },div2)
    }
</script>
```





## H5-新增方法



#### 获取元素

querySelector：获取第一个匹配到的元素

```js
/** 
 *  参数与css选择器使用方法相同，如：
 *  #div
 *  .div
 *  div:nth-child(1)
 *  div[class=wrap]
 */
document.querySelector('div')	// 第一个匹配到的 div
document.querySelector('div p')		// 第一个匹配到的 div 下的 p
```

querySelectorAll：获取所有匹配到的元素

```js
/** 
 *  参数与css选择器使用方法相同，如：
 *  #div
 *  .div
 *  div:nth-child(1)
 *  div[class=wrap]
 */
document.querySelectorAll('div')	// 所有匹配到的 div
document.querySelectorAll('div p')		// 所有匹配到的 div 下的 p
```

注意：`querySelector` 和 `querySelectorAll` 是静态方法，当要获取动态创建的元素时，需要重新获取



#### classList

add

```js
document.getElementById('div').classList.add('on')	// 添加类名
```

remove

```js
document.getElementById('div').classList.remove('on')	// 删除类名
```

toggle

```js
document.getElementById('div').classList.toggle('on')	// 切换类名
```

contains

```js
document.getElementById('div').classList.contains('on')	// 判断类名存在，返回 boolean
```

length

```js
document.getElementById('div').classList.length		// 返回类名数量
```



#### dataset

自定义属性：注意自定义标签属性`data-`后面的名称有`-`连接时，在JS中要换成驼峰写法

```html
<div id="box" data-class='on' data-my-code='javascript'></div>  // 自定义标签属性 data-
<script>
  console.log( box.dataset['class'] )     // 获取自定义属性的值
  console.log( box.dataset['myCode'] )    // js中换成驼峰写法   // my-code ==> myCode
</script>
```
删除自定义属性

```js
有两种方法：
1
box.removeAttribute('data-class')
box.removeAttribute('data-my-code')
2
delete box.dataset['class']
delete box.dataset['myCode']
```



#### JSON

[JSON.parse() 和 JSON.stringify() – 高级用法](http://www.css88.com/archives/8735)



**JSON.parse**

```js
#// 把 string 转换成 json
var str = '{"name":"myName","age":18}'
console.log( JSON.parse(str) )

#// JSON.parse() 可以接受第二个参数，它可以在返回之前转换对象值。
const user = {
  name: 'John',
  email: 'john@awesome.com',
  plan: 'Pro'
};
 
const userStr = JSON.stringify(user);
 
const newUserStr = JSON.parse(userStr, (key, value) => {
  if (typeof value === 'string') {
    return value.toUpperCase();
  }
  return value;
});
 
console.log(newUserStr); //{name: "JOHN", email: "JOHN@AWESOME.COM", plan: "PRO"}

#注：由于安全格式，必须使用双引号包裹属性
#注：尾随逗号在JSON 中无效，所以如果传递给它的字符串有尾随逗号，JSON.parse()将会抛出错误。
```



**JSON.stringify**

```js
// 把 json 转换成 string
var str = {"name":"myName","age":18}
console.log( JSON.stringify(str) )

#// JSON.stringify() 可以带两个额外的参数，第一个是替换函数，第二个间隔字符串，用作隔开返回字符串。
// 1. 替换函数
const user = {
  id: 229,
  name: 'John',
  email: 'john@awesome.com'
};

const userStr = JSON.stringify(user, function (key, value) {
  console.log(typeof value);
  if (key === 'email') {
    return undefined;  // 任何返回 undefined 的值将不在返回的字符串中
  }
  return value;
});
// "{"id":229,"name":"John"}"

// 2. 间隔字符串
const user = {
  name: 'John',
  email: 'john@awesome.com',
  plan: 'Pro'
};
 
const userStr = JSON.stringify(user, null, '...');
// "{
// ..."name": "John",
// ..."email": "john@awesome.com",
// ..."plan": "Pro"
// }"
```



**用 JSON.stringify 来格式化对象**

```js
var censor = function(key,value){
    if(typeof(value) == 'function'){
        return Function.prototype.toString.call(value)
    }
    return value;
}
var foo = {
    bar: "1", 
    baz: 3, 
    o: {
        name: 'xiaoli',
        age: 21,
        info: {
            sex: '男',
            getSex: function () { return 'sex'; }
        }
    }
};
console.log( JSON.stringify(foo,censor,4) )

/* log 如下 */
{
    "bar": "1",
    "baz": 3,
    "o": {
        "name": "xiaoli",
        "age": 21,
        "info": {
            "sex": "男",
            "getSex": "function (){return 'sex';}"
        }
    }
}
```



**toJSON方法**

```js
// 如果一个被序列化的对象拥有 toJSON 方法，那么该 toJSON 方法就会覆盖该对象默认的序列化行为：不是那个对象被序列化，而是调用 toJSON 方法后的返回值会被序列化
var obj = {
    foo: 'foo',
    toJSON:function(){	// 覆盖默认行为
        return 'bar';
    }
}
JSON.stringify(obj);//'"bar"'
JSON.stringify({x:obj});//'{"x":"bar"}'
```



**eval**

```js
// 尝试把 string 解析成 js 代码运行  **注意：这种做法会有风险**
eval('alert(1)')
```





#### URI编码

> 将字符串编码为统一资源标识符 (URI)

encodeURI：编码

```js
// URI 编码
console.log( encodeURI('localhost:80/Web前端.html') )	// ==> "localhost:80/Web%E5%89%8D%E7%AB%AF.html"
```

decodeURI：解码

````js
// URI 解码
console.log( decodeURI('localhost:80/Web%E5%89%8D%E7%AB%AF.html') )	// ==> "localhost:80/Web前端.html"
````





window.URL.createObjectURL( ev.dataTransfer.files[n] )



#### base64编码

btoa：编码

````js
// 将一个 base64 编码过的字符串转换成 ascii 字符串或二进制数据
var str = 'hello'
window.btoa( str )	// ==> "aGVsbG8="

// **注意**不能直接编译中文，若要使用中文请先用 encodeURI 编码
var str = '前端'
str = window.encodeURI( str )	// ==> "%E5%89%8D%E7%AB%AF"
str = window.btoa( str )		// ==> "JUU1JTg5JThEJUU3JUFCJUFG"
str = window.atob( str )		// ==> "%E5%89%8D%E7%AB%AF"
str = window.decodeURI( str )	// ==> "前端"
````

atob：解码

````js
// 对用 base64 编码过的字符串进行解码
var str = 'hello'
str = window.btoa( str )	// ==> "aGVsbG8="
str = window.atob( str )	// ==> "hello"
````





#### 历史管理

> HTML5引入了 [history.pushState()](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState) 和 [history.replaceState()](https://developer.mozilla.org/en-US/docs/Web/API/History_API#The_replaceState()_method) 方法，它们分别可以添加和修改历史记录条目。这些方法通常与[`window.onpopstate`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/onpopstate) 配合使用。



**window.history.pashState**

> 当用户执行某一操作时添加一条历史记录，此时浏览器可进行后退操作。
>
> `pushState()` 需要三个参数: 一个状态对象, 一个标题 (目前被忽略), 和 (可选的) 一个URL. 

```html
<button>option1</button>
<button>option2</button>
<div id="cont"></div>
<script>
    var data = {
            'option1': 'This\'s Content No.1',
            'option2': 'This\'s Content No.2'
        },
        btns = document.querySelectorAll('button');

    for (var i = 0; i < btns.length; i++) {
        btns[i].onclick = function () {
            cont.innerHTML = data[ this.innerHTML ]
            // 添加历史条目，同时显现在地址栏中
            window.history.pushState(this.innerHTML,'','?con='+this.innerHTML)
        }
    }

    // 当触发跳转历史条目时
    window.onpopstate = function (e) {
        // 获取状态对象
        console.log( e.state )
        // 利用状态对象值而对页面进行数据变化
        cont.innerHTML = data[ e.state ]
    }
</script>
```



**window.onpopstate**

> 在浏览器某些行为下触发, 比如点击后退、前进按钮(或者在JavaScript中调用`history.back()`、`history.forward()`、`history.go()`方法)
>
> 事件对象`event.state`可获取`window.history.pashState`设置的 **状态对象** 

```js
window.onpopstate = function (e) {
	consoloe.log( e.state )
  	// do something ...
}
```



**window.onhashchange**

> 当一个窗口的哈希改变时就会触发 hashchange 事件

```js
window.onhashchange = function () {
    console.log( window.location.hash );
}
```





## AJAX

`get`比`post`性能好，但`get`可传输的数据量相比较小，`post`传输数据没有大小限制



#### 下载文件



**通过js下载本地文件**

```js
btn.onclick = function () {
    var aTag = document.createElement('a');
    aTag.href = 'images/1.jpg'      // 文件路径
    aTag.download = 'new1.jpg'      // 更改下载的文件名
    aTag.click()                    // js点击下载
}
```





#### jsonp







#### 请求音频并播放



`audio` **标签**

> 一般用audio标签播放音乐。但在很多地方不是通过标签形式播放音乐，而是使用js

```html
<audio src="audio/1.mp3" controls>
```



**利用标签播放音频**

```js
var xhr = new XMLHttpRequest();

xhr.responseType = 'arraybuffer'
xhr.onload = function () {
    if ( xhr.readyState == 4 && xhr.status == 200) {
        var buffer = xhr.response   // 原始数据
            ,blob = new Blob([buffer], {type:'audio/mpeg'})
            ,url = window.URL.createObjectURL(blob)
            ,audio = document.createElement('audio')

        audio.src = url         // 音频地址
        audio.controls = 'controls'     // 控制面板
        audio.volume = 0.1      // 音量
        audio.play()            // 播放
        document.body.appendChild(audio)
    }
}
xhr.open('post', '/audio/1.mp3', true)
xhr.send()
```



**利用音频节点播放音频**

```js
var xhr = new XMLHttpRequest();

xhr.responseType = 'arraybuffer'
xhr.onload = function () {
    if ( xhr.readyState == 4 && xhr.status == 200) {
        var aCxt = new AuidoContext()   // 创建音频对象

        // 解码
        aCxt.decodeAudioData(xhr.response, function (buffer) {
            var sourceNode = aCxt.createBufferSource();
            sourceNode.buffer = buffer
            sourceNode.connect(aCxt.destination)    // 连接扬声器 耳机
            sourceNode.start(0)     // 播放 0秒开始

        }, function () {    // 播放失败回调

        })
    }
}
xhr.open('post', '/audio/1.mp3', true)
xhr.send()
```





#### 上传文件



先创建一个服务器文件以接收处理数据

```php
<?php
    move_uploaded_file($_FILES['file']['tmp_name'],'uploads/'.$_FILES['file']['name']);
?>
```

通过 `input type=file` 配合 `formData` 对象实现文件上传；

```html
<!-- multiple 多选文件 -->
<input type="file" name="file" id="files" multiple="multiple">

<button id="submit">上传</button>

<hr id="hr" style="width:300px;margin-left:0">

<script>
    var fileInp = document.getElementById('files')

    submit.onclick = function () {      // 点击上传

        #// 构建数据提交对象
        var fd = new FormData();

        // 随机数更名
        var newName = ''+ Math.floor((Math.random()*1e16)).toString(16) // 随机16进制数
                + fileInp.files[0]['name'].match(/\.[^.]+/g).sort(function (a,b){return 1})[0];  // 后缀名

        #// 添加文件数据   [键值] [blob对象] [更换文件名]
        fd.append('file', fileInp.files[0], newName )

        // 创建ajax
        var xhr = new XMLHttpRequest();

        #// 进度条 #注#要在 send 前注册
        xhr.upload.onprogress = function (e) {
            console.log( '当前进度：' + e.loaded +'\t总进度：'+ e.total )
            hr.style.width = e.loaded/e.total * 300 + 'px'
        }

        // 提交数据
        xhr.open('post', './serve.php', true)
        xhr.send( fd )      // 上传的文件数据

        // 服务器返回消息
        xhr.onload = function () {
            if (xhr.readyState == 4 && /(^2\n\n)|304/.test(xhr.status)) {
                alert('success')
            }
        }

    }
</script>
```

拖拽的图片上传

```html
<div id="box" style="height:300px;background:#eee;">将图片拖到此区域</div>

<input id="btn" type="button" value="上传图片">

<script>
// 存放文件
var arrFile = [];

// 拖拽图片
box.ondragover = function (e) {
    e.preventDefault();
    e.stopPropagation();
}
box.ondrop = function (e) {
    e.preventDefault();
    e.stopPropagation();

    // 多个文件
    var file = e.dataTransfer.files;
    [].forEach.call(file, function (val, index) {
        if ( ! /image/.test(val.type) ) return;
        var img = new Image();
        var url = window.URL.createObjectURL( val )
        img.src = url;
        img.height = 100
        box.appendChild( img )

        // 添加文件信息到数组
        arrFile.push( val )
    })
}

// 点击上传
btn.onclick = upFile;

function upFile() {
    // 文件数组换成对象
    var oFile = {};
    arrFile.forEach(function (val, index) {
        oFile[index] = val;

        // 构建数据提交对象
        var fd = new FormData();
        fd.append('file', oFile[index] )

        // 创建ajax
        var xhr = new XMLHttpRequest();
        xhr.open('post', './serve.php', true)
        xhr.send( fd )
        xhr.onload = function () {
            if (xhr.readState == 4 && /(^2\n\n)|304/.test(xhr.status)) {
                console.log(xhr.responseText)
                delete oFile[index]     // 加载完成删除相应的存值
            }
        }

        //设置超时时间    
        xhr.timeout = 100000;
        xhr.ontimeout = function(event){
            alert('请求超时！');
        }
    })

    arrFile = [];   // 清空添加文件数组，已转存到 oFile
}
</script>
```

上传进度条

```js
#// 进度条 #注#要在 send 前注册
xhr.upload.onprogress = function (e) {
  console.log( '当前进度：' + e.loaded +'\t总进度：'+ e.total )
  hr.style.width = e.loaded/e.total * 300 + 'px'
}
```





## 多线程

> 当需要运算大量的数据时，可以用多线程方式去处理，从而不会影响下文代码的长时间I/O阻塞



前端页面调用`new Worker`对象

```js
var w = new Worker('worker1.js');   // 运算数据的文件
w.postMessage(2e4);     // 传值到运算数据的文件
w.onmessage = function (e) {
  // e.data 接收返回的数据
  box2.innerHTML = e.data
}
```

处理数据的文件

```js
/* worker1.js */
self.onmessage = function (e) {
    // e.data接收前端的数据
    // 在此多线程里 各种算法 大量计算
    // 然后把运算的结果的发送到前端页面
    var str = '';
    for( var i=0;i<e.data;i++ ){
        str += String.fromCharCode(i);
    }
    self.postMessage(str);
}
```









## 本地存储

本地存储WebStorage (localstorage & sessionstorage)，所有数据保存为 String

localstorage ：永久存储

sessionstorage：临时存储（关闭页面时清除）

所有支持的浏览器目前都采用的每个域名大小5MB



> 最推荐使用的自然是`getItem()`和`setItem()`，清除键值对使用`removeItem()`。
>
> 如果希望一次性清除所有的键值对，可以使用`clear()`。
>
> 另外，HTML5还提供了一个`key()`方法，可以在不知道有哪些键值的时候使用



```js
    // 本地存储对象
    window.localStorage

    // 长度
    window.localStorage.length

    // 索引值
    window.localStorage.key(1)

    // 设置/添加 (键值对)
    window.localStorage.setItem('key','1')

    // 获取值
    window.localStorage.getItem('key')

    // 删除
    window.localStorage.removeItem('key')

    // 清除所有
    window.localStorage.clear()
```



**使用注意事项**

- 不同浏览器数据存储是相互独立的，chrome的localStorage在ff上访问不了

- 使用时要检测浏览器是否支持（不要使用window.localStorage检测对象是否存在，应该set一条数据然后进行异常捕获）

- 由于ls是永久存储，要做好更新策略，控制过期

  ```js
  function set(key,vel){
      var curTime = new Date().getTime();
      localStorage.setItem( key , JSON.stringify({data:vel , time:curTime }) );
  }
   
  function get(key,exp){
      var data = locaStorage.getItem(key);
      var dataObj = JSON.parse(data);
      if(new Date().getTime()-dataObj.time<exp){
          return dataObj.data;
      }else{
          alert('已过期！');
      }
  }　
  ```


- ss子域名之间是不能共享数据的-使用跨域方法传输数据









## 离线存储

> 原理就是
> 在有网络的时候，客户端第一次访问服务器，服务器收到请求后，会把所有的信息返回给客户，并且同时，也会发送到寄存器里面存储着，当突然没网络的时候，这时客户端请求不到服务器，就会去寄存器里面去找所需要的信息
>
> 可以缓存任何文件，比如图片、css、js、html 的名称



1. xampp服务器apache目录下的httpd.conf文件添加以下设置头信息

  ```
  /* httpd.conf */
  AddType text/cache-manifest .manifest
  ```

2. html文件设置

   ```html
   <html manifest="cache.manifest">
   ```

3. 配置文件`cache.manifest`

   > **离线存储的manifest一般由三个部分组成:**
   >
   > 1. CACHE : 表示需要离线存储的资源列表，由于包含manifest文件的页面将被自动离线存储，所以不需要把页面自身也列出来。
   > 2. NETWORK : 表示在它下面列出来的资源只有在在线的情况下才能访问，他们不会被离线存储，所以在离线情况下无法使用这些资源。不过，如果在CACHE和NETWORK中有一个相同的资源，那么这个资源还是会被离线存储，也就是说CACHE的优先级更高。
   > 3. FALLBACK : 表示如果访问第一个资源失败，那么就使用第二个资源来替换他，比如上面这个文件表示的就是如果访问根目录下任何一个资源失败了，那么就去访问offline.html。
   >
   > 
   >
   > **浏览器怎么解析manifest**
   >
   > 那么浏览器是怎么对离线的资源进行管理和加载的呢？这里需要分两种情况来讨论。
   >
   > - 在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
   > - 离线的情况下，浏览器就直接使用离线存储的资源。
   >
   > 这个过程中有几个问题需要注意。
   >
   > - 如果服务器对离线的资源进行了更新，那么必须更新manifest文件之后这些资源才能被浏览器重新下载，如果只是更新了资源而没有更新manifest文件的话，浏览器并不会重新下载资源，也就是说还是使用原来离线存储的资源。
   > - 对于manifest文件进行缓存的时候需要十分小心，因为可能出现一种情况就是你对manifest文件进行了更新，但是http的缓存规则告诉浏览器本地缓存的manifest文件还没过期，这个情况下浏览器还是使用原来的manifest文件，所以对于manifest文件最好不要设置缓存。
   > - 浏览器在下载manifest文件中的资源的时候，它会一次性下载所有资源，如果某个资源由于某种原因下载失败，那么这次的所有更新就算是失败的，浏览器还是会使用原来的资源。
   > - 在更新了资源之后，新的资源需要到下次再打开app才会生效，如果需要资源马上就能生效，那么可以使用`window.applicationCache.swapCache()`方法来使之生效，出现这种现象的原因是浏览器会先使用离线资源加载页面，然后再去检查manifest是否有更新，所以需要到下次打开页面才能生效。

   ```
   CACHE MANIFEST
   # version 1.0.2

   CACHE:
       img/1.jpg
       img/3.jpg

   FALLBACK:

   NETWORK:
       *
   ```



对于HTML5中离线存储对象`window.applicationCache`有几个事件需要我们关注下：

1. `oncached`:当离线资源存储完成之后触发这个事件，这个是文档的说法，我在Chrome上面测试的时候并没有触发这个事件。
2. `onchecking`:当浏览器对离线存储资源进行更新检查的时候会触发这个事件
3. `ondownloading`:当浏览器开始下载离线资源的时候会触发这个事件
4. `onprogress`:当浏览器在下载每一个资源的时候会触发这个事件，每下载一个资源就会触发一次。
5. `onupdateready`:当浏览器对离线资源更新完成之后会触发这个事件
6. `onnoupdate`:当浏览器检查更新之后发现没有资源更新的时候触发这个事件





## 多媒体

`video` `audio` 标签是用来播放音视频





#### video

video 标签目前只用来播放视频

```html
<video id="video" autoplay controls poster="1.jpg">
    <source src="1.mp4" type="video/mp4" />
    <source src="1.ogg" type="video/ogg" />
    <source src="1.webm" type="video/webm" />
</video>
```

| Video标签属性      |                           |
| -------------- | ------------------------- |
| autoplay       | 视频就绪自动播放                  |
| controls       | 向用户显示播放控件                 |
| width / height | 设置浏览器宽度 / 高度              |
| loop           | 播放完是否继续播放该视频，循环播放         |
| preload        | 是否等加载完再播放                 |
| src            | 视频url地址                   |
| poster         | 加载等待的画面图片                 |
| autobuffer     | 设置为浏览器缓冲方式，不设置autoplay才有效 |



**Video方法**

``` s
video.play()
video.pause()
video.load()
```

| Video AIP方法                 |                                          |
| --------------------------- | ---------------------------------------- |
| play()                      | 播放                                       |
| pause()                     | 暂停                                       |
| load()                      | 重新加载资源                                   |
| element.requestFullscreen() | 全屏<br />webkit兼容    element.webkitRequestFullScreen();<br />Firefox兼容    element.mozRequestFullScreen() |
| document.exitFullscreen()   | 退出全屏<br />webkit兼容    document.webkitCancelFullScreen()<br />Firefox兼容   document.mozCancelFullScreen() |



**Video事件**

```js
video.addEventListener('timeupdate', function () {
  document.title = this.currentTime +'/'+ this.duration
},false)
```

| 事件             | 描述                                       |
| -------------- | ---------------------------------------- |
| loadstart      | 浏览器开始在网上寻找媒体数据                           |
| progress       | 浏览器正在获取媒体数据                              |
| suspend        | 浏览器暂停获取媒体数据，但是下载过程并滑正常结束                 |
| abort          | 浏览器在下载完全部媒体数据之前中止获取媒体数据，但是并不是由错误引起的      |
| error          | 获取媒体数据过程中出错                              |
| emptied        | video元素或audio元素所在网络突然变为未初始化状态可能原因有两个:1.载入媒体过程中突然发生一个致命错误2.在浏览器正在选择支持的播放格式时，又调用 了load方法重新载入媒体 |
| stalled        | 浏览器尝试获取媒体数据失败                            |
| play           | 即将开始播放，当执行了play方法时触发，或数据下载后元素被设为autoplay属性 |
| pause          | 播放暂停，当执行了pause方式时触发                      |
| loadedmetadata | 浏览器获取完毕媒体的时间长和字节数                        |
| waiting        | 播放过程由于得不到下一帧而暂停播放（例如下一帧尚未加载完毕），但很快就能够得到下一帧 |
| canplay        | 浏览器能够播放媒体，但估计以当前的播放速率不能直接播放完毕，播放期间需要缓冲   |
| canplaythrough | 浏览器能够播放媒体，而且以当前播放速率能够将媒体播放完毕，不再需要进行缓冲    |
| seeking        | seeking属性变为true，浏览器正在请求数据                |
| seeked         | seeking属性变为false，浏览器停止请求数据               |
| timeupdate     | 由于播放位置被改变，可能是播放过程中的自然改变，也可能是被人为的改变，或由于播放不能连续而发生的跳变 |
| ended          | 播放结束后停止播放                                |
| ratechange     | defaultplaybackRate属性（默认播放速率）或playbackRate属性（当前播放速率）被改变 |
| druationchange | 播放时长被改变                                  |
| volumechange   | volume属性（音量）被改变或muted属性（静音状态）被改变         |



**Video API 属性**

```js
video.currentTime  :  开始到播放现在所用的时间
video.duration  :  媒体总时间(只读)
video.volume  :   0.0-1.0的音量相对值
video.muted  :   是否静音 false /true
video.paused  :   媒体是否暂停(只读)
video.ended   :   媒体是否播放完毕(只读)
video.error   :  媒体发生错误的时候，返回错误代码 (只读)
video.currentSrc  :   以字符串的形式返回媒体地址(只读)
video.playbackRate :  播放速度 
video.play
pause
canplay
timeupdate
```

| 属性                                       | 描述                                   |
| ---------------------------------------- | ------------------------------------ |
| [audioTracks](http://www.w3school.com.cn/tags/av_prop_audiotracks.asp) | 返回表示可用音轨的 AudioTrackList 对象          |
| [autoplay](http://www.w3school.com.cn/tags/av_prop_autoplay.asp) | 设置或返回是否在加载完成后随即播放音频/视频               |
| [buffered](http://www.w3school.com.cn/tags/av_prop_buffered.asp) | 返回表示音频/视频已缓冲部分的 TimeRanges 对象        |
| [controller](http://www.w3school.com.cn/tags/av_prop_controller.asp) | 返回表示音频/视频当前媒体控制器的 MediaController 对象 |
| [controls](http://www.w3school.com.cn/tags/av_prop_controls.asp) | 设置或返回音频/视频是否显示控件（比如播放/暂停等）           |
| crossOrigin                              | 设置或返回音频/视频的 CORS 设置                  |
| [currentSrc](http://www.w3school.com.cn/tags/av_prop_currentsrc.asp) | 返回当前音频/视频的 URL                       |
| [currentTime](http://www.w3school.com.cn/tags/av_prop_currenttime.asp) | 设置或返回音频/视频中的当前播放位置（以秒计）              |
| [defaultMuted](http://www.w3school.com.cn/tags/av_prop_defaultmuted.asp) | 设置或返回音频/视频默认是否静音                     |
| [defaultPlaybackRate](http://www.w3school.com.cn/tags/av_prop_defaultplaybackrate.asp) | 设置或返回音频/视频的默认播放速度                    |
| [duration](http://www.w3school.com.cn/tags/av_prop_duration.asp) | 返回当前音频/视频的长度（以秒计）                    |
| [ended](http://www.w3school.com.cn/tags/av_prop_ended.asp) | 返回音频/视频的播放是否已结束                      |
| [error](http://www.w3school.com.cn/tags/av_prop_error.asp) | 返回表示音频/视频错误状态的 MediaError 对象         |
| [loop](http://www.w3school.com.cn/tags/av_prop_loop.asp) | 设置或返回音频/视频是否应在结束时重新播放                |
| [mediaGroup](http://www.w3school.com.cn/tags/av_prop_mediagroup.asp) | 设置或返回音频/视频所属的组合（用于连接多个音频/视频元素）       |
| [muted](http://www.w3school.com.cn/tags/av_prop_muted.asp) | 设置或返回音频/视频是否静音                       |
| [networkState](http://www.w3school.com.cn/tags/av_prop_networkstate.asp) | 返回音频/视频的当前网络状态                       |
| [paused](http://www.w3school.com.cn/tags/av_prop_paused.asp) | 设置或返回音频/视频是否暂停                       |
| [playbackRate](http://www.w3school.com.cn/tags/av_prop_playbackrate.asp) | 设置或返回音频/视频播放的速度                      |
| [played](http://www.w3school.com.cn/tags/av_prop_played.asp) | 返回表示音频/视频已播放部分的 TimeRanges 对象        |
| [preload](http://www.w3school.com.cn/tags/av_prop_preload.asp) | 设置或返回音频/视频是否应该在页面加载后进行加载             |
| [readyState](http://www.w3school.com.cn/tags/av_prop_readystate.asp) | 返回音频/视频当前的就绪状态                       |
| [seekable](http://www.w3school.com.cn/tags/av_prop_seekable.asp) | 返回表示音频/视频可寻址部分的 TimeRanges 对象        |
| [seeking](http://www.w3school.com.cn/tags/av_prop_seeking.asp) | 返回用户是否正在音频/视频中进行查找                   |
| [src](http://www.w3school.com.cn/tags/av_prop_src.asp) | 设置或返回音频/视频元素的当前来源                    |
| [startDate](http://www.w3school.com.cn/tags/av_prop_startdate.asp) | 返回表示当前时间偏移的 Date 对象                  |
| [textTracks](http://www.w3school.com.cn/tags/av_prop_texttracks.asp) | 返回表示可用文本轨道的 TextTrackList 对象         |
| [videoTracks](http://www.w3school.com.cn/tags/av_prop_videotracks.asp) | 返回表示可用视频轨道的 VideoTrackList 对象        |
| [volume](http://www.w3school.com.cn/tags/av_prop_volume.asp) | 设置或返回音频/视频的音量                        |



#### audio

不仅能播放音频，还能进行音频处理。WebAudioAip 提供非常丰富的接口供我们处理音频数据





## canvas

**序言**

 在渲染复杂的动效、把数据可视化图形显示、游戏场景等需求，都会用canvas技术，比dom操作性能更高

 **特点**

 ① H5新增的图形标签，通过提供的JavaScript函数绘制各种图表或利用算法实际非常华丽的动效

 ② 在以前是用Flash技术实现，但不能和JS交互

 ③ 适合动态图形绘制

 **缺点**

 是位图，缩放会模糊

API

环境 目前只有2d绘制

getContext('2d') 创建2D绘制环境

 

**绘制矩形**

rectx,y,w,h)         绘制矩形

fillRect(x,y,w,h)   绘制填充实心矩形

strokeRect(x,y,w,h) 绘制空心矩形

clearRect(x,y,w,h)  清除矩形选区

 

**绘制方式**

stroke( )                     以边框线的方式绘制图形，默认填充黑色

fill( )                           以填充的方式绘制图形，默认填充黑色

 

**绘制样式属性**

fillStyle                填充颜色

strokeStyle                 触笔颜色

lineWidth                   触笔粗细(线宽)

 

**绘制线条**

moveTo(x,y)               从x,y开始绘制

lineTo(x,y)                  绘制到x，y

 

**图形路径**

beginPath()               开始路径

closePath()                结束路径

 

**图形边界样式属性**

lineJoin                     边界连接点样式

​              miter(默认值)

​              round(圆角)

​              bevel(斜角)

lineCap                      端点样式

​              butt(默认值)

​              round(圆角)

​              square(高度多出线宽一半)

 

 

 

三角函数讲解

 

绘制圆形

arc(x,y,r,0,360,false)

​             x,y           圆心坐标位置

​             r         圆半径 

​             0,360        从0度到360度所对应的弧度 (弧度: 角度值*Math.PI/180)

​             true/false 逆时针/顺时针绘图

 

变换

translate(x,y)              重新定义坐标原点基准点

rotate                         旋转角度所对应的弧度 :  弧度公式 ：角度*PI/180

scale(1,1)                   缩放图形宽高

 

独立路径 不影响上下文路径

save()                         保存路径               

restore()                     恢复路径

 

绘制img/video

图片预加载，获取图片文件，顾名思义，WEB中的预加载就是在网页全部加载之前，对一些主要内容进行加载，以提供给用户更好的体验，减少等待的时间。否则，如果一个页面的内容过于庞大，没有使用预加载技术的页面就会长时间的展现为一片空白，直到所有内容加载完毕。

var img = new Image()

img.onload = fn

drawImage(img,x,y,w,h)

绘制图片(img,从img图片的x点开始绘制,从img图片的y点开始绘制,绘制的img宽度,绘制的img高度,绘制在画布的x点,绘制在画布的y点，绘制的图形宽度，绘制的图形高度)

 

设置填充背景

createPattern(img,平铺方式)

​       平铺方式:repeat,repeat-x,repeat-y,no-repeat

 

颜色渐变

线性渐变:createLinearGradient(x1,y1,x2,y2)

​       x1,y1起始坐标点

​       x2,y2结束坐标点

径向渐变:createRadialGradient(x1,y1,r1,x2,y2,r2)

​       x1,y1,r1内圆坐标及半径

​       x2,y2,r2外圆坐标及半径

addColorStop(位置,颜色)

​       位置:渐变点  0-1之间 可多个

 

绘制曲线

arcTo(x1,y1,x2,y2,r)

​       x1,y1坐标一  x2,y2坐标二   r圆弧半径      

quadraticCurveTo(dx,dy,x1,y1)

​       贝塞尔曲线:dx,dy控制点  x1,y1结束坐标

bezierCurveTo(dx1,dy1,dx2,dy2,x1,y1)

​       贝塞尔曲线:dx1,dy1控制点一 dx2,dy2控制点二 x1,y1结束坐标

 

 

绘制文本属性

​       strokeText(文本,x,y)         绘制空心文本

​       fillText(文本,x,y)          绘制实心文本

​       font ="font-size  font-family"    注:尺寸 字体缺一不可

​       textAlign= ""                   文本左右对齐方式 

​              startcenter end  left right

​       textBaseline               文本上下对齐方式 

​              alphabetic                 默认。文本基线是普通的字母基线

​              top                             文本基线是em 方框的顶端

​              hanging                            文本基线是悬挂基线

​              middle                       文本基线是em 方框的正中

​              ideographic               文本基线是表意基线。

​              bottom                       文本基线是em 方框的底端。

​       measureText       (文本).width 文本实际宽度(只有宽度值)

 

阴影属性

​       shadowOffsetX,shadowOffsetY    x轴、y轴偏移

​       shadowBlur     阴影模糊度

​       shadowColor    阴影颜色

​       默认颜色:rgba(0,0,0,0)

 

像素操作

​       createImageData(sx,sy)

​              创建新的、空白的 ImageData 对象

​       getImageData(x1,y1,w,h)

​              返回ImageData 对象，该对象为画布上指定的矩形复制像素数据   putImageData(img,x2,y2)

​              把图像数据（从指定的 ImageData 对象）放回画布上

 

合成

   globalAlpha      设置或返回绘图的当前 alpha 或透明值

   globalCompositeOperation 设置或返回新图像如何绘制到已有的图像上

​       source-over        默认。在目标图像上显示源图像。

​       source-atop        在目标图像顶部显示源图像。源图像位于目标图像之外的部分是不可见的。

​       source-in            在目标图像中显示源图像。只有目标图像内的源图像部分会显示，目标图像是透明的。

​       source-out          在目标图像之外显示源图像。只会显示目标图像之外源图像部分，目标图像是透明的。

​       destination-over       在源图像上方显示目标图像。

​       destination-atop       在源图像顶部显示目标图像。源图像之外的目标图像部分不会被显示。

​       destination-in           在源图像中显示目标图像。只有源图像内的目标图像部分会被显示，源图像是透明的。

​       destination-out         在源图像外显示目标图像。只有源图像外的目标图像部分会被显示，源图像是透明的。

​       lighter                        显示源图像 +目标图像。

​       copy                           显示源图像。忽略目标图像。

​       xor                              使用异或操作对源图像与目标图像进行组合。

 

将画布导出为图片

​       火狐、谷歌浏览器右键菜单可直接导出为图片

​       canvas.toDataURL()         默认导出data:png;base64编码的二进制URL

​       canvas.toDataURL('image/jpeg')         导出data:jpg;base64编码的二进制URL


















