
# 基础部分 #


## 01课 ##

javascript诞生于1995年5月。
javascript之父 Brendan Eich 10天  完成任务的心态。

最初是叫 LiveScript（活力脚本） 傍大牌  营销手段  

javascript与java没有一毛钱关系。  北大和北大青鸟   ，  雷锋和雷峰塔；

几个月后，微软推出IE3  Jscript；

微软的哲学观：当别人火了以后，就要自己捣鼓一个差不多的东西出来，并且这个东西还不好使，过段时间就没人请学，这时候才想着回头来兼容别人的东西，并且还兼容不好。


javascript提交给了Ecma International（一个欧洲的标准化组织），在1997年这个组织就推出了EcmaScript的第一个版本

**  ECMAScript是javascript语言的标准。**

2003年之前有一个外号：牛皮癣。  
2004年：google从js的内部发现了一个对象，ajax，用来进行异步操作；用来提示用户体验。
2008年，google推出chrome浏览器。搭载是google自行开发的V8引擎。
2009年，jquery是js的一个库，开始流行起来。
2010年，canvas画布这个技术，得到了很多浏览器的支持。
2011年，nodejs得到广泛的运用。
2015年，ECMAScript的第6个版本发布。ES2015

JavaScript基于原型的动态解释性脚本语言

### 前端三层 ###

>  -  结构层：html标签
>  -  表现层：css
>  -  行为层：js

---------------------------------------------------------------------------------------------

## 02课 ##


alert()

js代码要写在script标签里



#### script的位置

任意，根据规范，一般写在body结束标签之前。

#### 弹窗

- alert（）	只有一个确定按钮
- confirm（）比alert多了一个取消按钮。
- prompt（）比alert多了一个取消按钮，还多了一个类似input的输入框



#### 注释 

单行注释： //

多行注释：/* */

#### 通过id获取标签 

`document.getElementById("box")`

在js里，对象=标签=节点=元素

调试的一种常用方式：console.log()



#### +号的问题 

- 当 加号 两边都是数字的时候，这时加号是数学意义上的加号运算符。
- 当 加号 两边有其中一边是字符串的时候，就是拼接。

  注意：被引号引起来的东西，不管是啥，都叫字符串。

#### innerHTML 

获取/设置 对象标签内的内容

注意：innerHTML会解析标签。

#### innerText 

获取/设置 对象标签内的内容

注意：跟innerHTML的区别是：innerText 不会解析标签。

#### 等号问题 

在js里，遇到等号，要先读等号的右边，右边读完了才进行赋值。

#### 变量 

变量其实就是起的一个听起来比较高端的东西，

** 使用变量的时候，实际是使用变量的值。**

变量只用声明一次，再次使用不需要声明，直接使用。

#### 变量的命名规则 

1. 注意大小写
2. 可以使用：  字母  数字   $    _  
3. 不能以数字开头
4. 通常要求见名知意。

**字符串两边的引号，在弹窗/打印 的时候，都不会显示出来**

#### 独有标签不需要获取

- body   title   head 这是独有标签
- document.body
- document.title   注意：title 获取的时候，不是标签，而是这个标签的innerHTML
- document.head


--------------------------------------------------------------------------------------------

## 03课 ##

#### 弹窗的问题。####

alert();  说明执行完了就被回收了！

confirm()  点击确定返回true（真），点击取消返回false（假）

prompt()  点击确定返回输入框里输入的内容。点击取消返回null（空）

**变量定义不赋值（系统会在内部默认赋值undefined）**

---

#### document.write() ####

往body的里追加内容。

#### window.onload=函数；

当页面里的所有内容加载完成后，才执行。

注意，如果说在head里引入js文件的时候，为了避免错误，最好放在window.onload里

**window.onload跟document.write配合使用时，会覆盖body里的所有内容**



#### 事件 ####

鼠标事件、键盘事件、表单事件、系统事件

#### 事件注册 ####

对象.事件=函数

#### 函数/方法

底层给用户提供的方法，就叫做API。

function(){}

作用，就是把一堆代码包起来。其实也就是我们常说的封装。

函数分为两种：
* 有名函数，就是说这个函数是有名字的。function **fn**(){};
* 匿名/无名函数，就说没有名字的函数。function(){};

**注意**：匿名函数不能一个人孤独的呆着。

​	   匿名函数必须要一个变量来接收，或者作为事件函数。



#### 有名函数的执行：函数名();  函数名加括号也叫做函数的自执行。

有名函数作为事件函数时，不需要加加括号。



** 在js里，只有函数可以加括号。**

所有加括号的东西，都是函数。



#### 函数里的this

并不是只有事件函数才有this。而是所有的函数都有this关键字。

**这个this关键字的指向是看函数的执行方式来判断的：**

1. 当函数是**自执行**的函数，函数内部this，指向window。
2. 当函数作为事件函数时，事件函数内部的this指向---事件对象。


---------------------------------------------------------------------------------------

## 04课

#### 事件

鼠标、键盘、input、系统

#### 函数

function fn (){}



#### 修改标签的属性

js操作的是行内样式。

js里写样式的时候，遇到了复合样式，要使用驼峰命名。

#### 驼峰命名

例如：background-color

驼峰命名写法就是把第二个及以后单词的首字母大写。**backgroundColor**



修改对象样式有两种方式：

1. 对象.style.样式 = 值；
2. 对象.style.cssText = 所有需要修改的属性，正常写在这里就好。（值是字符串）

#### 标签属性

对象.属性名 = 值；

是一个标签里的属性

1. js操作对象的class类名时要注意，需要写成className



#### 获取元素的其他方式

- 通过class
  **document.getElementsByClassName("class名字")**

- 通过name（这种方式主要是用来真针对获取input）
  **document.getElementsByName("name属性的值")**

- 通过tagName（通过标签选择器）
  **document.getElementsByTagName("标签选择器")**

- 通过querySelectorAll（所有满足条件的对象的集合）
  **document.querySelectorAll("任意css选择器")**

**注意：以上都是集合，使用需要加下标[];(js里所有的下标都是从0开始的)**


- querySelector（选择满足条件的第一个）
  **document.querySelector("任意css选择器")**

**上面这种方式只获取蛮满足条件的第一个对象，不是集合，可以直接使用**

---------------------------------------------------------------------------------------

## 05课

#### 回顾

获取元素的方式

name

className

tagName（标签）

querySelectorAll（“css的选择器都可以传进来”）

**以上获取到的都是集合，就算只有一个，也是集合，使用需要加下标 [对应的下标]**

js里的下标是从0开始的。

**通过style来操作对象的属性**

style读取/设置的是标签的**行内样式**





#### 合法的标签属性

对象.属性名 


#### 自定义标签属性 ####

不可以通过对象.属性名来操作！



#### getAttribute ####

获取自定义标签属性：

对象.getAttribute(“自定义属性名”)



#### setAttribute ####

设置：

对象.setAttribute(“属性名” , “对应的值”)




#### removeAttribute ####

删除：

对象.removeAttribute（“属性名）

**以上的三个方法还可以用来操作合法标签属性，但是非常不建议使用来操作合法的属性**



#### js变量的数据类型 ####

- 基本类型：简单的数据段
  - Undefined
  - Null
  - Boolean
  - Number
  - String
    **不能给基本类型的值添加属性**
- 引用类型：由多个值构成的对象
  - Object

    ​


#### 6大数据类型 ####

`number`  `string`  `boolean` `function` `object` `undefined`

NaN是number类型
null是object类型
所有被引号引起来的都是字符串，
要注意，js里的单双引号没有区别，但是必须成对出现。

-----------------------------------------------------------------------------------------

## 07课

#### 判断if

条件分支语句

判断条件

`>`   `<`   `>=`  `<=`   `==`   `!=`  `===`  `!==`

- `==`	等于  会进行强制类型装转换
- `!=`  不等于  会进行强制类型装转换
- `===`  全等于/恒等于   只会比较值，而不会进行类型转换
- `!==`  不全等于同上



if可以有很多的分支语句，看需求来写，

```	javascript
if(){
     
}else{
     
};
   
if(){
    
}else if(){
           
}else if(){
    
}
//注意：如果if只有真和假的时候，并且真和假的分支都只有一条语句，那么可以写成三目
//  条件 ？ 真的执行语句 ： 假的执行语句；
a>b?alert("大于"):alert("不大于");
//上面这个等价于下面这种写法
if(a>b){
    alert("大于")
}else{
    alert("不大于")
}

```

**如果比较符是全等于的时候 ===**

```javascript
if(a===b){
  alert("跟B是全等的")
}else if(a===c){
  alert("跟C是全等的")
}else if(a===d){
  alert("跟D是全等的")
}
//上面的写法等价于下面的写法
switch (a){
  case b:
    alert("跟B是全等的");
    break;
  case c:
    alert("跟C是全等的")
    break;
  case d:
    alert("跟D是全等的")
    break;
  default:
    alert("都不是")
}
```



**前置++和后置++的区别**

前置++：先自己递增1后，在去进行其他的运算；

后置++：先把自己原来的值拿去进行其他运算后，再自己递增。

**当前置++或者后置++是一条独立语句，并且没有其他运算的时候，没有区别**



#### for（语句1 定义；语句2 条件；语句4 变化量）{语句3 代码块}

执行顺序：

1 》2》3》4》2》3》4》2》3》4》2》3》4》2》3》4》2

最后到2停止。

```javascript
for(var i=0;i < 10; i++){
  	console.log(i)
  	// 0 1 2 3 4 5 6 7 8 9
}
```

---------------------------------------------------------------------------------------

## 08课

#### for循环里有俩关键字
*   continue    //跳出本次循环
*   break;      //跳出所有循环

#### label

标记for

```javascript
fy:  // 给for起名
for(var i=0;i<5;i++){
    fl:
    for(var j=0;j<5;j++){

        if(i===1){
            continue fy;
        }
        console.log("i的第"+i+'次-----'+"j的第"+j+'次')
    }
}
```

#### while、do while ####

```javascript
// while
var i = 2;
while(i<1){
   console.log(i)
   i++;
}

// do while 至少执行一次
var i = 5;
do{
    console.log(i)
    i++;
}while(i<1)
```

--------------------------------------------------------------------------------------

## 09课

#### 运算符

`+` `-` `*` `/`  `%`

`+`  如果+的两边有一边是字符串，那么就是拼接。 在内部悄悄的调用Number()

`-` `*` `/` `%`  如果两边都是数字，就是数学意义上的运算符。
假如 有一边是数字，另外一边不是数字，那么会尝试把不是数字的转换为数字，在进行运算，如果没有办法转为数字，那么就是NaN

`%`  取余 / 模

#### NaN  (not a number)
   不是一个数字，
   NaN的数据类型是number
   isNaN()  用来检测一个对象  是不是NaN，如果是NaN那么返回true，反之false。

   出现NaN的情况，一定是前面有非法的数学运算。


#### 赋值运算符

`=`  `+=`  `-=` `*=` `/=`  `++`  `--`  `%=`


#### 比较运算符 ####

`>` `<` `>=` `<=` `!=` `==` `===` `!==`


#### 逻辑运算符 ####

