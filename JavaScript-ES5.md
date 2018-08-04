# ESMAScritp5



## 前言

javascript诞生于1995年5月。
javascript之父 Brendan Eich 10天  完成任务的心态。

最初是叫 LiveScript（活力脚本） 傍大牌  营销手段  

javascript与java没有一毛钱关系。  北大和北大青鸟   ，  雷锋和雷峰塔；

几个月后，微软推出IE3  Jscript；

微软的哲学观：当别人火了以后，就要自己捣鼓一个差不多的东西出来，并且这个东西还不好使，过段时间就没人请学，这时候才想着回头来兼容别人的东西，并且还兼容不好。

javascript提交给了Ecma International（一个欧洲的标准化组织），在1997年这个组织就推出了EcmaScript的第一个版本

**ECMAScript是javascript语言的标准。**

2003年之前有一个外号：牛皮癣。  
2004年：google从js的内部发现了一个对象，ajax，用来进行异步操作；用来提示用户体验。
2008年，google推出chrome浏览器。搭载是google自行开发的V8引擎。
2009年，jquery是js的一个库，开始流行起来。
2010年，canvas画布这个技术，得到了很多浏览器的支持。
2011年，nodejs得到广泛的运用。
2015年，ECMAScript的第6个版本发布。ES2015

JavaScript基于原型的动态解释性脚本语言



#### 前端三层

- 结构层：html标签
- 表现层：css
- 行为层：js




## 字符











## 数组



## 函数



## 运算符



### 逻辑运算符

在JavaScript中的逻辑运算符： `+` `-` `*` `/` `%`





#### +号运算符

```js
当 加号 两边都是数字的时候，这时加号是数学意义上的加号运算符。
当 加号 两边有其中一边是字符串的时候，就是拼接。
注意：被引号引起来的东西，不管是啥，都叫字符串。
```



### 位运算符



# DOM



#### 弹窗

```js
// 弹出一个消息框，确定按钮
alert( 1 )

// 弹出一个消息框，确定/取消按钮，返回 true/false
var bool = confirm( 1 )

// 弹出一个消息框，确定/取消按钮和对话框，返回 对话框内容
var str = prompt( '在对话框里输入内容' )
```





#### 元素





#### 元素内容

`innerHTML`与 `innerText`的区别在与前者会尝试解析成元素，后者不会解析

**innerHTML**

```js
var e = document.body.innerHTML		// 获取 html 内容
document.body.innerHTML = '<div></div>'		// 解析成 html 标签
```

**innerText**

```js
var e = document.body.innerText		
document.body.innerText = '<p>文本内容</p>'
```







# BOM







# 正则表达式



