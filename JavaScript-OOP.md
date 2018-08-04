# 原型链



# 继承



JavaScript 主要通过原型链实现继承。原型链的构建是通过将一个类型的实例赋值给另一个函数的构造原型实现的。





## 原型继承

缺点：由于原型中包含引用类型值所带来的问题

```js
// 父类
function SuperType() {
  this.property = true;
}

// 父类方法
SuperType.prototype.getSuperValue = function () {
  return this.property;
}

// 子类
function SubType() {
  this.subproperty = false;
}

// 继承
SubType.prototype = new SuperType()
// 修正指向
SubType.prototype.constructor = SubType

// 子类方法
SubType.prototype.getSubValue = function () {
  return this.subproperty
}

// 子类实例化
var instance = new SubType()
alert( instance.getSuperValue() )    // true
```





## 借用构造函数

缺点：无法避免构造函数模式存在的问题，

```js
function SuperType() {
  this.colors = ["red", "blue", "green"]
}

function SubType() {
  // 继承，call使父类的this指向当前子类
  SuperType.call(this)
}

var instance1 = new SubType();
instance1.colors.push("black")
alert( instance1.colors )    // "red", "blue", "green", "black"

var instance2 = new SuperType();
allert( instance2.colors )    // "red", "blue", "green"
```





## 组合继承



```js
function SuperType(name) {
  this.name = name
  this.colors = ["red", "blue", "green"]
}

SuperType.prototype.sayName = function () {
  alert( this.name )
}

function SubType(name, age) {
  this.age = age
  // 继承属性
  SuperType.call(this, name)
}

// 继承方法
SubType.prototype = new SuperType()
SubType.prototype.constructor = SubType
SubType.prototype.sayAge = function () {
  alert( this.age )
}
```





## 原型式继承

创建一个过渡函数，其原型 浅复制 一个对象，然后实例化



```js
// 创建一个过渡函数
// 而这个过渡函数的{原型}对 obj 执行了一次{浅复制}

// 原型式继承
function inheritObject(obj) {
  // 过渡函数
  function F() {}
  // 过渡函数的原型继承父对象
  F.prototype = obj
  // 返回过渡函数的实例，该实例的原型继承了父对象
  return new F()
}

// 定义一个对象
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
}

var anotherPerson = inheritObject(person)
anotherPerson.name = "Greg"
anotherPerson.friends.push("Rob")

var yetAnotherPerson = inheritObject(person)
yetAnotherPerson.name = "Linda"
yetAnotherPerson.friends.push("Barbie")

alert(person.friends)    // "Shelby", "Court", "Van", "Rob", "Linda"
```



**Object.create()**

ES5通过新增 `Object.create()` 方法规范化了原型式继承。接收两个参数：一个用作新对象原型的对象和（可选）一个为新对象定义额外属性的对象。在传入一个参数的情况下， `Object.create()` 与 `inheritObject()` 方法的行为相同。

- 一个参数

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
}

var anotherPerson = Object.create(person)    // <-
anotherPerson.name = "Greg"
anotherPerson.friends.push("Rob")

var yetAnotherPerson = Object.create(person)    // <-
yetAnotherPerson.name = "Linda"
yetAnotherPerson.friends.push("Barbie")

alert(person.friends)    // "Shelby", "Court", "Van", "Rob", "Linda"
```

- 两个参数

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
}

var anotherPerson = Object.create(person, {
  name: { value: "Greg" }
})

alert( anotherPerson.name )    // "Greg"
```



## 寄生式继承

沿用了原型式继承的一种思路

缺点：函数复用效率低，与构造函数模式类似。

```js
// 接收一个作为新对象基础的对象
function createAnother(original) {
  var clone = obj(original)
  clonel.sayHi = function () {
    alert("Hi")
  }
  return clone
}
```

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
}

var anotherPerson = createAnother(person)
alert( anotherPerson.sayHi() )    // "Hi"
```





## 寄生组合式继承

所谓寄生组合继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。基本思路：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型原型的一个副本。本质上，就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型。

```js
function inheritPrototype(subType, superType) {
  // 创建对象
  var prototype = Object.create(superType.prototype)
  // 修正指向
  prototype.constructor = subType
  // 指定对象
  subType.prototype = prototype
}



function SuperType(name) {
  this.name = name
  this.colors = ["red", "blue", "green"]
}

SuperType.prototype.sayName = function () {
  alert( this.name )
}

function SubType(name, age) {
  SuperType.call(this, name)
  this.age = age
}

inheritPrototype(SubType, SuperType)

SubType.prototype.sayAge = function () {
  alert( this.age )
}
```



```js
// 超类
function SuperType(name) {
  this.name = name
}
SuperType.prototype.sayName = function () {
  alert( this.name )
}

// 子类
function SubType(name, age) {
  // 继承属性
  SuperType.call(this, name)
  this.age = age
}
// 继承方法
function F() {}
F.prototype = SuperType.prototype
SubType.prototype = new F()
SubType.prototype.curtructor = SubType






// 实现继承超类方法
function inheritPrototype(subType, superType) {
  // 过渡函数
  function F(){}
  // 过渡函数的原型{浅拷贝}超类原型
  F.prototype = superType.prototype
  // 过渡原型
  var prototype = new F()
  // 修正指向
  prototype.constructor = subType
  // 把过渡原型赋值给子类原型
  subType.prototype = prototype
}
// inheritPrototype(SubType, SuperType)
```