*  `&&`   与(逻辑与)   并且，遇到true就通过，遇到false就停止， 
*  `||`   或（逻辑或）  或者，遇到false就通过，遇到true就停止。
*  `!`    非           不是自己，取反！不是去false

#### 显示类型转换

*    Number()
   会排除开始和结尾的空格，中间的空格不会被过滤。
        从第一位不是空格的字符开始一直到最后，如果发现不是一个常规的数字，就会返回NaN

*    parseInt()
     从第一个不是空格的字符开始，到不是数字的地方结束。过滤小数部分

*    parseFloat();
     从第一个不是空格的字符开始，到不是数字的地方结束，但是允许小数点出现一次。


--------------------------------------------------------------------------------------

## 10课

### 函数的分类

#### 有名函数

也叫函数声明/函数定义，不能直接在后面加()执行，//不仅不会执行，还会语法报错

	function fn(){}

#### 函数表达式    

可以直接加()执行

	var fn = function (){};

#### 匿名函数

必须自执行，否则无意义

前缀 `!` `+` `-` `~` 或把语句整个括起来

```javascript
(function (){}())
!function (){}()
+function (){}()
-function (){}()
~function (){}()
```

#### 参数 ####

- 函数执行时，括号里传递进函数体的那个参数是： 实参
- 函数体里，使用一个对应变量来接收，函数执行时传进去的参数，叫: 形参
- 形参也需要符合变量的命名规则。
- 在定义步骤时，形参隐藏了定义的过程，并赋值

```javascript
function fn(a){ // 形参,等于var a,
    alert(a)  ==> 1
}

fn(1)  // 实参
```

#### 不定参 ####

`arguments` ：类数组

`arguments.callee` ：代表当前函数

**类数组和数组的区别：** 类数组不能使用数组的方法

#### return ####

函数执行完后被回收，默认的返回值是 `undefined`;


**return**
1. 改变函数的返回值
2. 当函数执行到return 就把 `return` 后面的东西返回，函数停止执行。


--------------------------------------------------------------------------------------

## 11课

#### 隐式类型转换 ####

`-` `*` `/` `++` `--`

以上符号在运算是，会把符号两边的数据转为 `number` 来运算，如果都可以转为 `number` 类型，那就直接运算，
如果有一边不能转为正常数字，就报 `NaN`

#### 小数运算精度的问题 ####

```javascript
var a = 0.1;
var b = 0.2;

var c = a*10 + b*10;  // 以10倍数整数后运算得出结果,再变成小数
alert(c/10)
```

#### eval( ) ####

尝试解析一段字符串当成 JS 代码



--------------------------------------------------------------------------------------

## 12课

#### 解析顺序 ####

从上往下执行

**ES5有声明意义的关键字：**
- var 会存在变量提升
- function 也有声明变量的作用。
- 当function声明的变量和var声明的变量重名时,** `function` 的变量权重会比 `var` 声明的要高**

解析顺序：
      　　1. 找声明，var / function   * 声明：只是声明变量，而不包括赋值
      　　2. 执行
        以上两步：都遵循从上之下，
        　　　　但是执行的时候:如果遇到等号，先看等号右边。


#### 作用域 ####

- ES5里的作用域：
    1.　全局作用域
        2.　函数作用域


> - script是最大的作用域。每一个script 都是一个作用域。
> - 作用域：起作用的范围。
> - 子作用域可以向父作用域找变量，直到找到全局作用域为止，找不到则会报错。
> - 全局变量都是寄存到window对象下, 如果一个属性的宿主是window，那么window可以省略。`window.document`
> - `var a = 2.1; //全局变量`  所有的全局变量都在window对象下
> - 当一个变量没有声明就使用时，不管在哪个作用域出来的，统统归到window下
> - 函数的作用域在函数定义时就决定了它的位置，而不是在执行的时候决定的。只不过这个作用域在执行时，才生效。
> - if、for没有作用域


#### 严格模式 ####

- `'use strict';`
- 严格模式下的代码执行时，非常严格。
- 变量不允许无中生有、
- 意义：规范代码开发的流畅，逻辑
- ES6默认严格模式


--------------------------------------------------------------------------------------

## 13课

#### 闭包 ####

闭包的**形成条件**：
       　1. 函数嵌套函数
       　2. 内部函数使用了外部函数的变量/参数。

作用：内部函数使用到的那个  变量/参数  会被永久的保存在内部函数。


//同一个函数定义，执行多次会产生不同的作用域

优点就是缺点：使用的那个变量会被保存不会被释放（除了刷新页面或关闭页面），由于闭包的特性，会对内存的消耗较大。


```javascript
/*
*   就这个例子而言自执行this也是指向事件对象。
*
*   事件函数的this 定义时默认绑定了事件对象。除非人为改变。
*
*/

box.onclick = function (e) {
    console.log(e)  ==> e 指向box
}

//box.onclick();
```



--------------------------------------------------------------------------------------

## 14课 ##


### 回顾--闭包 ###

事件函数的返回值不能保存

window.onload
document.onclick
...

```javascript
document.onclick = function() {
  var a = 1;
  alert(a);
  return a;  ==> a不能保存
}

// 闭包的使用
document.onclick = function(){
  var a = 1;
  console.log(this)  ==> window
  return function(){
    console.log(this)  ==> document
    alert(++a)
  }
}

for(var i=0; i<aLi.lenght; i++){
  (function(i){
    aLi[i].onclick = function(){
      alert(i)  ==> 不同作用域下的 i
    }
  })(i)
}
```



### 字符串方法 ###

#### 长度 ####

- length

  - 返回字符串的长度（包括空格）
  - 只读属性，不可写（数组可写）
  - `[]`取对应序列号的值（IE7有兼容性问题）
  - `charAt()`取值，解决`[]`兼容性问题



#### ASCII ####

- charCodeAt( )
- String.fromCharCode( )

```javascript
var str = '123'
str.charCodeAt(str[0])  ==> 49
String.fromCharCode(49)  ==> 1
```



#### 查找 ####

- indexOf( )

  [参数1] 要查找字符串
  [参数2] 起始下标

```
var str = '这是一个字符串';
str.indexOf("一个");  ==> 2
str.indexOf('1');  ==> -1 没有找到
```

- charAt( )
  参数为要查找字符的下标，默认为0



#### 替换

- str.**replace**(匹配内容, 替换内容)



#### 截取 ####

- **substring( )**

  `str.substring()` 截取字符串（下标）
  `str.substring(0,5)` // [0,5)  下标0-4 
  `str.substring(5,0) == substring(0,5)` 会交换位置

- **slice( )**

  [参数1] 起始下标
  [参数2] 结束下标
  参数不会交换位置

- **split( )**

  分割字符串成数组
  [参数] 分割点



#### 字母大小写 ####

- str.**toLowerCase( )**

  没有参数，把字母大写变小写

- str.**toUpperCase( )**

  没有参数，把字母小写变成大写


---

### 数组 ###

下标和长度的关系 ： **下标 = length-1**

- **length** ：长度
  可读可写
  []数组下标

- **slice( )** ：截取子项
  - 基于当前数组中的一或多个项创建一个新数组。该方法**不会影响原始数组**。
  - 接受一或两个参数，即要返回项的起始和结束位置。
    - 无参：创建相同内容的新数组
    - 一个参数：从指定起始位置开始到末尾的所有项。
    - 两个参数：从指定起始位置到结束位置所有的项，但不包括结束位置的项。

  ```js
  var arr = [1,2,3,4,5], newArr;
  newArr = arr.slice(1);	// [2, 3, 4, 5]  返回一个新数组
  console.log(arr);  // [1, 2, 3, 4, 5]  原数组没有改变
  /*=======================================*/
  var arr = [1,2,3,4,5], newArr;
  newArr = arr.slice();	// [1, 2, 3, 4, 5]  无参时，创建相同内容的数组
  ```

  ​

- **splice(index, num, info)** ：删除子项
  返回删除的数组，**会改变原数组**
  [参数1] 下标
  [参数2] 删除的个数
  [参数3] 替换的内容

  ```js
  var arr = [1,2,3,4,5];
  arr.splice(1);  // [2,3,4,5] 返回被删除的数组，一个参数时，从下标1开始删到结尾
  console.log(arr);  // [1]  已改变的数组

  arr = [1,2,3,4,5];
  arr.splice(1, 2);  // [2,3] 返回被删除的2个子项，从下标1开始删除的2个子项
  console.log(arr);  // [1,4,5]  被删除子项后的数组
  ```

  ​

- **join( )** ：数组 -> 字符串
  把数组拼接成字符串，不会改变原数组
  [参数] 拼接符



#### 添加 ####

- **push( )**
  数组后面追加一项，返回修改后数组的长度
  arr[arr.length] = 123
  arr[arr.length] = 456
  arr[arr.length] = 789

- **unshift( )**
  在数组最前面加子项
  [参数] 添加的内容



#### 删除 ####

- **pop( )**
  删除数组的最后一项，返回移除的值

- **shift( )**
  删除数组的第一项，返回该项，同时将数组长度减1




#### 排序 ####

- **sort(function( ){ })**
  默认按升序排列，会改变原数组。会调用每个数组项的 toString() 转型方法，然后比较得到的**字符串**

```
arr.sort(function(a,b){
  return a-b;
  return b-a;
  return 1;  倒置
  return -1;  
  return Math.random()-0.3;  随机
})
```

- **reverse( )**
  反转数组项的排序



#### 合并数组 ####

- **concat( )**
  基于当前数组中的所有项创建一个新数组

```
newArr = arr1.concat(arr2)
```



#### 过滤/筛选 ####

- **filter(function( ){ })**
  过滤，不会改变原数组

```
// 取偶数
var newArr = arr.filter(function(t){
  if(t%2 == 0) return true;
})

```



#### 数组项求和

##### reduce()方法

`reduce()`方法接收一个函数`callbackfn`作为累加器（accumulator），数组中的每个值（从左到右）开始合并，最终为一个值。

**语法**

```js
array.reduce(callbackfn,[initialValue])
```

`reduce()`方法接收`callbackfn`函数，而这个函数包含四个参数：

```js
function callbackfn(preValue,curValue,index,array){}
```

- **preValue**: 上一次调用回调返回的值，或者是提供的初始值（initialValue）
- **curValue**: 数组中当前被处理的数组项
- **index**: 当前数组项在数组中的索引值
- **array**: 调用 `reduce()`方法的数组

而`initialValue`作为第一次调用 `callbackfn`函数的第一个参数。

`reduce()`方法为数组中的每一个元素依次执行回调函数`callbackfn`，不包括数组中被删除或从未被赋值的元素，接受四个参数：初始值（或者上一次回调函数的返回值），当前元素值，当前索引，调用 `reduce()` 的数组。

回调函数第一次执行时，`preValue` 和 `curValue` 可以是一个值，如果 `initialValue` 在调用 `reduce()` 时被提供，那么第一个 `preValue` 等于 `initialValue` ，并且`curValue` 等于数组中的第一个值；如果`initialValue` 未被提供，那么`preValue` 等于数组中的第一个值，`curValue`等于数组中的第二个值。

来看一个示例：

