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
1. css盒子模型?
```
页面渲染时，dom元素所采用的布局模型。可通过box-sizing进行设置。根据计算宽高的区域可分为：
1. content-box (W3C标准盒模型)
2. border-box (IE 盒子模型) IE的content部分包含了 border 和 pading;
3. padding-box
4. margin-box

```
2. BFC?
```
块级格式化上下文，是一个独立的渲染区域，让处于BFC内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。
IE下为Layout，可通过zoom:1; 触发
触发条件：
1. 跟元素
2. position: absolute/fixed
3. float 元素
4. overflow != visible
规则：
1. 属于同一个BFC的两个相邻Box垂直排列
2. 属于同一个BFC的两个相邻Box的margin会发生重叠
3. BFC中子元素的margin box的左边，与包含块（BFC）border box的左边相接触（子元素absolute除外）
4. BFC的区域不会与float的元素区域重叠
5. 计算BFC的高度时，浮动子元素也参与计算
6. 文字层不会被浮动层覆盖，环绕于周围
应用：
1. 阻止margin重叠
2. 可以包含浮动元素 -- 清除内部浮动（清除浮动的原理是两个div都位于同一个BFC区域之中）
3. 自适用两栏布局
4. 可以阻止元素被浮动元素覆盖
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
!import > 行内样式 > #id > .class > tag > * > 继承 > 默认
```
4. 层叠上下文？
```
元素提升为一个比较特殊的图层，在三维空间中（z轴）高出普通元素一等。
触发条件：
1. 根层叠上下文(html)
2. position
3. css3属性
    flex
    transform
    opacity
    filter
    will-change
    -webkit-overflow-scrolling
4. 层叠等级
    在同一层叠上下文中，层叠等级才有意义
    z-index的优先级最高
background/border > z-index为负值 > 块级元素 > 浮动元素 > 行内元素 > z-index: 0/auto > z-index为正值
```
5. 居中布局？
```
1. 水平居中
    行内元素：text-align: center;
    块级元素：margin: 0 auto;
    absolute + transform
    flex + justify-content: center;
2. 垂直居中
    line-height: height;
    absolute + transform
    flex + align-items: center;
    table
3. 水平垂直居中
    absolute + transoform;
    flex + justify-content + align-items;
```
6. 去除浮动影戏那个，防止父级高度塌陷
```
通过增加尾部清除浮动: :after/<br> : clear: both;
创建父级BFC
父级设置高度
```
7. link 与@import的区别
```
link功能比较多，可以定义rss，定义Rel等作用，而@import 只能用于加载css
当解析到link时，页面会同步加载所引的css，而@import所引用的css会等到页面加载完才被加载
@import需要IE5以上才能使用
link可以使用js动态引入，@import不行
```
8. css预处理器(sass/less/postcss)
```
css预处理的原理：是将类css更多更强大的功能，常用功能：嵌套，变量，循环语句，条件语句，自动前缀，单位转换，mixin复用
```
9. css 动画
```
transition: 过渡动画
    transition-property: 属性
    transition-duration: 间隔
    transition-timing-function: 曲线
    transition-delay: 延迟
    常用钩子：transitionend
animation/keyframes
    animation-name: 动画名称，对应@keyframes
    animation-duration: 间隔
    animation-timing-function: 曲线
    animation-delay: 延迟
    animation-iteration-count: 次数
        infinite: 循环动画
    animation-direction: 方向
        alternate: 反向播放
    animation-fill-mode: 静止模式
        forwards: 停止时，保留最后一帧
        backwards: 停止时，回到第一帧
        both: 同时运用forwards/backwards
    常用钩子：animationend
动画属性：尽量使用动画属性进行动画，能拥有较好的性能表现
    translate
    scale
    rotate
    skew
    opacity
    color
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

## 框架vue
1. nextTick
```
在下次dom更新循环结束之后执行延迟回调，可用于获取更新后的dom状态
    新版本中默认是mincrotasks, v-on中会使用macrotasks
    macrotasks任务的实现:
        setImmediate / MessageChannel / setTimeout
