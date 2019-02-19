---
title: JS 学习笔记
date: 2019-01-15 16:14:28
tags: javascript
category: 前端
---

# web发展史
- mosaic是互联网历史上第一个获普遍使用和能后显示图片的网页浏览器，于1993年问世。
- 最初叫LiveScript
1. 浏览器的组成部分
shell部分
内核部分
渲染引擎（语法规则和渲染）
js引擎
其他
2. js引擎
2001年发布ie6， 首次实现对js引擎的优化和分离
2008年google发布最新浏览器chrome，它采用优化后的javascript引擎，代号v8，因能把js代码直接转化为机械码执行，进而以速度快而闻名
后Firefox也推出了具备强大功能的js引擎
Firefox3.5 TranceMonkey（对频繁执行的代码做了路径优化）
Firefox4.0 leagerMonkey

# 学习 JS
## JS 介绍
1. JS 的特性
解释性语言 --不需要编译成文件（跨平台）
单线程
ECMA标注  -- `ECMAScript`
2. JS 执行队列
js执行主线程
task,1ms <- task2,1ms <- task2,1ms <- task1,1ms ...
轮转时间片：类似吃饭
3. JS 的三大部分
JavaScript，dom，bom
4. 主流浏览器及其内核
ie                  trident
chrome         		webkit/blink
Firefox           	Gecko
opera             	presto
safar               webkit
5. 如何引入 .js
页面引用<script></script>
外部引用 <script src="index.js"></script>
-- 为符合web标准（w3c标准中的一项）结构、央视、行为相分离，通常采用外部引入
##  JS 基本语法
1. 变量
```
var	a,
	b,
	c,
	d,
	e; // 变量声明
a = 100; // 赋值
a = 200; // 覆盖
```
2. 命名规则
变量名必须以英文字母、\_、$开头
变量名可以包括英文字母、\_、$、数字
不可以用系统的关键字、保留字作为变量名
3. 值类型 -- 数据类型
不可改变的原始值   stack(栈数据)
Number, Boolean, String, undefied, null
引用值 heap(堆数据)
array，object，function 。。。 date RegExp
```
var arr1 = [1,2];
var arr2 = arr1;
arr1 = [2,3]
console.log(arr2);    // [1,2]
```
3. 基本语法
语句后面要用分号结束
js语法错误会引发后续代码终止，但不会影响其他js代码块
书写格式要规范， ”=+/-“两边都应该有空格
4. js 运算符
```
// "+" 1. 数学运算、字符串连接， 2. 任何数据类型加字符串都等于字符串
// "-" ，"*"，"/"，"%"，"="，"()"
// 优先级"=”最弱，“()“优先级较高
// "++"，"--"，"+="，"-="，"/="，"*="，"%="
console.log(1/0); // Infinity
console.log(0/0); //NaN
// 比较运算符： >，<， ==，>=，<=，!=    比较的结构为boolean值
// 逻辑预算符：&&，||，!    运算结果为真实的值
// 被认定为false的值：undefined,null,NaN,"",0,false
console.log(NaN == NaN);    // false
console.log(undefied == undefined); // true
console.log(0 && 2 + 2); // 0
console.log(1 && 2); // 2    先看第一个表达式转换成布尔值的结果，如果第一个结果为真，那么它会看第二个表达式的值返回
```
## 条件语句
```
if, if else if
if <--> && 转换
for
while, do while
```
## 条件语句补充
```
switch case
break;
continue;

```
## 初识引用值
1. 数组
2. 对象

## 编程形式的区别
1. 面向过程
2. 面向对象

## typeof
六种数据类型 number, string, boolean, undefined, object, function