```js
var arr = [0,1,2,3,4];

arr.reduce(function (preValue,curValue,index,array) {
    return preValue + curValue;
}); // 10

```

示例中的回调函数被执行四次，每次参数和返回的值如下：

|       | preValue | curValue | index | array       | 返回值  |
| ----- | -------- | -------- | ----- | ----------- | ---- |
| 第一次回调 | 0        | 1        | 1     | [0,1,2,3,4] | 1    |
| 第二次回调 | 1        | 2        | 2     | [0,1,2,3,4] | 3    |
| 第三次回调 | 3        | 3        | 3     | [0,1,2,3,4] | 6    |
| 第四次回调 | 6        | 4        | 4     | [0,1,2,3,4] | 10   |

上面的示例`reduce()`方法没有提供`initialValue`初始值，接下来再上面的示例中，稍作修改，提供一个初始值，这个值为`5`。这个时候`reduce()`方法会执行五次回调，每次参数和返回的值如下：

```js
var arr = [0,1,2,3,4];

arr.reduce(function (preValue,curValue,index,array) {
    return preValue + curValue;
}, 5); //15

```

|       | preValue | curValue | index | array       | 返回值  |
| ----- | -------- | -------- | ----- | ----------- | ---- |
| 第一次回调 | 5        | 0        | 0     | [0,1,2,3,4] | 5    |
| 第二次回调 | 5        | 1        | 1     | [0,1,2,3,4] | 6    |
| 第三次回调 | 6        | 2        | 2     | [0,1,2,3,4] | 8    |
| 第四次回调 | 8        | 3        | 3     | [0,1,2,3,4] | 11   |
| 第五次回调 | 11       | 4        | 4     | [0,1,2,3,4] | 15   |

这样一来，不用多说，应该都知道，可以使用`reduce()`实现数组求和的功能。如：

```js
var arr = [1,2,3,4,5,6];

Array.prototype.sum = function (){
    var sumResult = 0;
    return this.reduce(function (preValue, curValue) {
        return sumResult = preValue + curValue;
    });
    return sumResult;
}
arr.sum(); // 21

```

回到文章的前面，来看看使用`reduce()`方法对数组求和，需要多少时间：

```js
var arr = [1,2,3,4,5,6];

console.time("ruduce");
Array.prototype.ruduceSum = function (){
    for (var i = 0; i < 10000; i++) {
        return  this.reduce (function (preValue, curValue) {
            return preValue + curValue;
        });
    }
}
arr.ruduceSum();
console.log('最终的值：' + arr.ruduceSum()); // 21
console.timeEnd("ruduce"); // 0.417ms

```



##### reduceRight()方法

`reduceRight()`方法的功能和`reduce()`功能是一样的，不同的是`reduceRight()`从数组的末尾向前将数组中的数组项做累加。

`reduceRight()`首次调用回调函数`callbackfn`时，`prevValue` 和 `curValue` 可以是两个值之一。如果调用 `reduceRight()` 时提供了 `initialValue` 参数，则 `prevValue` 等于 `initialValue`，`curValue` 等于数组中的最后一个值。如果没有提供 `initialValue` 参数，则 `prevValue` 等于数组最后一个值， `curValue` 等于数组中倒数第二个值。

来看实例：

```js
var arr = [0,1,2,3,4];

arr.reduceRight(function (preValue,curValue,index,array) {
    return preValue + curValue;
}); // 10

```

回调将会被调用四次，每次调用的参数及返回值如下：

|       | preValue | curValue | index | array       | 返回值  |
| ----- | -------- | -------- | ----- | ----------- | ---- |
| 第一次回调 | 4        | 3        | 3     | [0,1,2,3,4] | 7    |
| 第二次回调 | 7        | 2        | 2     | [0,1,2,3,4] | 9    |
| 第三次回调 | 9        | 1        | 1     | [0,1,2,3,4] | 10   |
| 第四次回调 | 10       | 0        | 0     | [0,1,2,3,4] | 10   |

如果提供一个初始值`initialValue`为`5`:

```js
var arr = [0,1,2,3,4];

arr.reduceRight(function (preValue,curValue,index,array) {
    return preValue + curValue;
}, 5); // 15

```

回调将会被调用五次，每次调用的参数及返回的值如下：

|       | preValue | curValue | index | array       | 返回值  |
| ----- | -------- | -------- | ----- | ----------- | ---- |
| 第一次回调 | 5        | 4        | 4     | [0,1,2,3,4] | 9    |
| 第二次回调 | 9        | 3        | 3     | [0,1,2,3,4] | 12   |
| 第三次回调 | 12       | 2        | 2     | [0,1,2,3,4] | 14   |
| 第四次回调 | 14       | 1        | 1     | [0,1,2,3,4] | 15   |
| 第五次回调 | 15       | 0        | 0     | [0,1,2,3,4] | 15   |

同样的，可以对一个数组求和，也可以使用`reduceRight()`方法:

```js
var arr = [1,2,3,4,5,6];

console.time("ruduceRight");
Array.prototype.ruduceRightSum = function (){
    for (var i = 0; i < 10000; i++) {
        return  this.reduceRight (function (preValue, curValue) {
            return preValue + curValue;
        });
    }
}
arr.ruduceRightSum();
console.log('最终的值：' + arr.ruduceSum()); // 21
console.timeEnd("ruduceRight"); // 5.725ms

```

**总结**

`reduce()`和`reduceRight()`两个方法功能都是类似的，可以让数组调用一个回调函数`callbackfn`作为累加器。实际上根据这个回调函数，可以实现不同的功能，比如说，对数组项求合；将多个数组合并到一个数组等等。甚至配合数组其他的方法你还可以做更多功能的处理。如果感兴趣的话不仿尝试一二。



#### 遍历数组 ####

- **Array.forEach( )** ：遍历数组里的每个元素
  .forEach()方法没有返回值，你不需要在回调函数里写return，你可以在回调函数里对每个元素进行操作。

```
var animals = ['dog', 'cat', 'mouse'];
animals.forEach( function (item,index,arr){
    console.log(item,index,arr,this);
},false);
```

- **Array.map()**
  .map() 方法能够遍历整个数组，然后 返回一个新数组，这个新数组里的元素是经过了指定的回调函数处理过的。
  > *如果你想修改数组里的每个元素，然后将修改后的数组存入新的数组，那使用 .map() 方法最方便。*

```
var numbers = [2, 4, 6, 8];
var doubleNums = numbers.map( function (element) {
  return element * 2;
});
console.log('doubleNums: ', doubleNums)
```

- **Array.indexOf()**
  indexOf() 能够告诉你 某个元素在数组中的位置，它返回的是索引值，如果数组里有重复的元素，它会返回第一个元素的位置。

```
var a = [2, 9, 9, 18];
var i = a.indexOf(9);
console.log('i: ', i);  /*if (a.indexOf(7) === -1) { // 数组中没有这个元素}*/
```

- **Array.every()**
  .every() 方法的作用是用指定的回调函数去检查数组中的每个元素，如果对于每个元素，这个回调函数都返回true，则.every()返回true。否则，.every() 返回false。
  > *如果你想知道数组中的所有元素都是否符合某种条件，使用 .every() 最方便。*

```
var ages = [23, 19, 32, 44];
var olderThan18 = ages.every( function (element) {
  return element > 18;
});
console.log('olderThan18: ', olderThan18);
```



#### 判断是否为数组 ####

- **Array.isArray( )**
  判断接受的对象 是否为数组，返回一个布尔值
  不兼容 IE9 及以下




### 格式化数字转成汉字（两位数）

```js
function formatNum(n){
  var unitsDigit = n%10,
      tensDigit = Math.floor(n/10),
      arr = ["十","一","二","三","四","五","六","七","八","九"],
      str = "";
  
  if (tensDigit) {
    str = tensDigit>1 ? arr[tensDigit] : "";
    str += "十";
    if (unitsDigit != 0) {
      str += arr[unitsDigit];
    }
  } else {
    str = arr[unitsDigit]
  }
  
  return str
  
}

for (var i=1; i<100; i++) {
  console.log(formatNum(i));
}
```







--------------------------------------------------------------------------------------

## 15课 ##

封装函数：操作元素 class 的添加或删除

#### addClass & removeClass ####

```javascript
function addClass(ele,cName) {
    var arr = ele.className.split(' ').concat(cName.split(" "));
    for(var i=0;i<arr.length;i++){
        for(var k=arr.length-1;k>i;k--){
            (arr[k]==="")&&arr.splice(k,1)
            (arr[i]===arr[k])&&arr.splice(k,1)
        }
    }
    ele.className = arr.join(" ");
}


function removeClass(ele,cName) {
    var arr1 = ele.className.split(' ');//on wrap fy on on on on
    var arr2 = cName.split(" ");// on wrap
    for(var i=0;i<arr2.length;i++)for(var j=arr1.length-1;j>=0;j--)(arr2[i]===arr1[j])&&arr1.splice(j,1)
    ele.className = arr1.join(" ")
}
```

#### 逻辑与代替if ####

```javascript
if (true){ alert(1) } // 可简写成下面的语句
true && alert(1);
```



--------------------------------------------------------------------------------------

## 16课 ##


#### 冒泡排序 ####

```javascript
//a = [b,b=a][0];//交换值

/*for(var i=0;i<arr.length-1;i++){//确定趟数
    for(var j=arr.length-1;j > i;j--){
        if(arr[j]<arr[j-1]){//后一个值跟前一个值比较，如果后一个值比前一个小，就交换位置
            arr[j] = [arr[j-1],arr[j-1]=arr[j]][0]
        }
    }
}*/

//简化
for(var i=0;i<arr.length-1;i++)for(var j=arr.length-1;j > i;j--)(arr[j]<arr[j-1])&&(arr[j] = [arr[j-1],arr[j-1]=arr[j]][0])
```


#### 动态获取和静态获取 ####

动态和静态的区别：
- 静态只会获取一次，而动态每次使用到这个变量，都会隐式的去再获取一次。

静态的方法有：
- getElementById
- querySelector
- querySelectorAll


 除了上面三个 其他都是动态。


#### json对象 ####

- 对象里的数据存放法方式：键值对
- json格式，在其他语言里，对象的属性必须加双引号
- 取值： 对象.属性名
- `[]` 代替点操作时：括号里需要是字符串，除了数字直接作为属性名时，可以不用变为字符串
- 对象再弹窗是表现为[object Object]；
- 对象没有长度length。


#### 删除json属性 ####

	json.key = null
	delete json['key']
	delete json.key

#### for in ####


- forin循环里定义的变量i，在遍历对象时，代表了每次循环时遍历到的那个属属性名，取值必须 对象[i]
- 在遍历数组时，代表数组的下标. 取值 ：数组[i]


	for (var i in obj){}  ==> i代表obj的每个属性名
	
	

--------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------

## 17课 ##

#### call ####

函数.**call(obj, a, b)**
call接收的参数个数不限制，看需求，但是第一个必须是this需要指向的对象，函数执行需要的参数写在后面就好


#### apply ####

函数.**apply(obj, [a, b])**
接收的参数只有俩个，第一个：需要改变this指向的对象；第二个必须是一个数组，数组里函数需要的参数



