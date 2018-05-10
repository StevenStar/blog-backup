---
title: 前端面试集锦
date: 2018-05-10 16:14:28
tags: 前端,面试
category: 前端
---

# 一、HTML 面试问题及答案
## HTML 基础
1. 说说你对语义化的理解？
```
去掉或者丢失样式的时候能够让页面呈现出清晰的结构
有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。
```
2. Doctype作用? 严格模式与混杂模式如何区分？它们有何意义??
```
<!DOCTYPE>声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。
严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。
在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。   
```

# 二、CSS 面试问题及答案
## CSS 基础
1. 介绍一下css盒子模型?
```
IE 盒子模型，标准 W3C 盒子模型
    IE的content部分包含了 border 和 pading;

```
2. 行内元素有哪些？块级元素有哪些?
```
df
```
3. .css选择符有哪些？优先级算法如何计算?
```
ID选择器
类选择器
标签选择器
相邻选择器
子选择器
后代选择器
通配符选择器
属性选择器
伪类选择器
可继承的样式
不可继承的样式

优先级就近原则，同权重情况下样式定义最近者为准;
```

# 三、JAVASCRIPT 面试问题及答案
## JS 基础
1. 介绍一下JS的数据类型？
```
简单类型：String、Number、Boolean、Null、Undefined
复杂类型：Object

&扩展：
  1. null与undefined有什么区别？
     null 表示一个对象被定义了，值为“空值”，而undefined 表示不存在这个值。所以使用typeof判断是，null返回的是object，而undefined返回的是undefind
  2. Boolean类型在进行判断的时候设置为 0、-0、null、""、false、undefined 或 NaN，则该对象设置为 false。否则设置为 true（即使 value 参数是字符串 "false"）
```
2. 如何通过JS判断一个数组？
```
instanceof方法
    instanceof 运算符是用来测试一个对象是否在其原型链原型构造函数的属性。
    var arr = []; 
    arr instanceof Array; // true

constructor方法
    constructor 属性返回对创建此对象的数组函数的引用，就是返回对象相对应的构造函数。
    var arr = []; 
    arr.constructor == Array; //true

特性判断法
    利用判断数组独有的length和splice方法，但是这是不靠谱的，因为对象也能添加方法和属性。那怎么办了，有一个办法，可以利用数组的length属性没法枚举来判断。
    function isArray(object){
    	//判断length属性是否是可枚举的 对于数组 将得到false  
    	return  object && typeof object==='object' && typeof object.length==='number' && typeof object.splice==='function' && !(object.propertyIsEnumerable('length'));

最简单的方法
    这种写法，是 jQuery 正在使用的，淘宝的 kissy 也是使用这种方式。
    Object.prototype.toString.call(value) == '[object Array]'
    // 利用这个方法，可以写一个返回数据类型的方法
    var isType = function (obj) {
    	return Object.prototype.toString.call(obj).slice(8,-1); 
    }

ES5新增方法isArray()
    var a = new Array(123);
    var b = new Date();
    console.log(Array.isArray(a)); //true
    console.log(Array.isArray(b)); //false

&扩展
    使用instaceof和construcor，被判断的array必须是在当前页面声明的。比如，一个页面（父页面）有一个框架，框架中引用了一个页面（子页面），在子页面中声明了一个array，并将其赋值给父页面的一个变量，这时判断该变量，Array == object.constructor;会返回false。
    最简单的方法，在IE6下判断null和undefined，有一些bug，判断undefined和null均为Object，(并不是bug，是在ES3的标准下返回的就为Object)

```
3. 谈一谈let与var的区别？
```
let为ES6新添加申明变量的命令，它类似于var，但是有以下不同：
    let命令不存在变量提升，如果在let前使用，会导致报错
    暂时性死区，如果块区中存在let和const命令，就会形成封闭作用域
    不允许重复声明，因此，不能在函数内部重新声明参数
```
4. map与forEach的区别？
```
因为平时基本只用forEach，所以这个很尴尬，索性就把新增的数组方法都刷一遍吧。
    forEach方法，是最基本的方法，就是遍历与循环，默认有3个传参：分别是遍历的数组内容item、数组索引index、和当前遍历数组Array。另外，除去第一个必须的回调函数参数，还可以接受一个上下文参数(改变回调函数的this指向)；并且forEach不会遍历空元素。
    map方法，基本用法与forEach一致，但是不同的，它会返回一个新的数组，所以在callback需要有return值，如果没有，会返回undefined。(从字面理解，map就是映射的意思)
    filter方法，用法和map很相似，从字面理解，就是过滤、筛选的意思。但是函数的callback需要返回布尔值true或false，并且返回值只需要为弱等==即可。
    some 方法，对数组中每一项运行指定函数，如果该函数对任一项返回true，则返回true。(一旦遇到true，就会中断循环，返回true，类似于||判断)
    every方法，对数组中的每一项运行给定函数，如果该函数对每一项返回true，则返回true。(一旦遇到false，就会中断循环，返回false，类似于&&判断)
    indexOf方法，与字符串中的indexOf类似，返回数组索引值，如果没有匹配，则会返回-1，第二个参数为可选，表示从当前位置开始搜索。
    lastIndexOf方法，与indexOf相似，只是是从数组的末尾开始查找，而第二个参数的默认值是array.length - 1。
    reduce方法，字面意思应该是‘减少’，但是实际是‘递归’的意思。实际就是应用一个函数针对数组的两个值(从左到右)，以减至一个值。它的callback接收4个参数：之前值(上一次循环返回的值)、当前值、索引值以及数组本身。initialValue参数可选，表示初始值。
```
5. 谈一谈你理解的函数式编程？
```
    简单说，"函数式编程"是一种"编程范式"（programming paradigm），也就是如何编写程序的方法论。
    它具有以下特性：闭包和高阶函数、惰性计算、递归、函数是"第一等公民"、只用"表达式"，不用"语句"(都会有返回值)、没有"副作用"、不修改状态、引用透明性。
    具体的特性代表了什么，还要好好研究一下！！
```
6. 谈一谈箭头函数与普通函数的区别？
```
箭头函数使得表达更加简洁。(这个是废话)
函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
不可以使用yield命令，因此箭头函数不能用作Generator函数。
```
7. 谈一谈函数中this的指向吧？
```
this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，实际上this的最终指向的是那个调用它的对象。
《javascript语言精髓》中大概概括了4种调用方式：
    方法调用模式
    函数调用模式
    构造器调用模式
    apply/call调用模式
特别补充：
    在构造器调用时，如果加入了return并且return了一个对象，this会指向这个return的对象。
    为什么构造器时this会指向new的对象？
    var p = new Emp();
    // 过程模拟，new关键字会创建一个空的对象，然后会自动调用一个函数apply方法，将this指向这个空对象，这样的话函数内部的this就会被这个空的对象替代。
    var p = {};
    Emp.apply(p);
    p.__proto__=Emp.prototype;
```
8. 谈一谈闭包吧？
```
「闭包」，是指那些能够访问独立(自由)变量的函数 (变量在本地使用，但定义在一个封闭的作用域中)。换句话说，这些函数可以“记忆”它被创建时候的环境。特性：
    函数嵌套函数
    函数内部可以引用外部的参数和变量
    参数和变量不会被垃圾回收机制回收
```
9. 异步编程的实现方式？
```
回调函数：
    优点：简单、容易理解
    缺点：不利于维护，代码耦合高
事件监听(采用时间驱动模式，取决于某个事件是否发生)：
    优点：容易理解，可以绑定多个事件，每个事件可以指定多个回调函数
    缺点：事件驱动型，流程不够清晰
发布/订阅(观察者模式)：
    类似于事件监听，但是可以通过‘消息中心’，了解现在有多少发布者，多少订阅者。
Promise对象
    优点：可以利用then方法，进行链式写法；可以书写错误时的回调函数；
    缺点：编写和理解，相对比较难
Generator函数
    优点：函数体内外的数据交换、错误处理机制
    缺点：流程管理不方便
async函数
    优点：内置执行器、更好的语义、更广的适用性、返回的是Promise、结构清晰。
    缺点：错误处理机制
```
10. function P(){}
    P.prototype.a = 'a';
    function C(){}
    C.prototype = new P();
    var obj1 = new C();
    通过obj1来进行修改a