## 类型转换
1. 显示类型转换
`Number(mix)`
`parseInt(string, radix)`
`parseFloat(string)`
`toString(radix)`
`String(mix)`
`Boolean()`
```
Number('123'); // number
Number('a'); // NaN
Number(undefined); // NaN
Number(null); // 0
parseInt(123.9); // 123
parseInt('10', 16); // 16
var num = 10;
num.toString(8); // 12
```
2. 隐形类型转换
`isNaN()`
`++` `/` `--` `+/`
`+`
`-` `*` `/` `%`
`&&` `||` `!`
`<` `>` `<=` `>=`
`==` `!=`
```
isNaN(123); // false
isNaN(NaN); // true
isNaN('abc'); // true
isNaN(undefined); // true
isNaN(null); // false
```
## 函数
1. 定义
函数声明
函数表达式
```
function test1() {
	console.log('hello world');
}
var test2 = function() {
	// ...
}
var test3 = function abc() { //  除了test3.name是abc，其他无区别
	// ...
}
function add(a, b) { // 形式参数  -- 形参
	console.log(arguments) // 实参列表
	return a + b;
}
add(1, 2); // 实际参数 -- 实参
```
2. 组成形式
函数名称
参数
-- 形参
-- 实参
-- 返回值
## 作用域
变量（变量作用域又称上下文）和函数生效（能被访问）的区域
全局、局部变量
作用域的访问顺序
```
var aaa = 123;
function test() {
	function b() {
		var bbb = 234;
		console.log(aaa)
	}
	return b;
}
var glob = 100;
var demo = a();
demo();
//
```
## 闭包
当内部函数被保存到外部时，将会生成闭包。闭包会导致原有作用域链不释放，造成内存泄漏。
1. 作用
实现公有变量，eg：函数累加器
可以做缓存（存储结构），eg：eater
可以实现封装，属性私有化。eg：Person()
模块化开发，防止污染全局变量
```
function add() {
	var count = 0;
	function demo() {
		count++;
		console.log(count);
	}
	return demo;
}
var counter = add();
counter();
counter();
counter();

function test() {
	var num = 100;
	function a() {
		num++;
		console.log(num);
	}
	function b() {
		num--;
		console.log(num);
	}
	return [a, b];
}
var arr = test();
arr[0]();
arr[1]();
```
2. 立即执行函数
此类函数没有声明，在一次执行过后释放。适合做初始化工作。
```
// (function() {}()); // w3c推荐使用
// (function() {})();
// 只有表达式才能被执行符号执行
// var test = function () {}();
// + - ! function test() {}();

function test() {
	var arr = [];
	for (var i = 0; i < 10; i++) {
		(function(j) {
			arr[j] = function() {
				console.log(j);
			}
		}(i))
	}
	return arr;
}
var myArr = test();
for (var j = 0; j < 10; j++) {
	myArr[j]();
}

// 针对初始化功能的函数
((function abc() {
	var a = 123;
	var b = 234;
	console.log(a + b);
})())
console.log(abc);  // 执行完立即销毁


a = 100;
function demo(e) {
	function e() {}
	arguments[0] = 2;
	console.log(e);
	if (a) {
		var b = 123;
		function c() {}
	}
	var c;
	a = 10;
	var a;
	console.log(b);
	f = 123;
	console.log(c)
	console.log(a)
}
var a;
demo(1);
console.log(a);
console.log(f);  // 2 undefined undefined 10 100 123

```
3. 防范
闭包会导致多个执行函数共有一个公有变量，如果不是特殊需要，应尽量防止这种情况发生
4.js 运行三部曲
语法分析
预编译
解释执行
```
// 函数声明整体提升
// 变量 声明提升
var a = 123;
function test() {
	// ...
}
```
5. 预编译前奏
imply global暗示全局变量：即任何变量，如果变量未经声明就赋值，此变量就称为全局变量所有。eg：a = 123;var a = b = 123;
一切声明的全局变量，全是window的属性。eg：var a = 123; --> window.a = 123
```
function test() {
	var a = b = 123;
}
test();  // window.a undefined, window.b 123;
```
6. 预编译四部曲
创建AO对象(Activation Obejct)(执行期上下文)
找形参和变量声明，将变量和形参名作为AO属性名，值为undefined
将实参值和形参统一
在函数体里面找函数声明，值赋予函数体
```
function fn(a) {
	console.log(a);         // function a() {}
	var a = 123;
	console.log(a);         // 123
	function a() {}
	console.log(a);         // 123
	var b = function() {}
	console.log(b);         // function () {}
	function d() {}
}
fn(1);

function test(a, b) {
	console.log(a);       // 1
	c = 0;
	var c;
	a = 3;
	b = 2;
	console.log(b);        // 2
	function b() {}
	function d() {}
	console.log(b);        // 2
}
test(1);

function test1(a, b) {
	console.log(a); // function() {}
	console.log(b); // undefined
	var b = 234;
	console.log(b); // 234
	a = 123;
	console.log(a); // 123
	function a() {}
	var a;
	b = 234;
	var b = function () {}
	console.log(a);  // 123
	console.log(b); // fn
}

global = 100;
function fn() {
	console.log(global);
	global = 200;
	console.log(global);
	var global = 300;
}
fn();
var global;   // undefined  200


function test() {
	console.log(b);
	if (a) {
		var b = 100;
	}
	console.log(b);
	c = 234;
	console.log(c);
}

var a;
test();
a = 10;
console.log(b);  // undefined undefined 234 234

function bar() {
	return foo;
	foo = 10;
	function foo() {

	}
	var foo = 11;
}
console.log(bar()) // function foo() {}

```
## 作用域精解
[[scope]]：每个js函数都是一个对象，对象中有些属性我们可以访问，但有些不可以，这些属性仅供js引擎存取，[[scope]]就是其中一个。[[scope]]指的就是我们所说的作用域，其中存储了运行期上下文的集合
作用域链：[[scope]]中所存储的执行期上下文对象的集合，这个集合呈链式链接，我们把这种链式链接叫做作用域链
运行期上下文：当函数执行时，会创建一个成为执行器上下文的内部对象。一个执行期上下文定义了一个函数执行时的环境，函数每次执行时对应的执行上下文都是独一无二的，所以多次调用一个函数会导致船桨多个执行上下文，当函数执行完毕，他所产生的执行上下文被销毁。
查找变量：从作用域链的顶端依次向下查找。
```
function a () {
	function b() {
		var b = 234;
	}
	var a = 123;
	b();
}
var glob = 100;
a();
// a defined a.[[scope]] --> 0 : GO {}
// a doing   a.[[scope]] --> 0 : GO {}
// 							1 : AO {}


function a() {
	function b() {
		var bbb = 234;
		console.log(aaa);
	}
	var aaa = 123;
	return b;
}

var glob = 100;
var demo = a();
demo();   // 123
```