#### bind ####

函数.**bind(obj, a, b)**   
也是用来改变this指向，
传参跟call是一样的。
bind是在函数**被执行时**，才去改变this指向。


#### call/apply/bind ####

- `call/apply` 都可以用来改变函数执行时的this指向, 会**主动执行**函数.
- `bind` 跟 `call/apply` 的区别：不会主动执行函数。
- `call` 和 `apply` 没有兼容问题，`bind` 不兼容IE678
- ~~当不得不适用 `call/apply/bind` 时，而又不希望改变指向，就传null。~~
- 改变this指向时，只对本次执行生效。
- 需要指向 `window` 时，可以传 `null` / `window`，如果不传实参，也是默认指向 `window`
- es5：类数组转为数组： `[].slice.apply(arguments)`




#### 判断浏览器 IE678 ####

利用 IE 对数组长度解析与其他浏览器不同的特征

```javascript
//alert([1,2,].length)
//alert(Number([1,]))
//alert(Boolean(NaN))

if(!-[1,]){
    alert("这是IE678")
}

//  !-[1,]  // IE识别数组长度为2，减号转换成数字类型不成功为 NaN， !NaN = true 时为 IE678
```

#### 遍历json属性到数组 ####

```javascript
/*
*   遍历对象的属性到数组。
*
* */
var json  = {
    a : 1,
    b : 2,
    name : "FY"
}
var arr = [];
for ( arr[arr.length] in json) arr[arr.length] = key
console.log(arr)
```



--------------------------------------------------------------------------------------

## 18课 ##

#### setInterval( ) ####

> 循环执行

- [参数1]：函数 或 字符串
- [参数2]：时间间隔，单位 ms(毫秒)



#### setTimeout( ) ####

> 单次执行

- [参数1]：函数
- [参数2]：时间间隔，单位 ms(毫秒)


#### 定时器 ####

- 当函数有 alert( ) ,定时器会在点击确定之前暂时计时
- 浏览器最低的刷新频率 13~20
- **事件队列**，即时函数都为第一队列。定时器里的事件，属于下一次的事件队列，即使时间间隔为0，也是放在最后面执行


#### 定时器的返回值 ####

定时器的返回值：是一些 number 类型的数字，代表定时器的序号。
通过序号也能清除定时器


#### 清除定时器 ####

- clearInterval( )
- clearTimeout( )



#### H5动画方法 ####

timer = requestAnimationFrame(fn)  // 开启
始终与浏览器刷新频率保持一致
IE6789不兼容
cancelAnimationFrame(timer)  // 取消


setTimeout() 比 setInterval() 方法好





#### console.time ####

计算代码执行间隔的时间

```
console.time('t')

(do something...)

console.timeEnd('t')
```

#### window.open( ) ####

- window.open(url ) ： 默认新窗口打开网址
- window.open(url ，"_self") ： 本窗口打开


----

### Math对象 ###

Math是一个对象。


#### 取整 ####

- Math.cile( )	: 向上取整
- Math.floor( ): 向下取整
- Math.round( ): 四舍五入


#### 随机数 ####

- Math.random()	: 返回随机数 [0, 1)

```javascript
// 随机6位16进制
(~~Math.floor(Math.random()*(1<<24))).toString(16)
Math.random().toString(16).slice(2,8)
```


#### 比较值 ####

- Math.max(a, b)	: 返回最大值
- Math.min(a, b): 返回最小值


#### 绝对值 ####

- Math.abs( )	: 返回绝对值


#### 弧度 ####

- Math.sin( 30*Math.PI/180 )  正弦 ： 对边/斜边
- Math.cos( 30*Math.PI/180 )  余弦 ： 邻边/斜边
- 30度 = 30/360 * 2π


#### 平方

```
Math.pow(3,2)   // 平方
Math.sqrt(9)    // 开方
```

--------------------------------------------------------------------------------------

## 19课 ##

#### onmousedown ####

鼠标按下


#### onmouseup ####

鼠标抬起

-----

### Date对象 ###

时间戳
var date = new Date(); 获取的事件是本地(计算机)的时间



| 方法                 | 解析     | 要点                              |
| ------------------ | ------ | ------------------------------- |
| date.getTime()     | 当前的毫秒数 | 距离 1970/1/1 00 :00 :00 至今过了多少毫秒 |
| date.getFullYear() | 获取年份   |                                 |
| date.getMonth()    | 获取月份   | 从0开始到11，正确显示要 +1                |
| date.getDate()     | 获取日期   |                                 |
| date.getHours()    | 获取小时   |                                 |
| date.getMinutes()  | 获取分钟   |                                 |
| date.getSeconds()  | 获取秒钟   |                                 |
| date.getTime()     | 毫秒数    |                                 |
| date.getDay()      | 获取星期   | 周日返回 0 ，周一返回 1                  |


#### 设置日期时间 ####

> 不带参数是获取时间，带参数是设置时间。需要注意一个参数时：带引号是设置年份      。如果一个参数时：参数的类型是number，那就是毫秒值，是距离 [1970/1/1 08:00 :00] 过了多少毫秒 

JavaScript下，new Date([params]),参数传递有以下五种方式：

1. new Date("month dd,yyyy hh:mm :ss"); 
2. new Date("month dd,yyyy"); 
3. new Date(yyyy,mth,dd,hh,mm,ss); 注意：这种方式下，必须传递整型；
4. new Date(yyyy,mth,dd); 
5. new Date(ms); 注意：ms:是需要创建的时间和 GMT时间1970年1月1日之间相差的毫秒数；当前时间与GMT1970.1.1之间的毫秒数：var mills = new Date().getTime();


#### Date.parse() / Date.UTC() ####

date.parse("mth dd yy") //参数必须是字符串
date.UTC(yy,mth,dd)  //不能是字符串

这两参数都接收一个参数，参数里是日期信息。返回该日期到1970/1/1 00:00 :00 的毫秒值

**月的差异**
- Date.parse(); 月[1-12]
- Date.UTC();  月[0-11]

**都可以传递参数**
```
Date.parse("10,24,2016,21:00:00"));
Date.UTC(2016,9,24,21,00,00));
new Date(Date.parse("10,24,2016")));
new Date(Date.UTC(2016,9,24)));
//下面这两个UTC比parse快8小时 这里参数选择的是 -8
new Date(Date.parse("10,24,2016,00:00:00")));
new Date(Date.UTC(2016,9,24,-8,0,0)));
```

#### 获取毫秒值 ####

```js
new Date().getTime()===Date.now()
```

- new Date().getTime()
- Date.now()  不兼容IE678


#### 时间格式化

```js
var d = new Date();

// UTC时间
d.toDateString(); 			// 日期字符串，输出：Mon Nov 04 2013
d.toUTCString(); 			  // 转换为世界时间，输出：Mon, 04 Nov 2013 14:03:05 GMT
d.toGMTString(); 			  // 格林威治时间，输出：Mon, 04 Nov 2013 14:03:05 GMT
d.toISOString(); 			  // 国际标准组织（ISO）格式，输出：2013-11-04T14:03:05.420Z
d.toJSON(); 				    // UTC时间 输出：2013-11-04T14:03:05.420Z

// 本地时间
d.toLocaleDateString(); // 转换为本地日期格式，视环境而定，输出：2013年11月4日
d.toLocaleString(); 		// 转换为本地日期和时间格式，视环境而定，输出：2013年11月4日 下午10:03:05
d.toLocaleTimeString(); // 转换为本地时间格式，视环境而定，输出：下午10:03:05
d.toString(); 				  // 转换为字符串，输出：Mon Nov 04 2013 22:03:05 GMT+0800 (中国标准时间)
d.toTimeString(); 			// 转换为时间字符串，输出：22:03:05 GMT+0800 (中国标准时间)


// 常用转换
new Date().toLocaleDateString().replace(/\//g, '-')  //  ->  "2018-2-24"
new Date().toLocaleDateString().match(/\d+/g).join('-')  //  ->  "2018-2-24"
new Date().toString().split(' ')[4]    //  ->  "19:45:56"
```



#### 日期相差时间 ####

Date对象可以相减


#### getTimezoneOffset ####

回协调世界时（UTC）相对于当前时区的时间差值，单位为分钟。

```
// 通过本地时间 获取UTC时间
var date = new Date();
var Udate = new Date(date.getTime() + date.getTimezoneOffset()*60*1000);
```

--------------------------------------------------------------------------------------

## 20课 ##

### 获取内部样式表的样式 ###

#### window.getComputedStyle(obj) ####

不兼容 IE8

```
var box = document.getElementById('box');
window.getComputedStyle(box).width;  ==> 100px
```


#### obj.currentStyle ####

只支持IE

```
//IE8 下的方法，chrome不支持
box.currentStyle.width;  ==> 100px
```


#### 兼容方法 ####

```
function getStyle(obj){
    return obj.currentStyle || getComputedStyle(obj);
}
```

样式的颜色和路径不能作为判断条件


### H5动画方法 ###
#### requestAnimationFrame(fn) ####
设置动画帧
根据不同浏览器的刷新频率来决定刷新时间
不在当前浏览器标签页则停止，不再占用资源
不兼容 IE9 及以下，用 setTimeout

**兼容方法**
```
window.requestAnimationFrame = window.requestAnimationFrame || function(fn){return setTimeout(fn,1000/60)};

```

#### cancelAnimationFrame(fn) ####
清除动画帧
同样不兼容 IE9

**兼容方法**
```
window.cancelAnimationFrame = window.cancelAnimationFrame || clearTimeout;

```

###  速度版运动框架 ###

```js
function animation(ele, style, target, speed) {     // 元素,样式,目标值,速度
    var start = parseFloat(getStyle(ele)[style]);   // 获取内部样式
    var flag = start>target;                        // 判断与目标值的关系
    if (flag) speed = -speed;                       // 大于目标值时 速度为负
    fn();                                           // 执行动画
    function fn() {
        start += speed;                             // 速度
        if (flag?start<=target:start>=target) {start = target}
        else {requestAnimationFrame(fn)}            // 不到目标值时，回调
        ele.style[style] = start + 'px';
    }
}
```









--------------------------------------------------------------------------------------

## 21课 ##
### 时间版运动框架 ###

```javascript
/**
 * 时间版动画框架
 * @param obj   元素
 * @param json  样式集合
 * @param time  动画时间
 * @param callback  回调函数
 */

var animation = function(obj, json, time, callback) {
    var getStyle = function (obj) {return obj.currentStyle || getComputedStyle(obj)};
    window.requestAnimationFrame = window.requestAnimationFrame || function (fn) {return setTimeout(fn);};
    window.cancelAnimationFrame = window.cancelAnimationFrame || clearTimeout;
    var initDate = new Date();
    var initArr = {}, distanceArr = {};
    for (var key in json) {
        initArr[key] = parseFloat(getStyle(obj)[key]);
        distanceArr[key] = json[key] - parseFloat(getStyle(obj)[key]);
        if (!distanceArr[key]) {
            delete initArr[key];
            delete distanceArr[key]
        }
    }
    fn();
    function fn() {
        var ppt = (new Date() - initDate)/time;
        ppt>=1?ppt=1:requestAnimationFrame(fn);
        for (var key in distanceArr) {
            if (key === 'opacity') {
                obj.style.opacity = ppt*distanceArr.opacity+initArr.opacity;
                obj.style.filter = 'alpha(opacity='+(ppt*distanceArr.opacity+initArr.opacity)*100+')';
            } else {
                obj.style[key] = ppt * distanceArr[key] + initArr[key] + 'px';
            }
        }
        if (ppt === 1 && callback) callback.call(obj);
    }
};
```