```
2. 生命周期
```
_init_
    initLifecycle/Event，往vm上挂载各种属性
    callHook: beforeCreated: 实例刚创建
    initInjection/initState: 初始化注入和 data 响应性
    created: 创建完成，属性已经绑定， 但还未生成真实dom
    进行元素的挂载： $el / vm.$mount()
    是否有template: 解析成render function
    *.vue文件: vue-loader会将<template>编译成render function
    beforeMount: 模板编译/挂载之前
    执行render function，生成真实的dom，并替换到dom tree中
    mounted: 组件已挂载
update:
    执行diff算法，比对改变是否需要触发UI更新
    flushScheduleQueue
    watcher.before: 触发beforeUpdate钩子        - watcher.run(): 执行watcher中的 notify，通知所有依赖项更新UI
    触发updated钩子: 组件已更新
actived / deactivated(keep-alive): 不销毁，缓存，组件激活与失活
destroy:
    beforeDestroy: 销毁开始
    销毁自身且递归销毁子组件以及事件监听
        remove(): 删除节点
        watcher.teardown(): 清空依赖
        vm.$off(): 解绑监听
destroyed: 完成后触发钩子
上面是vue的声明周期的简单梳理，接下来我们直接以代码的形式来完成vue的初始化
new Vue({})
// 初始化Vue实例
function _init() {
     // 挂载属性
    initLifeCycle(vm)
    // 初始化事件系统，钩子函数等
    initEvent(vm)
    // 编译slot、vnode
    initRender(vm)
    // 触发钩子
    callHook(vm, 'beforeCreate')
    // 添加inject功能
    initInjection(vm)
    // 完成数据响应性 props/data/watch/computed/methods
    initState(vm)
    // 添加 provide 功能
    initProvide(vm)
    // 触发钩子
    callHook(vm, 'created')
    // 挂载节点
    if (vm.$options.el) {
        vm.$mount(vm.$options.el)
    }
}

// 挂载节点实现
function mountComponent(vm) {
     // 获取 render function
    if (!this.options.render) {
        // template to render
        // Vue.compile = compileToFunctions
        let { render } = compileToFunctions()
        this.options.render = render
    }
    // 触发钩子
    callHook('beforeMounte')
    // 初始化观察者
    // render 渲染 vdom，
    vdom = vm.render()
    // update: 根据 diff 出的 patchs 挂载成真实的 dom
    vm._update(vdom)
    // 触发钩子
    callHook(vm, 'mounted')
}

// 更新节点实现
funtion queueWatcher(watcher) {
    nextTick(flushScheduleQueue)
}

// 清空队列
function flushScheduleQueue() {
     // 遍历队列中所有修改
    for(){
        // beforeUpdate
        watcher.before()
        // 依赖局部更新节点
        watcher.update()
        callHook('updated')
    }
}

