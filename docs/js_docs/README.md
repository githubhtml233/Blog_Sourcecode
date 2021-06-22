---
sidebar: auto
---

## GET与POST的区别

- GET请求参数存在长度限制，POST无限制
- GET产生一个TCP数据包，POST产生两个
- GET请求的内容暴露在地址栏中，POST的请求内容包含在Request Body中
- GET的请求内容会被浏览器主动缓存
- POST比GET更安全
- GET回退无风险，POST会重新提交请求
- 
## 闭包

**定义：** 指有权访问另一函数作用域中变量的函数

**作用：** 
- 常用来定义模块，将操作函数暴露给外部，细隐藏在模块内部
- 创建私有变量
- 保留某些停止执行的上下文变量

```js
function module() {
	var arr = [];
	function add(val) {
		if (typeof val == 'number') {
			arr.push(val);
		}
	}
	function get(index) {
		if (index < arr.length) {
			return arr[index]
		} else {
			return null;
		}
	}
	return {
		add: add,
		get: get
	}
}
var mod1 = module();
mod1.add(1);
mod1.add(2);
mod1.add('xxx');
console.log(mod1.get(2));
```
## 对象与类
**什么是对象**
对象可以被看作一组没有特定顺序的值。
在对象中，属性可分为数据属性和访问器属性，且都有一些内部特性描述属性的特征。这种内部特征用[\[Property]]标识，其中Property表示不同的标识。

**继承**

***1、原型链***

将父类的实例作为子类的原型
```js
function SuperType() {
	this.property = true;
}
SuperType.prototype.getSuperValue = function() {
	return this.property;
}
function SubType() {
	this.subproperty = false;
}
//继承SuperType
SubType.prototype = new SuperType();
SubType.getSubValue = function() {
	return this.subproperty;
}
let instance = new SubType();
console.log(instance.getSuperValue()) //true
```
优点：实现简单
缺点：
- 原型中包含的引用值会在所有实例中共享
- 子类型在实例化时不能给父类型的构造函数传参

***2、盗用构造函数***

在子类构造函数中调用父类构造函数
```js
funciton SuperType() {
	this.colors = ["red", "blue", "green"];
}
function SubType() {
	SuperType.call(this);
}
let instance1 = new SubType();
instance.colors.push("black");
console.log(instance1.colors) //["red", "blue", "green", "black"]
let instance2 = new SuperType();
console.log(instance2.colors) //["red", "blue", "green"]
```
优点：
- 可以在子类构造函数中向父类构造函数传参
```js
function SuperType(name) {
	this.name = name;
}
function SubType() {
	SuperType.call(this,"Yang");
	this.age = 24;
}
let instance = new SubType();
console.log(instance.name); //Yang
console.log(instance.age); //24
```
缺点：
- 必须在构造函数中定义方法，导致函数不能重用

***3、组合继承***

综合原型链和盗用构造函数，用原型链继承原型上的属性和方法，通过盗用函数继承实例属性。是JS中使用最多的继承模式。
```js
function SuperType() {
	this.name = "Yang";
	this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function() {
	console.log(this.name);
}
function SubType(name, age) {
	//继承属性
	SuperType.call(this, name);
	this.age = 24;
}
//继承方法
SubType.prototype = new SuperType();
SubType.prototype.sayAge = function() {
	console.log(this.age);
}
let instance1 = new Subtype("Yang", "24");
instance1.colors.push("black");
console.log(instace1.colors) //["red", "blue", "green", "black"]
instance1.sayName(); //Yang
instance1.sayAge(); //24

let instance2 = new Subtype("Xiong", "29");
console.log(instance2.colors);
instance2.sayName(); //Xiong
instance2.sayAge(); //29
```
缺点：两次调用父类构造函数

***4、寄生式继承***

创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。
适合主要关注对象，而不在乎类型和构造函数的场景。
```js
function createAnother(original) {
	let clone = object(original); //通过调用函数创建一个新对象
	clone.sayHi = function() { //以某种方式增强对象
		console.log("hi");
	}
	return clone; //返回对象
}
let person = {
	name: "Yang",
	frend:["Zhou", "Wu", "Zheng", "Wang"]
};
let anotherPerson = creatAnother(person);
anotherPerson.sayHi(); //"hi"
```

***5、寄生式组合继承***

由于组合继承存在效率问题：父类构造函数始终会被调用两次,因此提出寄生式组合继承：通过调用父类构造函数继承属性，使用混合式原型链继承方法，即使用寄生式继承父类原型。
```js
function inheritPrototype(subType, superType) {
	let prototype = object(superType.prototype); //创建父类原型副本
	prototype.constructor = subType; //增强对象
	subType.prototype = prototype; //赋值对象
}
function SuperType(name) {
	this.name = name;
	thih.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayNme = function() {
	console.log(this.name);
}
function SubType(name, age) {
	SuperType.call(this, name);
	this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function() {
	console.log(this.age);
}
```
只调用一次SuperType构造函数，是引用类型继承的最佳模式。


**类定义**
- 类声明
  ```js
  class Person {}
  ```
- 类表达式
  ```js
  const Animal = class {};
  ```

**类的实例化**

使用new调用类的构造函数进行实例化。其具体执行过程如下。
- 在内存中创建一个新对象。
- 这个新对象内部的[\[prototype]]指针被赋值为构造函数的prototype属性
- 构造函数的this被赋值为新对象
- 执行构造函数操作
- 如果构造函数返回非空对象，则返回该对象，否则返回创建的新对象。

## 作用域与作用域链
作用域：定义变量的区域，有一套访问变量的规则
作用域链：指向变量对象的指针列表，能让我们访问外部环境的变量和函数。
## this、call、apply和bind
- 全局范围内，this指向window
- 函数中，this指向最后调用它的对象
- 构造函数中，this指向创建的新对象
- call、apply和bind强行改变this指向
- 箭头函数中，this指向为离它最近的父作用域this