```
方法一：
    obj1._prototype_.a = 'xx';
方法二：
    obj1.constructor.prototype.a = 'xx';
```
11. 说一下图片的格式 jpg、png、gif 
```
png8以及png24 
png8：8位索引色，1位透明通道 
png24：24位索引色，8位透明通道 
png图片设置半透明 
opacity，filter（滤镜）、png24本身是支持半透明的
```
12. 说说动画?
```
CSS animation 
javascript操作（太频繁，经常reflow和repaint，面试官不满意） 
canvas画图
```
13. 谈一下你对ajax的认识?
```
```
14. 请谈谈事件冒泡的过程?
```
```
15. 请你谈谈Cookie的弊端?
```
cookie虽然在持久保存客户端数据提供了方便，分担了服务器存储的负担，但还是有很多局限性的。
    第一：每个特定的域名下最多生成20个cookie
    IE和Opera 会清理近期最少使用的cookie，Firefox会随机清理cookie。
    cookie的最大大约为4096字节，为了兼容性，一般不能超过4095字节。
    IE 提供了一种存储可以持久化用户数据，叫做uerData，从IE5.0就开始支持。每个数据最多128K，每个域名下最多1M。这个持久化数据放在缓存中，如果缓存没有清理，那么会一直存在。
优点：极高的扩展性和可用性
缺点：
```
16. 浏览器本地存储？
```
在较高版本的浏览器中，js提供了sessionStorage和globalStorage。在HTML5中提供了localStorage来取代globalStorage。
html5中的Web Storage包括了两种存储方式：sessionStorage和localStorage。
sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。
而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。
```
17. DOM操作——怎样添加、移除、移动、复制、创建和查找节点?
```
创建新节点:
    createDocumentFragment() // 创建一个DOM片段
    createElement() // 创建一个具体的元素
    createTextNode() // 创建一个文本节点
添加、移除、替换、插入:
    appendChild()
    removeChild()
    replaceChild()
    insertBefore() // 在已有的子节点前插入一个新的子节点
查找:
    getElementsByTagName() // 通过标签名称
    getElementsByName() // 通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
    getElementById() // 通过元素Id，唯一性
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```