# DOM部分 #

## 22课 ##

### javascript的三大核心 ###



1. **ECMAScript**

   ES是js的语法标准，js是ES的实现
   js里最大的 BOSS 是 window对象。
   document是window下的一个对象。



2. **DOM**

   document Object Model    文档对象模型提供的方法
   js 只能通过 **DOM方法** 去操作 节点



3. **BOM**

   browser Objest Model    浏览器对象模型
   提供方法让 JS 可以操作浏览器 





### DOM ###

文档树

独有标签可以直接使用 ，html 除外

取html标签：document.documentElement









--------------------------------------------------------------------------------------

## 23课 ##

### DOM 节点种类 ###

| DOM 节点种类 | 种类                                  | nodeType值 |
| -------- | ----------------------------------- | --------- |
| **元素节点** | **Node.ELEMENT_NODE(1)**            | **1**     |
| **属性节点** | **Node.ATTRIBUTE_NODE(2)**          | **2**     |
| **文本节点** | **Node.TEXT_NODE(3)**               | **3**     |
| CDATA节点  | Node.CDATA_SECTION_NODE(4)          | 4         |
| 实体引用名称节点 | Node.ENTRY_REFERENCE_NODE(5)        | 5         |
| 实体名称节点   | Node.ENTITY_NODE(6)                 | 6         |
| 处理指令节点   | Node.PROCESSING_INSTRUCTION_NODE(7) | 7         |
| **注释节点** | **Node.COMMENT_NODE(8)**            | **8**     |
| 文档节点     | Node.DOCUMENT_NODE(9)               | 9         |
| 文档类型节点   | Node.DOCUMENT_TYPE_NODE(10)         | 10        |
| 文档片段节点   | Node.DOCUMENT_FRAGMENT_NODE(11)     | 11        |
| DTD声明节点  | Node.NOTATION_NODE(12)              | 12        |



### DOM属性 ###

| DOM属性                  | 获取                                      | 描述                                       |
| ---------------------- | --------------------------------------- | ---------------------------------------- |
| **nodeType**           | **节点类型**                                | **1元素节点 2属性节点 3文本节点 8注释节点**              |
| childNodes             | 所有子节点对象，包括文本节点                          | 在不同浏览器下表现不一样<br>在IE8，只会返回元素节点            |
| **children**           | 所有**子元素节点**                             | 类数组，**动态方法**                             |
| fristChild             | 第一个子节点                                  |                                          |
| lastChild              | 最后一个子节点                                 |                                          |
| firstElementChild      | 第一个**子元素节点**                            | 不兼容IE8                                   |
| lastElementChild       | 最后一个**子元素节点**                           | 不兼容IE8                                   |
| nextSibling            | 下一个兄弟节点                                 | 在主流的浏览器下，可能会拿到除了元素节点以外的节点。在IE8，只会返回元素节点，如果没有则返回null |
| previousSibling        | 返回上一个兄弟节点                               | 在主流的浏览器下，可能会拿到除了元素节点以外的节点。在IE8，只会返回元素节点，如果没有则返回null |
| nextElementSibling     | 下一个兄弟**元素节点**                           | 不兼容IE8                                   |
| previousElementSibling | 上一个兄弟**元素节点**                           | 不兼容IE8                                   |
| **parentNode**         | **返回父级节点**                              | **没有兼容性问题**                              |
| **offsetParent**       | **返回第一个position定位的父级。如果都没有找到，最终返回body** | **没有兼容性问题**                              |
| ownerDocument          | 返回元素的根元素                                | HTML中, HTML 文档本身是元素的根元素。                 |
| nodeValue              | 获取第一个按钮元素的节点值                           | nodeValue等同于：.innerText  或.textContent   |
| nodeName               | 返回标签的构造器                                | 与tagName值相同                              |



---

#### HTMLCollection 对象 ####

HTMLCollection 是一个接口，表示 HTML 元素的集合，它提供了可以遍历列表的方法和属性。

HTML DOM 中的 HTMLCollection 是“活”的；如果基本的文档改变时，那些改变通过所有 HTMLCollection 对象会立即显示出来。



### DOM方法 ###



| DOM方法                    | 描述                                       |
| ------------------------ | ---------------------------------------- |
| getElementById()         | 返回带有指定 ID 的元素。                           |
| getElementsByTagName()   | 返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。         |
| getElementsByClassName() | 返回包含带有指定类名的所有元素的节点列表。                    |
| **appendChild()**        | 把新的子节点添加到指定节点。                           |
| **removeChild()**        | 删除子节点。但不能移除自己，只能通过父级来调用                  |
| replaceChild()           | 替换子节点。                                   |
| hasChildNodes()          | 表明当前节点是否包含有子节点，返回一个布尔值                   |
| **insertBefore**()       | 在指定的子节点前面插入新的子节点。                        |
| createAttribute()        | 创建属性节点。                                  |
| **createElement()**      | 创建元素节点(构造器)<br />需要接收一个参数，参数就是需要新建的标签<br />只能使用一次<br />与obj.innerHTML的性能问题，后者性能好。但是要绑定事件用前者 |
| **createTextNode**()     | 创建文本节点。标签不会被解析                           |
| **createComment**()      | 创建注释节点                                   |
| getAttribute()           | 返回指定的属性值。                                |
| setAttribute()           | 把指定属性设置或修改为指定的值。                         |
| removeAttribute()        | 删除指定的属性                                  |
| createDocumentFragment() | 创建一个文档碎片，把要插入的新节点先附加在它上面，然后再一次性添加到document中 |



### 操作节点内容 ###

- obj.innerHTML    ：    操作标签内的内容，如有标签会被解析

- obj.innerText    ：    标签不会被解析






--------------------------------------------------------------------------------------



## 24课 ##



#### cloneNode() ####

返回克隆的节点 `克隆母体.cloneNode()`

接收一个参数，这个参数是一个布尔值，默认false：浅复制。true：深复制

浅复制：只复制标签

深复制：把跟这个标签对象相关的标签行内的内容(显性属性)一起复制



### 元素的宽高属性 ###

| 获取宽/高                    | 只读属性，返回 Number，内容超出时值不变                  |
| ------------------------ | ---------------------------------------- |
| **clientWidth**          | 读取元素的style宽 + padding，内容超出时值不变           |
| **clientHeight**         | 读取元素的style高 + padding，内容超出时值不变           |
| **clientTop**            | 返回对象border上边框的大小                         |
| **clientLeft**           | 返回对象border左边框的大小                         |
| **offsetWidth**          | 读取元素的style宽 + border + padding，内容超出时值不变  |
| **offsetHeight**         | 读取元素的style高 + border + padding，内容超出时值不变  |
| **scrollWidth**          | 读取元素的content宽 + padding，    当内容超出时 content+左padding，    当内容超出hidden时 content+左右padding |
| **scrollHeight**         | 读取元素的content高 + padding，    当内容超出时 content+上padding，    当内容超出hidden时 content+上下padding |
| getBoundingClientTect()  | 得到矩形元素的界线，返回的是一个对象，包含  top, left, right, bottom 四个属性值 |
| element.scrollIntoView() | 让元素滚动到可视区域（HTML5标准),参数  true  与浏览器对齐， false 元素在窗口居中显示 |




### 元素的定位距离 ###

- **offsetLeft**    ：获取到 定位父级 的left距离

- **offsetTop**        ：获取到 定位父级 的top距离



### 文档相关的值 ###

读取body实际的宽高，不受滚动条影响，只读属性

- **document.body.clientWidth**    ：文档body的宽度

- **document.body.clientHeight**    ：文档body的高度



### 可视区域的宽高 ###

- **document.documentElement.clientWidth**    ：浏览器可视区域的宽度，不包括滚动条

- **document.documentElement.clientWidth**    ：浏览器可视区域的高度，不包括滚动条

- **window.innerWidth**        ：浏览器可视区域的宽度，包括滚动条，不兼容IE8

- **window.innerHeight**        ：浏览器可视区域的高度，包括滚动条，不兼容IE8



### 滚动距离 ###

有兼容性问题

- **document.body.scrollTop**        ：谷歌 62.0.3版本之前的方法

- **document.body.scrollLeft**    ：谷歌 62.0.3版本之前的方法

- **document.documentElement.scrollTop**        :设置或获取位于对象最顶端和对象中可见内容的最顶端之间的距离

- **document.documentElement.scrollLeft**        :设置或获取位于对象左边界和对象中目前可见内容的最左端之间的距离



```js
document.body.scrollTop || document.documentElement.scrollTop  //兼容写法
```



### 滚动事件 ###

window.onscroll = fn()

Element.onscroll = fn()





--------------------------------------------------------------------------------------



## 25课 ##



### 改变窗口时触发事件 ###

window.onresize = fn()



### 浏览器窗口大小 ###

#### 获取显示器当前分辨率的大小 ####

- window.screen.width

- window.screen.height



#### 获取显示器当前除了任务栏高度的区域的大小 ####

- window.screen.availWidth

- window.screen.availHeight


--------------------------------------------------------------------------------------



## 26课 ##

### BOM ###



#### Window对象 ####



- **window.history.back()**：跳转前一条历史记录

  **window.history.forward()**：跳转后一条历史记录

  **window.history.go(n)**：跳转基于当前页面的第n条历史记录。接受一个参数 Number。当前为0 ，前一条为 -1，后一条为 1

  **window.history.length**：保存历史记录的数量



**window.open(url)**：默认新窗口打开url

  **window.open(url, "_self")**    ：当前窗口打开

  **window.open(url, "窗口名称", "width=200,height=200")**    ：宽高



**window.close()**：关闭当前标签页




#### url信息 ####

**window.location.href = url**：重定向url，可后退

  **window.location.host**    ：主机名+端口号

  **window.location.hostname**    ：主机名

  **window.location.port**    ：端口号

  **window.location.search**    ：查询的信息  get的内容

  **window.loaction.replace("url")**    ：跳转到 url，不可后退

  **window.loaction.reload()**    ：重新加载当前显示的页面，若传参 true 则强制从服务器重新加载





window.navigator 浏览器信息





#### window.event事件对象 ####



- **e = e || window.event;**：兼容



- **event.pageX / event.pageY**：在IE678不支持，拿到的是相对文档顶部（左边）的绝对距离（坐标），

  兼容写法`document.documentElement.scrollTop + clientY`



- **event.clientX / event.clientY**： 拿到的是可视屏幕区域鼠标到左顶点的距离（坐标）



- **event.screenX / event.screenY**： 相对于整个电脑屏幕的坐标位置 



- **event.type**：事件类型（click/mouseenter/keydown/scroll）