// 销毁实例实现
Vue.prototype.$destory = function() {
     // 触发钩子
    callHook(vm, 'beforeDestory')
    // 自身及子节点
    remove()
    // 删除依赖
    watcher.teardown()
    // 删除监听
    vm.$off()
    // 触发钩子
    callHook(vm, 'destoryed')
}
```
3. 数据响应(数据劫持)
```
看完生命周期后，里面的watcher等内容其实是数据响应中的一部分。数据响应的实现由两部分构成: 观察者( watcher ) 和 依赖收集器( Dep )，其核心是 defineProperty这个方法，它可以 重写属性的 get 与 set 方法，从而完成监听数据的改变。
    Observe (观察者)观察 props 与 state
        遍历 props 与 state，对每个属性创建独立的监听器( watcher )
    使用 defineProperty 重写每个属性的 get/set(defineReactive）
        get: 收集依赖
        Dep.depend()
            watcher.addDep()
        set: 派发更新
            Dep.notify()
            watcher.update()
            queenWatcher()
            nextTick
            flushScheduleQueue
            watcher.run()
            updateComponent()
大家可以先看下面的数据相应的代码实现后，理解后就比较容易看懂上面的简单脉络了。
let data = {a: 1}
// 数据响应性
observe(data)

// 初始化观察者
new Watcher(data, 'name', updateComponent)
data.a = 2

// 简单表示用于数据更新后的操作
function updateComponent() {
    vm._update() // patchs
}

// 监视对象
function observe(obj) {
     // 遍历对象，使用 get/set 重新定义对象的每个属性值
    Object.keys(obj).map(key => {
        defineReactive(obj, key, obj[key])
    })
}

function defineReactive(obj, k, v) {
    // 递归子属性
    if (type(v) == 'object') observe(v)
    // 新建依赖收集器
    let dep = new Dep()
    // 定义get/set
    Object.defineProperty(obj, k, {
        enumerable: true,
        configurable: true,
        get: function reactiveGetter() {
              // 当有获取该属性时，证明依赖于该对象，因此被添加进收集器中
            if (Dep.target) {
                dep.addSub(Dep.target)
            }
            return v
        },
        // 重新设置值时，触发收集器的通知机制
        set: function reactiveSetter(nV) {
            v = nV
            dep.nofify()
        },
    })
}

// 依赖收集器
class Dep {
    constructor() {
        this.subs = []
    }
    addSub(sub) {
        this.subs.push(sub)
    }
    notify() {
        this.subs.map(sub => {
            sub.update()
        })
    }
}

Dep.target = null

// 观察者
class Watcher {
    constructor(obj, key, cb) {
        Dep.target = this
        this.cb = cb
        this.obj = obj
        this.key = key
        this.value = obj[key]
        Dep.target = null
    }
    addDep(Dep) {
        Dep.addSub(this)
    }
    update() {
        this.value = this.obj[this.key]
        this.cb(this.value)
    }
    before() {
        callHook('beforeUpdate')
    }
}
```
4. virtual dom 原理实现
```
创建 dom 树
树的diff，同层对比，输出patchs(listDiff/diffChildren/diffProps)
    没有新的节点，返回
    新的节点tagName与key不变， 对比props，继续递归遍历子树
        对比属性(对比新旧属性列表):
            旧属性是否存在与新属性列表中
            都存在的是否有变化
            是否出现旧列表中没有的新属性
    tagName和key值变化了，则直接替换成新节点
渲染差异
    遍历patchs， 把需要更改的节点取出来
    局部更新dom
// diff算法的实现
function diff(oldTree, newTree) {
     // 差异收集
    let pathchs = {}
    dfs(oldTree, newTree, 0, pathchs)
    return pathchs
}

function dfs(oldNode, newNode, index, pathchs) {
    let curPathchs = []
    if (newNode) {
        // 当新旧节点的 tagName 和 key 值完全一致时
        if (oldNode.tagName === newNode.tagName && oldNode.key === newNode.key) {
              // 继续比对属性差异
            let props = diffProps(oldNode.props, newNode.props)
            curPathchs.push({ type: 'changeProps', props })
            // 递归进入下一层级的比较
            diffChildrens(oldNode.children, newNode.children, index, pathchs)
        } else {
              // 当 tagName 或者 key 修改了后，表示已经是全新节点，无需再比
            curPathchs.push({ type: 'replaceNode', node: newNode })
        }
    }

     // 构建出整颗差异树
    if (curPathchs.length) {
            if(pathchs[index]){
                pathchs[index] = pathchs[index].concat(curPathchs)
            } else {
                pathchs[index] = curPathchs
            }
    }
}

// 属性对比实现
function diffProps(oldProps, newProps) {
    let propsPathchs = []
    // 遍历新旧属性列表
    // 查找删除项
    // 查找修改项
    // 查找新增项
    forin(olaProps, (k, v) => {
        if (!newProps.hasOwnProperty(k)) {
            propsPathchs.push({ type: 'remove', prop: k })
        } else {
            if (v !== newProps[k]) {
                propsPathchs.push({ type: 'change', prop: k , value: newProps[k] })
            }
        }
    })
    forin(newProps, (k, v) => {
        if (!oldProps.hasOwnProperty(k)) {
            propsPathchs.push({ type: 'add', prop: k, value: v })
        }
    })
    return propsPathchs
}

// 对比子级差异
function diffChildrens(oldChild, newChild, index, pathchs) {
        // 标记子级的删除/新增/移动
    let { change, list } = diffList(oldChild, newChild, index, pathchs)
    if (change.length) {
        if (pathchs[index]) {
            pathchs[index] = pathchs[index].concat(change)
        } else {
            pathchs[index] = change
        }
    }

     // 根据 key 获取原本匹配的节点，进一步递归从头开始对比
    oldChild.map((item, i) => {
        let keyIndex = list.indexOf(item.key)
        if (keyIndex) {
            let node = newChild[keyIndex]
            // 进一步递归对比
            dfs(item, node, index, pathchs)
        }
    })
}

// 列表对比，主要也是根据 key 值查找匹配项
// 对比出新旧列表的新增/删除/移动
function diffList(oldList, newList, index, pathchs) {
    let change = []
    let list = []
    const newKeys = getKey(newList)
    oldList.map(v => {
        if (newKeys.indexOf(v.key) > -1) {
            list.push(v.key)
        } else {
            list.push(null)
        }
    })

    // 标记删除
    for (let i = list.length - 1; i>= 0; i--) {
        if (!list[i]) {
            list.splice(i, 1)
            change.push({ type: 'remove', index: i })
        }
    }

    // 标记新增和移动
    newList.map((item, i) => {
        const key = item.key
        const index = list.indexOf(key)
        if (index === -1 || key == null) {
            // 新增
            change.push({ type: 'add', node: item, index: i })
            list.splice(i, 0, key)
        } else {
            // 移动
            if (index !== i) {
                change.push({
                    type: 'move',
                    form: index,
                    to: i,
                })
                move(list, index, i)
            }
        }
    })

    return { change, list }
}
```
5. Proxy 相比于 defineProperty 的优势
```
数组变化也能监听到
不需要深度遍历监听

let data = { a: 1 }
let reactiveData = new Proxy(data, {
    get: function(target, name){
        // ...
    },
    // ...
})
```
6. vue-router
```
mode
    hash
    history
跳转
    this.$router.push()
    <router-link to=""></router-link>
占位
    <router-view></router-view>
```
7. vuex
```
state: 状态中心
mutations: 更改状态
actions: 异步更改状态
getters: 获取状态
modules: 将state分成多个modules，便于管理
```

## 浏览器
1. 跨标签页通讯
```
不同标签页的通讯，本质原理就是运用一些可以共享的中间介质，因此比较常用的有以下方法：
    通过父页面window.open()和子页面postMessage
        异步下，通过window.open('about: blank') 和 tab.location.href = '*'
    设置同域下共享的localStorage与监听window.onstorage
        重复写入相同的值无法触发
        会受到浏览器隐身模式等的限制
    设置共享cookie与不断轮询脏检查(setInterval)
    借助服务端或中间层实现
```
2. 浏览器架构
```
用户界面
主进程
内核
    渲染引擎
    js引擎
        执行栈
    事件触发线程
        消息队列
            微任务
            宏任务
    网络异步线程
    定时器线程
```
3. 浏览器下事件循环(Event Loop)
```
事件循环是指：执行一个宏任务，然后执行清空微任务列表，循环再执行宏任务，再清微任务列表
```
4. 从输入url到展示的过程
```
DNS解析
TCP三次握手
发送请求，分析url，设置请求报文（头，主体）
服务器返回请求的文件（html）
浏览器渲染
    HTML parser --> DOM Tree
        标记化算法，进行元素状态的标记
    CSS parser --> Style Tree
        结合dom树与style树
    layout：布局
    GPU painting: 像素绘制页面
```
5. 重绘与回流
```
当元素的样式发生变化时，浏览器需要触发更新，重新绘制元素。这个过程中，有两种类型的操作，即重绘与回流
重绘(repaint)：当元素样式的改变不影响布局时，浏览器将使用重绘对元素进行更新，此时由于只需要UI层面的重新像素绘制，因此损耗较少
回流(reflow)：当元素的尺寸、结构或触发某些属性时，浏览器会重新渲染页面，称为回流。此时，浏览器需要重新经过计算，计算后还需要重新页面布局，因此是较重的操作。会触发回流的操作：
    页面初次渲染
    浏览器窗口尺寸大小改变
    元素尺寸、位置、内容发生改变
    元素字体大小改变
    添加或删除可见的dom元素
    激活css伪类(例如：:hover)
    查询某些属性或调用某些方法
        clientWidth,clientHeight,clientTop,clientLeft
        offsetWidth...
        scrollWidth...
        getComputedStyle()
        getBoundingClientRect()
        scrollTo()
回流必定触发重绘，重绘不一定触发回流。重绘的开销较少，回流的代价较高

最佳实践：
    css：
        避免使用table布局
        将动画效果应用到position属性为absolute或fixed的元素上
    js：
        避免频繁操作样式，可汇总后统一一次修改
        尽量使用class进行样式修改
        减少dom的增删次数，可使用字符串或者documentFragment一次性插入
        极限优化时，修改样式可将其display:none后修改
        避免多次触发上面提到的那些触发回流的方法，可以的话尽量用变量存住
```
6. 存储
```
我们经常需要对业务中的一些数据进行存储，通常可分为短暂性存储和持久性存储。
短暂性存储，我们只需要将数据存在内存中，只在运行时可用
持久性存储，可以分为浏览器端与服务器端
    浏览器：
        cookie：通常用于存储用户身份，登录状态等
        localStorage/sessionStorage：长久存储/窗口关闭删除，体积限制为4～5m
        indexDB
    服务器：
        分布式缓存redis
        数据库
```
6. 请你谈谈Cookie的弊端?
```
cookie虽然在持久保存客户端数据提供了方便，分担了服务器存储的负担，但还是有很多局限性的。
    第一：每个特定的域名下最多生成20个cookie
    IE和Opera 会清理近期最少使用的cookie，Firefox会随机清理cookie。
    cookie的最大大约为4096字节，为了兼容性，一般不能超过4095字节。
    IE 提供了一种存储可以持久化用户数据，叫做uerData，从IE5.0就开始支持。每个数据最多128K，每个域名下最多1M。这个持久化数据放在缓存中，如果缓存没有清理，那么会一直存在。
优点：极高的扩展性和可用性
缺点：
```
7. Web Worker
```
现代浏览器为JavaScript创造的 多线程环境。可以新建并将部分任务分配到worker线程并行运行，两个线程可 独立运行，互不干扰，可通过自带的 消息机制 相互通信。
基本用法:
    // 创建 worker
    const worker = new Worker('work.js');

    // 向主进程推送消息
    worker.postMessage('Hello World');

    // 监听主进程来的消息
    worker.onmessage = function (event) {
        console.log('Received message ' + event.data);
    }
限制:
    同源限制
    无法使用 document / window / alert / confirm
    无法加载本地资源

```
8. V8垃圾回收机制
```
垃圾回收: 将内存中不再使用的数据进行清理，释放出内存空间。V8 将内存分成 新生代空间 和 老生代空间。

新生代空间: 用于存活较短的对象
    又分成两个空间: from 空间 与 to 空间
    Scavenge GC算法: 当 from 空间被占满时，启动 GC 算法
        存活的对象从 from space 转移到 to space
        清空 from space
        from space 与 to space 互换
        完成一次新生代GC
老生代空间: 用于存活时间较长的对象
    从 新生代空间 转移到 老生代空间 的条件
        经历过一次以上 Scavenge GC 的对象
        当 to space 体积超过25%
    标记清除算法: 标记存活的对象，未被标记的则被释放
        增量标记: 小模块标记，在代码执行间隙执，GC 会影响性能
        并发标记(最新技术): 不阻塞 js 执行
    压缩算法: 将内存中清除后导致的碎片化对象往内存堆的一端移动，解决 内存的碎片化

```
9. 内存泄露
```
意外的全局变量: 无法被回收
定时器: 未被正确关闭，导致所引用的外部变量无法被释放
事件监听: 没有正确销毁 (低版本浏览器可能出现)
闭包: 会导致父级中的变量无法被释放
dom 引用: dom 元素被删除时，内存中的引用未被正确清空

可用 chrome 中的 timeline 进行内存标记，可视化查看内存的变化情况，找出异常点。
```

```
```

```
```

```
## 服务端与网络
1. http/https 协议
```
1.0 协议缺陷:
    无法复用链接，完成即断开，重新慢启动和 TCP 3次握手
    head of line blocking: 线头阻塞，导致请求之间互相影响
1.1 改进:
    长连接(默认 keep-alive)，复用
    host 字段指定对应的虚拟站点
    新增功能:
        断点续传
        身份认证
        状态管理
        cache 缓存
            Cache-Control
            Expires
            Last-Modified
            Etag
2.0:
    多路复用
    二进制分帧层: 应用层和传输层之间
    首部压缩
    服务端推送
https: 较为安全的网络传输协议
    证书(公钥)
    SSL 加密
    端口 443
TCP:
    三次握手
    四次挥手
    滑动窗口: 流量控制
    拥塞处理
        慢开始
        拥塞避免
        快速重传
        快速恢复
缓存策略: 可分为 强缓存 和 协商缓存
    Cache-Control/Expires: 浏览器判断缓存是否过期，未过期时，直接使用强缓存，Cache-Control的 max-age 优先级高于 Expires
    当缓存已经过期时，使用协商缓存
        唯一标识方案: Etag(response 携带) & If-None-Match(request携带，上一次返回的 Etag): 服务器判断资源是否被修改，
        最后一次修改时间: Last-Modified(response) & If-Modified-Since (request，上一次返回的Last-Modified)
            如果一致，则直接返回 304 通知浏览器使用缓存
            如不一致，则服务端返回新的资源
    Last-Modified 缺点：
        周期性修改，但内容未变时，会导致缓存失效
        最小粒度只到 s， s 以内的改动无法检测到
    Etag 的优先级高于 Last-Modified
```
2. 常见状态码
```
1xx: 接受，继续处理
200: 成功，并返回数据
201: 已创建
202: 已接受
203: 成为，但未授权
204: 成功，无内容
205: 成功，重置内容
206: 成功，部分内容
301: 永久移动，重定向
302: 临时移动，可使用原有URI
304: 资源未修改，可使用缓存
305: 需代理访问
400: 请求语法错误
401: 要求身份认证
403: 拒绝请求
404: 资源不存在
500: 服务器错误
```
3. get / post
```
get: 缓存、请求长度受限、会被历史保存记录
    无副作用(不修改资源)，幂等(请求次数与资源无关)的场景
post: 安全、大数据、更多编码类型
    两者详细对比如下图:
```
4. Websocket
```
Websocket 是一个 持久化的协议， 基于 http ， 服务端可以 主动 push
兼容：
    FLASH Socket
    长轮询： 定时发送 ajax
    long poll： 发送 --> 有消息时再 response
new WebSocket(url)
ws.onerror = fn
ws.onclose = fn
ws.onopen = fn
ws.onmessage = fn
ws.send()
```
5. TCP三次握手
```
建立连接前，客户端和服务端需要通过握手来确认对方:
    客户端发送 syn(同步序列编号) 请求，进入 syn_send 状态，等待确认
    服务端接收并确认 syn 包后发送 syn+ack 包，进入 syn_recv 状态
    客户端接收 syn+ack 包后，发送 ack 包，双方进入 established 状态
```
6. TCP四次挥手
```
客户端 -- FIN --> 服务端， FIN—WAIT
服务端 -- ACK --> 客户端， CLOSE-WAIT
服务端 -- ACK,FIN --> 客户端， LAST-ACK
客户端 -- ACK --> 服务端，CLOSED
```
7. Node 的 Event Loop: 6个阶段
```
timer 阶段: 执行到期的setTimeout / setInterval队列回调
I/O 阶段: 执行上轮循环残流的callback
idle, prepare
poll: 等待回调
    执行回调
    执行定时器
        如有到期的setTimeout / setInterval， 则返回 timer 阶段
        如有setImmediate，则前往 check 阶段
check
    执行setImmediate
close callbacks
```
8. 跨域
```
JSONP: 利用<script>标签不受跨域限制的特点，缺点是只能支持 get 请求
function jsonp(url, jsonpCallback, success) {
    const script = document.createElement('script')
    script.src = url
    script.async = true
    script.type = 'text/javascript'
    window[jsonpCallback] = function(data) {
        success && success(data)
    }
    document.body.appendChild(script)
}
设置 CORS: Access-Control-Allow-Origin：*
postMessage
```
9. 安全
```
XSS攻击: 注入恶意代码
    cookie 设置 httpOnly
    转义页面上的输入内容和输出内容
CSRF: 跨站请求伪造，防护:
    get 不修改数据
    不被第三方网站访问到用户的 cookie
    设置白名单，不被第三方网站请求
    请求校验
```

## 算法
1. 五大算法
```
贪心算法: 局部最优解法
分治算法: 分成多个小模块，与原问题性质相同
动态规划: 每个状态都是过去历史的一个总结
回溯法: 发现原先选择不优时，退回重新选择
分支限界法
```
2. 基础排序算法
```
冒泡排序: 两两比较

    function bubleSort(arr) {
        var len = arr.length;
        for (let outer = len ; outer >= 2; outer--) {
            for(let inner = 0; inner <=outer - 1; inner++) {
                if(arr[inner] > arr[inner + 1]) {
                    [arr[inner],arr[inner+1]] = [arr[inner+1],arr[inner]]
                }
            }
        }
        return arr;
    }
选择排序: 遍历自身以后的元素，最小的元素跟自己调换位置

function selectSort(arr) {
    var len = arr.length;
    for(let i = 0 ;i < len - 1; i++) {
        for(let j = i ; j<len; j++) {
            if(arr[j] < arr[i]) {
                [arr[i],arr[j]] = [arr[j],arr[i]];
            }
        }
    }
    return arr
}
插入排序: 即将元素插入到已排序好的数组中

function insertSort(arr) {
    for(let i = 1; i < arr.length; i++) {  //外循环从1开始，默认arr[0]是有序段
        for(let j = i; j > 0; j--) {  //j = i,将arr[j]依次插入有序段中
            if(arr[j] < arr[j-1]) {
                [arr[j],arr[j-1]] = [arr[j-1],arr[j]];
            } else {
                break;
            }
        }
    }
    return arr;
}

```
3. 高级排序算法
```
快速排序

选择基准值(base)，原数组长度减一(基准值)，使用 splice
循环原数组，小的放左边(left数组)，大的放右边(right数组);
concat(left, base, right)
递归继续排序 left 与 right

function quickSort(arr) {
    if(arr.length <= 1) {
        return arr;  //递归出口
    }
    var left = [],
        right = [],
        current = arr.splice(0,1);
    for(let i = 0; i < arr.length; i++) {
        if(arr[i] < current) {
            left.push(arr[i])  //放在左边
        } else {
            right.push(arr[i]) //放在右边
        }
    }
    return quickSort(left).concat(current,quickSort(right));
}

希尔排序：不定步数的插入排序，插入排序
口诀: 插冒归基稳定，快选堆希不稳定
稳定性： 同大小情况下是否可能会被交换位置, 虚拟dom的diff，不稳定性会导致重新渲染；
```
4. 递归运用(斐波那契数列)： 爬楼梯问题
```
初始在第一级，到第一级有1种方法(s(1) = 1)，到第二级也只有一种方法(s(2) = 1)， 第三级(s(3) = s(1) + s(2))
function cStairs(n) {
    if(n === 1 || n === 2) {
        return 1;
    } else {
        return cStairs(n-1) + cStairs(n-2)
    }
}
```
5. 数据树
```
二叉树: 最多只有两个子节点
    完全二叉树
    满二叉树
        深度为 h, 有 n 个节点，且满足 n = 2^h - 1
二叉查找树: 是一种特殊的二叉树，能有效地提高查找效率
    小值在左，大值在右
    节点 n 的所有左子树值小于 n，所有右子树值大于 n
遍历节点
    前序遍历
        根节点
        访问左子节点，回到 1
        访问右子节点，回到 1
    中序遍历
        先访问到最左的子节点
        访问该节点的父节点
        访问该父节点的右子节点， 回到 1
    后序遍历
        先访问到最左的子节点
        访问相邻的右节点
        访问父节点， 回到 1
插入与删除节点

```
6. 天平找次品
```
有n个硬币，其中1个为假币，假币重量较轻，你有一把天平，请问，至少需要称多少次能保证一定找到假币?
三等分算法:
    将硬币分成3组，随便取其中两组天平称量
        平衡，假币在未上称的一组，取其回到 1 继续循环
        不平衡，假币在天平上较轻的一组， 取其回到 1 继续循环
```