## 对象
1. 描述心中的对象
2. 属性的增删改查
```
var mrWang = {
	name: 'wang steven',
	age: 30,
	sex: 'male',
	health: 100,
	smoke: function() {
		console.log('I am smoking! cool!');
		this.health --;
	},
	drink: function() {
		console.log('I am drinking!');
		this.health ++;
	}
}

mrWang.wife = 'missMa'; // 增
mrWang.sex = 'female'; // 改
delete mrWang.name; // 删
console.log(mrWang.age); // 查
```
3. 对象的创建方法
字面量
构造函数 --系统自带 new Object();Array();Number();Boolean();String();Date();
Object.create(原型)方法
```
var obj = {} // 对象字面量/对象直接量
var obj1 = new Object(); // 系统自带的构造函数创建对象
```
4. 构造函数内部原理
在函数体最前面隐式的加上`this = {}`
执行`this.xxx = xxx`
隐式的返回`this`
```
function Person(name, height) {
	// var this = {};
	this.name = name;
	this.height = height;
	this.say = function () {
		console.log(this.say);
	}
	// return this;
}
console.log(new Person('wang', 180).name);
```
5. 包装类
`new String();`
`new Boolean();`
`new Number();`
```
var num = new Number(123);
num.len = 4; // 包装类可以设置属性
var num1 = 234;
num.len = 3; // 字面量设置属性无效
var str = new String('abc');
var bool = new Boolean('true');

var str = "abc";
str += 1;
var test = typeof(str);
if (test.length == 6) {
	test.sign = 'typeof 返回的结果可能是string';
}
console.log(test.sign);
```
## 原型
1. 定义： 原型是function对象的一个属性，它定义了构造函数制作出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法。原型也是属性。
```
// Person.prototype = {}; 原型
Person.prototype.name = 'hehe';
function Person() {
}
var person = new Person();
var person1 = new Person();
```
2. 利用原型特点和概念，可以提取公共属性。
```
Person.prototype.name = 'hehe';
Person.prototype.say = function() {
	console.log('hehe');
}
function Person() {
	this.name = 'wang';
}
var person = new Person();
var person1 = new Person();

Person.prototype.say = function() {
	console.log('say');
}
function Person(name, age) {
	this.name = name;
	this.age = age;
}
var person = new Person('wang', 30);
```
3. 对象如何查看原型 --> 隐式属性 __proto__
```
function Person() {
	//var this = {
	//	  __proto__: Person
	//}
}
```
4. 对象如何查看对象的构造函数 --> constructor
```
function Person() {
}
Car.prototype = {
	constructor: Person.prototype
}
functio Car() {
}
var car = new Car();

Grand.prototype.lastName = 'wang';
function Grand() {}
var grand = new Grand();
Father.prototype = grand;
function Father() {
	this.name = 'xiaoming';
	this.num = 100;
}
var father = new Father();
Son.prototype = father;
function Son() {
	this.hobbit = 'smoke';
}
var son = new Son();
son.num ++;
console.log(son.num); // 101
console.log(father.num); // 100
```
## 原型链
1. 如何构成原型链
2. 原型链上属性的增删改查
3. 绝大多数对象的最终都会继承自`Object.prototype`
4. `Object.create(原型)`
```
Object.prototype.toString.call(123); // "[object Number]"
```
## call/apply
作用：改变this指向
区别：传的参数形式不同
```
function Person(name, age) {
	// var this = obj;
	this.name = name;
	this.age = age;
}
var person = new Person('wang', 100);
var obj = {};
Person.call(obj);
Person.call(obj, 'chen', 300);
// test() --> test.call()

function Person(name, age) {
	this.name = name;
	this.age = age;
}
function Student(name, age, sex, tel, grade) {
	Person.call(this, name, age);
	// Person.apply(this, [name, age]);
	this.sex = sex;
	this.tel = tel;
	this.grade = grade;
}
var student = new Student('wang', 30, 'male', 123, 2017);
```
## 继承发展史
1. 传统形式 --> 原型链
过多的继承了没用的属性
```
Grand.prototype.lastName = 'js';
function Grand() {
}
var grand = new Grand();
Father.prototype = grand();
function Father() {
	this.name = 'hehe';
}
var father = new Father();
Son.prototype = father;
function Son() {
}
```
2. 借用构造函数
不能继承借用构造函数的原型
```
function Person(name, age, sex) {
	this.name = name;
	this.age = age;
	this.sex = sex;
}
function Student(name, age, sex, grade) {
	Person.call(this, name, age, sex);
	this.grade = grade;
}
var student = new Student('wang', 100, 'male', '2018');
```
每次构造函数都要多走一个函数
3. 共享原型
不能随便改动自己的原型
```
Father.prototype.lastName = 'wang';
function Father() {
}
function Son() {
}
Son.prototype = Father.prototype;
var son = new Son();
var father = new Father();
```
4. 圣杯模式
```
Father.prototype.lastName = 'wang';
function Father() {
}
function Son() {
}
function inherit(target, origin) {
	var F = function() {}
	F.protoytype = origin.prototype;
	target.prototype = new F();
	target.prototype.constructor = target;
	target.prototype.uber = origin.prototype;
}
inherit(Son, Father);
var son = new Son();
var father = new Father();

// YUI3
var inherit = (function() {
	var F = function() {};   // 属性私有化
	return function(target, origin) {
		F.prototype = origin.prototype;
		target.prototype = new F();
		target.prototype.constructor = target;
		target.prototype.uber = origin.prototype;
	}
}())
```
## 命名空间
管理变量，防止污染全局，适用于模块化开发
```
var init = (function() {
	var name = 'abc';
	function callName() {
		console.log(name);
	}
	return function() {
		callName();
	}
}())
```
## 属性的表示方法
`obj.prop`
`obj['prop']`
## 对象的枚举
`for in`
`hasOwnProperty`
`in`
`instanceof`
```
var obj = {
	name: 'wang';
	age: 100,
	sex: 'male''
	weight: 123,
	hegith: 180,
	__proto__: {
		lastName: 'deng'
	}
}
for (var prop in obj) {
	console.log(obj['prop']);
	if (obj.hasOwnProperty(prop)) {
		console.log(obj['prop'])
	}
}

// A 对象是不是 B构造函数构造出来的
// 看A原型链上有没有B 的原型
```

















