- **e.keyCode**：键盘键值






--------------------------------------------------------------------------------------



## 27课 ##



### 原始数据类型 / 基础数据类型 ###

- number

- string

- boolean

- undefined

- null

在比较时，原始数据类型只会比较值是不是长得一样。如果是则true

在赋值时，就是把这个值赋值给一个变量/对象。给完以后就没有其他什么事



### 引用数据类型 ###

- object

- function

- array

在比较时，主要比较内存地址是否一致，只有一致才会返回true







### 添加/移除 DOM事件监听 ###

- **addEventListener()**

    添加事件绑定

    ele.addEventListener(事件类型, 事件函数, 布尔值)

    布尔值：默认false，不捕获（事件冒泡）。true，事件捕获

    不兼容IE8



- **removeEventListener()**

    移除事件绑定

    ele.removeEventListener(事件类型, 事件函数, 布尔值)

    不兼容IE8



- **attachEvent()**

    IE8的添加事件绑定

    attachEvent(on事件类型, 事件函数)

    后绑定先执行

    注意：此方法里的事件函数this指向window



- **detachEvent()**

    IE8的移除事件绑定

    detachEvent(on事件类型, 事件函数)





### 事件捕获 ###

事件先从父级触发，依次到子级

IE8没有事件捕获





### 事件冒泡 ###

事件先从子级触发，依次到父级



### 阻止冒泡 ###

event.stopPropagation()  //不兼容IE8，W3C标准

event.cancelBubble = true; //兼容IE8与最新chrome firefox

阻止冒泡要在事件源上进行阻止



### 阻止默认行为 ###

event.preventDefault()  //不兼容IE8

window.event.returnValue = false;  //IE8-10

return false;




```js
/**
 * 兼容性查询
 *
 *      事件绑定
 *          chrome/firefox/IE9-11 : document.addEventListener(type, handler)
 *
 *          IE8                   : document.attachEvent(type, handler(e))
 *
 *
 *      事件移除
 *          chrome/firefox/IE9-11 : document.removeEventListener(type, handler)
 *
 *          IE8                   : document.detachEvent(type, handler(e))
 *
 *
 *      阻止事件冒泡
 *          chrome/firefox/IE9-11 : event.stopPropagation()  ||  event.cancelBubble = true
 *
 *          IE8                   : event.cancelBubble = true
 *
 *
 *      阻止事件默认行为
 *         chrome/firefox/IE9-11  : event.preventDefault()
 *
 *         IE8  chrome            : event.returnValue = false
 *
 * */
```









---

**document.onselectstart=function(){}**：文字选中事件

**document.oncontextmenu=function(){}**：鼠标右键事件

**document.onmousewheel=function(){}**：鼠标滚轮事件







--------------------------------------------------------------------------------------



## 28课 ##



### 滚轮事件 ###

- onmousewheel : 支持除了火狐以外所有浏览器

- DOMMouseScroll    ：只支持火狐



### 滚轮方向 ###

- e.wheelDelta  ：支持除了火狐以外所有浏览器

- e.detail ：只支持火狐



```

/**
 * 兼容性查询
 *
 *      chrome/IE9-11  : addEventListener("mousewheel", fn)
 *
 *      firefox        : addEventListener("DOMMouseScroll", fn)
 *
 *      IE8-10         : attachEvent("onmousewheel", fn)
 *
 *      ------------------------------------------------------
 *                                        up       down
 *
 *      chrome/IE   : e.wheelDelta        120      -120
 *
 *      firefox     : e.detail            -3       3
 *
 * */

```



--------------------------------------------------------------------------------------



## 29课 ##



### 事件委托/事件代理 ###

把事件运用 事件冒泡/捕获 让一个其他对象代为执行。



### 事件源 ###

event.target

不兼容IE8

IE8：event.srcElement

兼容写法：This = e.target || e.srcElement





--------------------------------------------------------------------------------------



## 30课 ##



ondragstart="return false" ：禁止拖动







#### 焦点 ####

有焦点的元素 input/select/textarea/button/a/document

**input.onfocus = func;** ： 获得焦点

**input.onblur = func;**  ： 失去焦点

**input.onchange = func;** ：失去焦点 且 内容发生改变 才触发

**input.oninput = func;**  ：内容发生改变 即 触发，H5方法（IE8不兼容）



**input.focus()** ： 通过js方法 获得焦点

**input.blur()**  ： 通过js方法 失去焦点



#### 键盘键值 ####

**ele.onkeydown** ： 键按下，长按触发多次

**ele.onkeyup**   ： 键抬起

**ele.onkeypress** ： 只响应非功能键及`Enter`按下，不兼容IE8

**e.keyCode** ： 键值

**e.charCode**  ：按下键的字符的ASCII编码（keypress事件）不兼容IE8。【DOM3级不再有此值，而是 key、char(非字符为null)，有跨浏览器问题】



#### 鼠标键值 ####

**e.which** 获取 onkeydown / onmousedown 键值 鼠标左键 1 、中键 2 、右键 3 （不兼容IE8）

**e.button** 左键 0 ，中键 1 ， 右键 2（不兼容IE8）



#### 组合键 ####

e.altKey

e.ctrlKey

e.shiftKey



#### 操作表格 ####

操作表格 | 描述

-|-

**insertRow(n)**  |插入一行 tr

**insertCell(n)** |插入一单元格 td

**deleteRow(n)**  |删除一行 tr

**deleteCell(n)** |删除一单元格 td

**rows**   |保存行的 HTMLCollection

**cell**   |保存`<tr>`中单元格的 HTMLCollection `tbody.rows[0].cell[0]`

-|-

tBodies |是一个`<tbody>`元素的HTMLCollection

tHead / tFoot  |保存着对`<thead>`/`<tfoot>`元素的指针

createTHead / createTHead  |创建`<thead>`/`<tfoot>`元素，将其放到表格中，返回引用

deleteTHead / deleteTFoot  |删除`<thead>`/`<tfoot>`元素





**HTMLCollection** 是一个接口，表示 HTML 元素的集合，它提供了可以遍历列表的方法和属性；如果基本的文档改变时，那些改变通过所有 HTMLCollection 对象会立即显示出来。



```javascript

var table = document.getElementsByTagName("table")[0],

    tbody = document.createElement("tbody");

table.appendChild(tbody);

tbody.insertRow(0);  //在tbody插入第一行

tbody.rows[0].insertCell(0);  //在第一个 tr 新增第一个 td

tbody.rows[0].cells[0].appendChild(document.createTextNode("Cell 1,1"));  //第一行第一格新增文本节点

tbody.rows[0].insertCell(1);  //在第一个 tr 新增第二个 td

tbody.rows[0].cells[1].appendChild(document.createTextNode("Cell 1,2"));  //第一行第二格新增文本节点

```

...

【JS高级程序设计-P283】







-----------------------------------------------------



## 31-32课 ##

### 飞机大战 ###

- 判断元素是否呈现在页面

  判断是否有父级 ：ele.parentNode



- 移除元素时先移除该元素的事件&&定时器



- 判断元素的碰撞

```js
    //检测碰撞
    function isCollide(obj1, obj2) {
        var L1 = obj1.offsetLeft,
            R1 = L1 + obj1.width,
            T1 = obj1.offsetTop,
            B1 = T1 + obj1.height;
        var L2 = obj2.offsetLeft,
            R2 = L2 + obj2.width,
            T2 = obj2.offsetTop,
            B2 = T2 + obj2.height;
        return !(L1>R2 || R1<L2 || T1>B2 || B1<T2)
    }
```



-----------------------------------------------------



## 33课 ##

### 正则表达式 ###

regular Expression

**new RegExp() 对象**

对象属性

- global：是否全文搜索，默认false。只读

- ignore case：是否大小写敏感，默认是false。只读

- multiline：多行搜索，默认值是false。只读

- lastIndex：是当前表达式匹配内容的最后一个字符的下一个位置

- source：正则表达式的文本内容




#### 写法 ####

var reg = //;  字面量

var reg = new RegExp();  实例化



#### 方法 ####

- **reg.test(str)**    ：reg匹配str，成功返回true，失败返回false

  ```js
  // 在全局匹配下受 reg.lastIndex 影响，结果会不一样
  // reg.lastIndex 属性可读可写
  ```

  ​

- **reg.exec(str)** 

  - 使用正则表达式模式对字符串执行搜索，并将更新全局RegExp对象的属性以反映匹配结果

  - 如果没有匹配的文本则返回null，否则返回一个结果数组

  - `index` 声明匹配文本的第一个字符位置

  - `input` 存放被检索的字符串 `string`

    - 非全局调用

      ```
      - 调用非全局的RegExp对象的exec()时，返回数组
      - 第一个元素是与正则表达式相匹配的文本
      - 第二个元素是与RegExpObject的第一个子表达式相匹配的文本（如果有）
      - 第三个元素是与RegExpObject的第一个子表达式相匹配的文本（如果有）
      ```

    - 全局调用

      ```js
      //找出相匹配的起始位置和结束位置
      var reg = /(\w)(\d)/g;
      var str = "a1b2c3d4e5f6";
      var ret;
      while( ret = reg.exec(str) ){
        console.log(ret.index, reg.lastIndex, ret)
        //匹配的起始位置，结束位置，匹配结果数组[相匹配文本,子集1,子集2,...]
      }
      ```

  ​



- **str.match(reg)**  ：返回一个数组，

    - 非全局
       包含着匹配内容的类数组，如果匹配不成功返回null。
       属性 index：返回匹配到的下标
       属性 input：返回匹配的目标字符串

    - 全局
        在加了标识 g 的时候，只返回数组，没有属性。



- **str.replace(reg, 替换文本)**    ：返回 新的字符串，把匹配成功的部分替换

  ```js
  str.replace(reg, "替换文本")
  str.replace(reg, function(i,j,k){})
  str.replace(reg, "$1 $2")  //$1 $2 $3 ：代表子集1 2 3
  /*
  *	function有四个参数，
  *	1、要匹配的字符串 
  *	2、正则表达式分组内容，没有分组则没有该参数 
  *	3、匹配项在字符串中的index 
  *	4、原字符串
  */
  ```



- **str.search(reg)**    ：返回正则第一次出现的位置，匹配失败返回-1（indexOf）



- **str.split(reg)**    ：切割字符串，返回数组




#### 标识符 ####

g ：全局匹配  global

i ：不区分大小写  ignore case

m ：换行匹配      multiline

```js
var reg = /abc/gim;
var reg = new RegExp("abc", "gim");
```



#### 元字符 \ ####

>当我们在匹配有特殊意义的字符时候，需要加 \ 符号转义
>
>\d ：数字
>
>\D ：非数字
>
>\w ：字符（数字，字母，下划线）
>
>\W ：非字符
>
>\s ：空格、tab
>
>\S ：非空格
>
>\b ：独立部分 单词边界，起始、结束、连词符（除了\w）、空格 `/\bwrod\b/`。只针对于字母和数字
>
>\B ：非独立部分 非单词边界
>
>
>
>\n ：换行
>
>\r ：换行
>
>\t ：tab符
>
>
>
>.    ：正则里代表除了 \n  \r  的任意字符
>
>^    ：在字符集之外，代表起始位置
>
>$    ：代表结束位置





#### 量词 {} ####

>/a{5}/    ：匹配5个连续的a
>
>/a{1,5}/ ：范围 1 <= n <= 5
>
>/a{2,}/  :范围 2 <= n <= 无限
>
>
>
>特殊的量词，可以用特定的符号表示
>
>{0,1} ： ?
>
>{1,} 	 ： +
>
>{0,} 	 ： *
>
>
>
>贪婪匹配  ：以最多次匹配
>
>惰性    ：给任意量词后加 ? 变成惰性匹配，尽量往少的匹配  `/a+?/` `/a{2,}?/`





#### 子集 () ####

> 圆括号里的字符代表一个整体
>
> var reg = /ab(12)/;  匹配 ab12，12
>
> /(ab)+/  匹配括号里的整体，且出现次数大于1
>
> /(\w)\1+/g	必须搭配子集  \1 代表子集1  （重复匹配子集1的内容）
>
> 
>
> \$1 \$2 \$3 ：代表子集1 2 3
>
> /(?:a)(b)/ ： `?:`代表不捕获，$1就代表了`(b)`
>
> 
>
> /exp(?=assert)/  ：正向前瞻，括号里代表断言
>
> /exo(?!assert)/  ：负向前瞻，括号里代表断言



#### 字符集 [] ####

> 方括号里的所有字符都是或者关系
>
> /[2-8]/  ：一段范围的内容 2~8,。 [0-9]、 [a-z]、 [A-Z]、 [\u4e00-\u9fa5]汉字集
>
> /[ab]/  ：匹配 a 或 b
>
> /[ab]c/  ：局部匹配 ac 或 bc。等同于 /(a|b)c/
>
> /\[^ab]/  ：取反，匹配除了 a 或 b 以外的，^要出现在字符集开头才有意义
>
> /a|b/     ：|	或者



### 表单验证

```js
var reg = {
        user : /^[a-zA-Z]\w{5,17}$/,
        pwd : /^[\w`~!@#$%^&*()_+=,.[\]{}|\\/]{6,18}$/,
        tel : /^1[3-8]\d{9}$/,
        qq : /^[1-9]\d{4,9}$/,
        idcard : /^[1-9]\d{16}[\dX]$/,
        email : /^[a-zA-Z]\w+@[\da-zA-Z]+(\.[0-9a-zA-Z\u4e00-\u9fa5]+){1,2}$/
    };

```



### 取小数的四舍五入

```js
/*
*   Number.toFixed(int)
*       保留int位小数
*       但此方法不是使用四舍五入，而是银行家的规则，四舍六入
*       例如： 1.555.toFixed(2)  ==>  输出 1.55 而不是1.56
*/

/*
*   需要标准四舍五入保留n位小数
*       function fn(num, int){
*           return Math.round(num*Math.pow(10, int))*Math.pow(10, -int);
*       }
*          console.log( fn(1.555, 2) );  // 1.56
*          
*       [ pow() 方法可返回 x 的 y 次幂的值。]
*/

// 覆盖默认 toFixed方法
Number.prototype.toFixed = function (n) {
    return Math.round(this*Math.pow(10, n))*Math.pow(10, -n);
}
console.log( 1.555.toFixed(2) );  // 1.56
```



-----

## 36课

### Cookie

存储数据大小上限是 4kb



**设置cookie**

```js
1.	存储cookie
document.cookie = '数据名=值';
一次只能存储一个，并且默认是临时存储，当关闭浏览器之后就被清除了。

2.	改变存储时间
var date = new Date(new Date().getTime() + n*24*60*60*1000).toUTCString(); //n天数
document.cookie = '数据名=值; expires=过期时间' + date;  //expires=时间戳

3.	获取cookie
当当前网页有cookie时，可以直接通过document.cookie 来找出所有cookie
consol.log( document.cookie );

4.  获取coolie值
document.cookie.match(/\bid=([^;]+)(;|$)/)[1]  //id属性
```



**封装cookie**

```js
/**
 * 获取cookie
 * @param key 属性
 * @returns {string}
 */
var getCookie = function (key) {
    var val = document.cookie.match(new RegExp("/\\b"+key+"=([^;]+)(;|$)/"))[1];
    return val?val[1]:""
},
/**
 * 设置cookie
 * @param json 键值
 * @param time 过期时间,天数
 */
setCookie = function (json, time) {
    var date = new Date(Date.now() + time*24*60*60*1000).toUTCString();
    for (var key in json) {
        document.cookie = key+"="+json[key]+";expires="+date;
    }
},
/**
 * 删除cookie
 * @param key 属性
 */
removeCookie = function (key) {
    var json = {};
    json[key]="";
    setCookie(json, -1)
};

setCookie({suyoulun:"boy"},7)
removeCookie("suyoulun")
getCookie("suyoulun")
```





---

## 37课

### AJAX 

全称：Asynchronous Javascript And XML

**AJAX流程**

```js
//ajax的使用极其简单，只有4步：
1.创建ajax对象 	xhr = new XMLHttpRequest();
2.建立请求		xhr.open(type,url,boolean)	//type请求方式（Get or post） url(后台接口) bool(是否异步 true是异步，false则同步)
3.发送请求		xhr.send();
4.监听状态码    xhr.onreadystatechange=function(){}
5.响应内容		xhr.responseText
//结束
```



**创建XHR对象**

```js
//创建XHR对象
var xhr = new XMLHttpRequest();
var url = "http://www.baidu.com"; 
```



**GET**

> GET方式不需要设置请求头，数据是跟在URL?后面，send不需要数据

```js
xhr.open("GET", url + "?name=name&age=age", true);  //true异步  false同步
xhr.send();
```



**POST**

> post需要设置请求头（数据格式），发送的数据需要放到send里

```js
xhr.open("post" , url);
//设置请求头
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send(data);
```

**post请求头的几种常用数据格式**

1.`application/x-www-form-urlencoded`

```js
#浏览器的原生 form 表单，如果不设置 enctype属性，那么最终就会默认以 application/x-www-form-urlencoded 方式提交数据。

在POST提交数据中Content-Type 被指定为 application/x-www-form-urlencoded；提交的数据按照 key1=val1&key2=val2 的方式进行编码，key 和 val 都进行了 URL 转码。大部分服务端语言都对这种方式有很好的支持。很多时候，我们用 Ajax 提交数据时，也是使用这种方式。
```

2.`multipart/form-data`

```js
#这也是一个常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 form 的 enctype 等于这个值。
这种方式一般用来上传文件，各大服务端语言对它也有着良好的支持。上面提到的这两种 POST 数据的方式，都是浏览器原生支持的。
```

3.`application/json`

```js
#用来告诉服务端消息主体是序列化后的 JSON 字符串。
由于 JSON 规范的流行，除了低版本 IE 之外的各大浏览器都原生支持 JSON.stringify，服务端语言也都有处理 JSON 的函数，使用 JSON 不会遇上什么麻烦。
```

4.`text/xml`

```js
#它是一种使用 HTTP 作为传输协议，XML 作为编码方式的远程调用规范
它的使用也很广泛，能很好的支持已有的 XML-RPC 服务。不过，XML 结构还是过于臃肿，一般场景用 JSON 会更灵活方便。
```



**请求状态码**

> xhr.readyState

0  请求未初始化，open还没有调用
1  请求正在发送，服务器连接已建立，open已
2  请求已接收，也就是接收到头信息了send
3  请求处理中，也就是接收到响应主体了
4  请求已完成，且响应已就绪，也就是响应完成了



**HTTP状态码**

> xhr.status

1xx	 信息类，表示收到Web浏览器请求，正在进一步的处理中
2xx	 成功，表示用户请求被正确接收，理解和处理 如：200 OK
3xx	 重定向，表示请求没有成功，客户必须采取进一步的动作
4xx	 客户端错误，表示客户端提交的请求有错误，如：404 NOT Found，表示请求中所引用的文档不存在
5xx	 服务器错误，表示服务器不能完成请求的处理



**响应的数据**

> xhr.responseText	（文本）
>
> xhr.responseXML （XML文档）



**转换json格式**

```js
var json = eval(data);
var json = JSON.parse(data);  //字符串转换成json格式，必须用双引号
var str = JSON.stringify(json);  //json格式转换成字符串，不兼容IE7，可引入 [json2.js] 文件解决
```



#### AJAX封装

```js
function ajax(json) {
    var xhr = new XMLHttpRequest(),
        type = json.type||"GET",
        url = json.url,
        async = json.async!==false,
        data = json.data,
        success = json.success,
        error = json.error;

    if (data) {
        data = function () {
            var str = "";
            for (var key in data) {str += key + "=" + data[key] + "&"}
            return str
        }()
    }

    if (/get/i.test(type)) url+="?"+(data||"")+"_="+Date.now();

    xhr.open(type, url, async)
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded")
    xhr.send(data||null)

    xhr.onreadystatechange = function () {
        if (this.readyState===4) {
            if (/(^2\d{2}|304)/.test(this.status)) {
                success(this.responseText)
            } else {
                error(this.status)
            }
        }
    }
}
```





**Fetch**

*Fetch*被称为下一代Ajax技术,采用Promise方式来处理数据。是一种简洁明了的API，比XMLHttpRequest更加简单易用。



---

## 39课

### jsonp

JSONP(JSON with Padding)是[JSON](https://baike.baidu.com/item/JSON)的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。由于同源策略，一般来说位于 server1.example.com 的网页无法与不是 server1.example.com的服务器沟通，而 HTML 的<script> 元素是一个例外。利用 <script> 元素的这个开放策略，网页可以得到从其他来源动态产生的 JSON 资料，而这种使用模式就是所谓的 JSONP。用 JSONP 抓到的资料并不是 JSON，而是任意的JavaScript，用 JavaScript 直译器执行而不是用 JSON 解析器解析。

比如，我们要访问服务器上的数据，在本地创建 <script>标签 scr属性引用服务器的地址并传入要获取的数据和callback函数名。服务器返回这个函数名加括号，相当于我们引入的<script>执行了一个函数，而函数的实参就等于我们需要访问到的数据。在这个时候，我们本地需要创建一个callback函数来接收这个参数，而本地函数就可以把访问到的数据作处理。

```html
<script>
    // 利用jsonp从百度上访问到搜索结果
    var key = "关键词";    //要搜索的关键词
    var cb = "callback";  //回调函数名
	var script = document.createElement("script");  //创建script标签
    script.src = "https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd="+key+"&cb="+cb;
    document.body.appendChild(script);  //添加到body，执行里面的函数 callback(数据)
    script.onload = function(){ document.body.removeChild(script) }  //加载完成移除自己
    
    //在本地定义callback函数
    function callback(json){
       //json就是访问到的数据，此时可以对json作处理
    }
</script>
```





-----

## 40课  ##

### 包装对象

包装对象类型（值类型）： boolean  number  str

包装对象：字面量定义的原始类型的对象，临时创建了一个对象，这个对象就叫包装（包装对象），包装对象使用完，就被销毁

1. 字面量创建的对象，原理是js在内部隐式调用对应构造函数生成的对象，如果是有js机制隐式的调用了构造函数创建的原始类型的对象，那么创建完成后，会把对象干掉。
2. 如果人为显示的调用构造函数生成原始类型的对象，那么不会把对象干掉（可以进行属性的写入和读取）

```js
//字面量创建方式
var str1 = "abcd";
alert(typeof str1)  // String
str1.attr = 1;      // js会隐式的把基本类型尝试以对象的方式去执行，基本类型会转换成临时的本身的包装类型对象，这个临时对象创建完即销毁
alert(str1.attr);   // undefined

//new创建方式
var str2 = new String("abcd");
alert(typeof str2)  // Object
str2.attr = 1;      // 人为显式的创建一个基本类型的对象，添加属性不会消失
alert(str2.attr)    // 1

/*
str是string(基本类型)，本身是没有方法的。

只要是引用了字符串的属性和方法，JavaScript就会将字符串值通过new String(s)的方式转为内置对象String，一旦引用结束，这个对象就会销毁。

当尝试把基本类型的str当做对象一样访问时，例如：str.length; 

解释器会创建一个临时的包装对象，伪代码：

[[tempObj]] = new String(str);

[[tempObj]].length; // 返回具体的length;

delete [[tempObj]]; // 销毁临时对象


重复访问str.length会重复创建这个临时对象。

所以str.t赋值可以成功，但再次访问str.t返回undefined，因为每次创建的临时包装对象都是不同的。
*/
```

console.dir（）打印对象的属性



### 面向对象 OOP

**构造函数**

```js
function Fun(){
  //构造函数内默认创建一个对象，然后返回这个对象
  //里面的this指向这个对象
}
var obj = new Fun();
```



**原型、原型链**

```js
constructor ：属性返回对创建此对象的数组函数的引用
__proto__	：该对象对应的构造函数的原型，浏览器创造的
prototype	：该对象的原型
```



**获取该对象继承的原型**

```js
obj.__proto__
Object.getPrototypeOf(obj)
```



**私有属性与公共属性**

```js
function Fn(){
  //对象私有属性
  this.x = 1;
  this.y = 2;
}

Fn.prototype = {
  //原型公有属性
  z : 3,
  show : function(){ alert(this.x) }
};

var foo = new Fn(); // 实例化

console.log(foo.x, foo.y, foo.z); // ==> 1 2 3 实例的私有属性
foo.show();  // ==> 1  原型链上的公共属性
```



**构造函数继承**

- Child.prototype = new Parent();  ==>  子类原型继承父类的实例化
- Parent.call(this, [].slice.call(arguments));  ==>  父类执行把**this指向**子类函数里的对象

```js
//父类
function Parent(){
  this.x = 1;
}
Parent.prototype = {
  constructor : Parent,
  y : 1,
  show : function (){}
}

//子类
function Child(){
  Parent.call(this, [].slice.call(arguments)); //使父类指向当前对象，不定参转成数组
}

//实例化父类给子类原型
Child.prototype = new Parent();

//不能再使用 Child.prototype = {}; 覆盖子类原型，只能以下方法添加子类属性
Child.prototype.constructor = Child;
Child.prototype.z = function(){ alert(this.x, this.y) };

//子类实例化
var oneChild = new Child();
oneChild.z()
```



**Object.create()** 方法会使用指定的原型对象及其属性去创建一个新的对象。

```js
//语法
Object.create(proto[, propertiesObject])

//参数
- proto
  新创建对象的原型对象。
- propertiesObject
  可选。如果没有指定为 undefined，则是要添加到新创建对象的可枚举属性（即其自身定义的属性，而不是其原型链上的枚举属性）对象的属性描述符以及相应的属性名称。这些属性对应Object.defineProperties()的第二个参数。

//返回值
在指定原型对象上添加新属性后的对象。
```



**原型继承**

```js
//父类
function Parent(){
  this.x = 1;
}
Parent.prototype = {
  constructor : Parent,
  y : 1,
  show : function (){}
}

//子类
function Child(){
  Parent.call(this, [].slice.call(arguments)); //继承父类的私有属性
  this.h = 172;  //子类的原型扩展
}

//继承父类的原型
	//方法1--新对象
	Child.prototype = Object.create( Parent.prototype ); //IE8不兼容
	//方法2--新对象 IE8
	function F(){}
  F.prototype = Parent.prototype;
  Child.prototype = new F();
	//方法3--浅复制
  for(var key in Parent.prototype){ 
    Child.prototype[key] = Parent.prototype[key] 
  }
	//方法4--深复制 复制不了函数
	//Child.prototype = JSON.parse(JSON.stringify(Parent.prototype));

//子类修正constructor指向
Child.prototype.constructor = Child;

//子类的原型扩展
Child.prototype.z = function(){ alert(this.x, this.y) };

//子类的实例化
var a = new Child();
a.z();
```



**instanceof**

判断该对象是否后面类(对象)的实例，它**并不代表两者的继承**。

`instanceof` 运算符用来检测 `constructor.prototype` 是否存在于参数 `object `的原型链上

```js
子类.prototype instanceof 父类  //true
子类 instanceof 父类            //false
子类实例 instanceof 子类        //true
子类实例 instanceof 父类        //true
```

`isPrototypeOf()`判断原型对象

```js
Parent.prototype.isPrototypeOf(oChild)
```



**判断对象自身属性**

- `hasOwnProperty()`函数用于指示一个对象自身(不包括原型链)是否具有指定名称的属性。如果有，返回`true`，否则返回`false`。

  ```js
  oChild.hasOwnProperty("name")
  ```

  该方法属于`Object`对象，由于所有的对象都"继承"了Object的对象实例，因此几乎所有的实例对象都可以使用该方法。

- `in`操作符：单独使用时，in操作符会在通过对象能够访问给定属性时返回true，无论该属性存在于实例还是原型中。

  ```js
  alert("name" in oChild)  //返回布尔值
  ```

- `hasPrototypeProperty()`








------

[**js 原型的问题 Object 和 Function 到底是什么关系？**](https://segmentfault.com/q/1010000002736664)

1. 首先`Object`和`Function`都是构造函数，而所有的构造函数的都是`Function`的实例对象. 因此`Object`是`Function`的实例对象

2. `Function.prototype`是`Object`的实例对象

3. 实例对象的原型(我们以`__proto__`来表示)会指向其构造函数的prototype属性, 因此 

   ```js
   Object.__proto__ === Function.prototype 
   Function.__proto__ === Function.prototype 
   Function.prototype.__proto__ === Object.prototype
   ```

4. 当我们访问一个属性值的时候, 它会沿着原型链向上查找, 直到找到或者到Object.prototype.__proto__(为null)截止.

   假如我们有以下例子:

```js
var foo = {},
F = function(){};

Object.prototype.a = 'value a';
Function.prototype.b = 'value b';

console.log(foo.a)    // value a
console.log(foo.b)    // undefined
console.log(F.a)      // value a
console.log(F.b)      // value b
```

​	那么

```js
/*
*   foo.a的查找路径: foo自身: 没有 
		---> foo.__proto__(Object.prototype): 找到value a
        
*   foo.b的查找路径: foo自身: 没有 
		---> foo.__proto__(Object.prototype): 没有 
		---> foo.__proto__.__proto__ (Object.prototype.__proto__): 没有

*   F.a的查找路径: F自身: 没有 
		---> F.__proto__(Function.prototype): 没有 
		---> F.__proto__.__proto__(Object.prototype): 找到value a
        
*   F.b的查找路径: F自身: 没有 
		---> F.__proto__(Function.prototype): 找到value b
*/
```

5. 关于instanceof的结果不要仅从字面上理解, 它的计算规则是: 如果右侧构造函数的prototype属性能在左侧的对象的原型链中找到, 那么就返回true, 否则就返回false

   ```js
   Object instanceof Function:  Object.__proto__ === Function.prototype, 结果为true
   Function instanceof Object:  Function.__proto__.__proto__ === Object.prototype, 结果也为true

   Object.__proto__ === Function.__proto__   结果为true
   ```


6. 实例对象的constructor属性指向其构造函数, 因此

   ```js
   Object.constructor === Function       // true
   Function.constructor === Function     // true
   ```

   **所以，`Object`是`Function`的实例对象, `Function.prototype`是`Object`的实例对象。**








**clone一个对象**

```js
//深克隆一个对象 递归
function deepClone(obj) {
  	// 判断obj是否为对象
  	if (!obj instanceof Object) return obj
    // 判断obj的引用数据类型
    var t;
    if (obj instanceof Array) {
        t = []
    } else {
        t = {}
    }
    // 循环拷贝
    for (var i in obj) {
        // 判断子层级的数据类型 
        if ( obj[i] && /object/i.test(typeof obj[i]) ) {
            t[i] = deepClone(obj[i])
        } else {
            t[i] = obj[i]
        }
    }

    return t
}
```

```js
// 深复制 递归
function deepClone(obj){
    let objClone = Array.isArray(obj)?[]:{};
    if(obj && typeof obj==="object"){
        for(key in obj){
          	// 判断obj是否有key属性
            if(obj.hasOwnProperty(key)){
                //判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key] && typeof obj[key] === "Object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}
```

```js
// 借用JSON对象的parse和stringify
function deepClone(obj){
  return JSON.parse( JSON.stringify(obj) )
}
```

```js
// 多克隆
function ployClone(target, obj) {
  for (var i=1; i<arguments.length; i++) {
    for (key in arguments[i]) {
      if ( /object/i.test(arguments[i][key]) ) {
        ployCloen( target[key], arguments[i][key] )
      } else {
        target[key] = arguments[i][key]
      }
    }
  }
}
// function ployClone(target, obj) {
//   for (var i=1; i<arguments.length; i++) {
//     for (key in arguments[i]) {
//       if ( /object/i.test(arguments[i][key]) ) {
//         ployCloen( target[key], arguments[i][key] )
//       } else if ( Array.isArray(arguments[i][key]) ) {
//         if (!target[key]) target[key] = []
//         target[key] = target[key].concat( arguments[i][key] )
//       } else {
//         target[key] = arguments[i][key]
//       }
//     }
//   }
// }
```



**多继承**

```js
var a = {x:1, y:2};
var b = {x:2, z:3};

var c = Object.assign({},a,b);  //ES6方法
```

```js
//父类FN1
function FN1(){
  this.a = 1;
  this.b = {x:1,y:2};
  this.c = [1,2];
  this.d = function(){
    alert(this.a)
  }
}

FN1.prototype = {
  constructor: FN1,
  e: "hi"
}

//父类FN2
function FN2(){
  this.f = "hello";
}

FN2.prototype = {
  constructor: FN2,
  g: "Myname",
  h: function(){
    alert(this.g)
  }
}

//子类Fn3
function Fn3(){
  FN1.call(this);
  FN2.call(this);
}

//子类多继承
Fn3.prototype = Object.assign({},FN1.prototype,FN2.prototype)
Fn3.prototype.constructor = Fn3;

var a = new Fn3();

console.log(Fn3.prototype)
console.log(a)
```



**多态**





**链式结构**







## 移动端网址重定向

```js

```





