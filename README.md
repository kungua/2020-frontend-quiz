## 注意事项
1. [很多] 公司面试题目都是常年不更新的，[可能]你搜该公司往年的面经，就能猜到今年的题目
2. 很多公司的面试官的知识也是常年不更新的，你不要答得太[偏激]，应该了解大众的想法。
3. 搜索某道题目的具体答案时，不要用[百度]
## 技巧
1. 遇到比较抽象的题目就具体话(举例)，遇到比较具体的题目就抽象化（简述）
2. 抽象题目搜知乎，代码题目搜 Stack Overflow 或博客
3. [xxx的原理]这种题目一般都是说源代码思路，但你不需要看源代码，直接看别人的博客即可(再次强调不要用百度)
## HTML
1. 必考： 你是怎么理解 HTML 语义化的？
    - 举例
2. meta viewport 是做什么用的，怎么写?
    - 举例
3. 你用过哪些 html5 标签？
    - 举例
4. H5 是什么？
    - 简述
    - header,nav,footer,article,main
    - canvas,video,audio
# CSS
1. 必考：两种盒模型分别说一下？
    
border-box 写起来更方便
2. 必考：如何垂直居中？

https://jscode.me/t/topic/1936
3. 必考：flex 怎么用？

[一个例子](https://codesandbox.io/s/mutable-grass-psscl?fontsize=14&hidenavigation=1&theme=dark)
4. 必考：BFC 是什么？

BFC 块级格式化上下文 给一个 div 加一个 overflow: hidden， div 里面的浮动元素就会被包裹起来
5. CSS 选择器优先级
    - 越具体优先级越高 （长）
    - 现在后面的覆盖写在前面的
    - important！ 最高少用
6. 清除浮动说一下
    - 代码
    ```css
    .clearfix:after {
        display: block;
        content: " ";
        clear: both;
    }
    ```
7. 移动端高清方案如何解决?
8. 简述从网页输入url到网页展示的过程发生了哪些事情 ?

首先浏览器主进程接管，开了一个下载线程。
然后进行HTTP请求（DNS查询、IP寻址等等），中间会有三次捂手，等待响应，开始下载响应报文。
将下载完的内容转交给Renderer进程管理。
Renderer进程开始解析css rule tree和dom tree，这两个过程是并行的，
所以一般我会把link标签放在页面顶部。
解析绘制过程中，当浏览器遇到link标签或者script、img等标签，浏览器会去下载这些内容，遇到时候缓存的使用缓存，不适用缓存的重新下载资源。
css rule tree和dom tree生成完了之后，开始合成render tree，这个时候浏览器会进行layout，开始计算每一个节点的位置，然后进行绘制。
绘制结束后，关闭TCP连接，过程有四次挥手。
Q3 你刚刚说了三次握手，四次挥手，那你描述一下？
Q4 刚刚Q2中说的CSS和JS的位置会影响页面效率，为什么？
css在加载过程中不会影响到DOM树的生成，但是会影响到Render树的生成，进而影响到layout，
所以一般来说，style的link标签需要尽量放在head里面，因为在解析DOM树的时候是自上而下的，
而css样式又是通过异步加载的，
这样的话，解析DOM树下的body节点和加载css样式能尽可能的并行，加快Render树的生成的速度。
js脚本应该放在底部，原因在于js线程与GUI渲染线程是互斥的关系，如果js放在首部，
当下载执行js的时候，会影响渲染行程绘制页面，js的作用主要是处理交互，
而交互必须得先让页面呈现才能进行，所以为了保证用户体验，尽量让页面先绘制出来。
9. `SSR` 和客户端渲染有什么区别？
10. 移动端 `rem` 布局如何实现? 简述原理?
11. `JSbridge`原理, `js` 和 `native`是如何通信的?
12. flex布局和传统布局有什么区别？
13. 说了下双飞翼布局
14. 双飞翼布局怎么保证三列的高度一致呢？
15. 双飞翼布局具体怎么实现的？
16. 假设用flex实现双飞翼布局，让三列等高？
17. css在flex盒子里加一个float浮动元素，会出现什么效果？
18. 使用flex布局实现头部吸顶，底部吸底，中间可滚动布局，必须使用flex布局。
19. 宽高等比用css如何实现
## 原生JS
1. 必考： ES6 语法知道哪些，分别怎么用？
    1. [阮一峰 ES6 before 23](https://es6.ruanyifeng.com/)
    2. [方应杭 es6 文字版 | Promise、class](https://fangyinghang.com/es-6-tutorials/)
    3. 异步 ES6 Generator yield ES7 Async await
    4. 举一些ES6对String字符串类型做的常用升级优化?
    5. 举一些ES6对Array数组类型做的常用升级优化
    6. 举一些ES6对Number数字类型做的常用升级优化
    7. 举一些ES6对Object类型做的常用升级优化?(重要)
    8. 举一些ES6对Function函数类型做的常用升级优化?
2. 必考： Promise、Promise.all、Promise.race 分别怎么用？
    1. Promise 对象用于表示一个异步操作的最终完成（或失败）及其结果值
    2. `Promise.all(iterable)` 方法返回一个 `Promise` 实例，此实例在 `iterable` 参数内所有的 `promise` 都完成 或 参数中不包含 `promise` 时回调完成；如果参数中 `promise` 有一个失败，此实例回调失败，失败原因是第一个失败的 `Promise` 结果
        - `Promise.all` 等待所有都完成（或第一个失败）。
        - 如果参数中包含非 `promise` 值，这些值将被忽略，但仍然会被放在返回数组中（如果 `promise` 完成的话）：
    3. `Promise.race(iterable)` 方法返回一个 `promise` 一旦迭代器中的某个 `promise` 解决或拒绝，返回的 `promise` 就会解决或拒绝
        - 只处理返回最快的那一个
    4. `finally`

[Promise Code](https://codesandbox.io/s/eloquent-vaughan-38fgn?fontsize=14&hidenavigation=1&theme=dark)
3. 必考： 手写函数防抖和函数节流
    1. 防抖
    ```javascript
    // 带着一起做
    // https://codesandbox.io/s/focused-visvesvaraya-7f6ur
    let timer = null;
    
    btn1.onclick = function() {
      if (timer) {
        console.log("接到了一单新的外卖， 1s 后我会开始派送");
        clearTimeout(timer);
      }
      timer = setTimeout(() => {
        console.log("时间到啦 我去送外卖啦");
        clearTimeout(timer);
        timer = null;
      }, 1000);
    };
    ```
    2. 节流
    ```javascript
    // CD 冷却时间
    // https://codesandbox.io/s/jovial-mcclintock-w5y7h?fontsize=14&hidenavigation=1&theme=dark
    var cd = false;
    const fn = () => {
      console.log("你释放了妙手回春");
    };
    btn1.onclick = function() {
      if (cd) {
        console.log("我还不能使用那个法术");
      } else {
        fn();
        cd = true;
        var timeId = setTimeout(() => {
          cd = false;
        }, 3000);
      }
    };
    ```
    2. 节流
4. 必考： 手写 AJAX
```javascript
var request = new XMLHTTPRequest()
request.open('GET', '/api/xxx')
request.onreadystatechange = () => { // request.onload
    if (request.readyState === 4) {
        console.log('请求完成')
        if (request.status === 200) {
            console.log('请求成功')
        }
    }
}
request.send()
```
5. 必考： 这段代码里面的 this 是什么？
    1. fn() this->window/global
    2. obj.fn() this->obj
    3. fn.call(xx) this->xx
    4. fn.apply(xx) this-> xx
    5. fn.bind(xx) this->xx
    6. new Fn() this->新的对象
    7. fn = () => {} this->外面的this
    8. with/this
```javascript
// 1
var obj = {
  name: "wcky",
  foo: function() {
    console.log(this.name); //wcky
  }
};
obj.foo();
// 显示绑定，通过call()或者apply()方法，第一个参数是一个对象。
// 2
function foo() {
  console.log(this.a);
}
var obj = {
  a: 2
};
foo.call(obj); // 2
// 3
let a = 1;
const obj = {
    a: 2,
    b: () => {
        console.log(this.a);
    },
    c: function() {
        console.log(this.a);
    }
}
obj.b();
obj.c();
console.log(this.a);
var a = 1;
const obj = {
    a: 2,
    b: () => {
        console.log(this.a);
    },
    c: function() {
        console.log(this.a);
    }
}
obj.b();
obj.c();
console.log(this.a);
```

[方应杭 this](https://zhuanlan.zhihu.com/p/23804247)
6. 必考： 闭包/立即执行函数是什么？

[方应杭 闭包](https://zhuanlan.zhihu.com/p/22486908)

[方应杭 立即执行函数](https://zhuanlan.zhihu.com/p/22465092)
7. 必考： 什么是JSONP，什么是 CORS，什么是跨域？
    - 跨域: 
        - 同源策略(Same origin Policy)：浏览器出于安全方面的考虑，只允许与同域下的接口交互。
        - 同域是指：
            - 同协议：如都是http或者https
            - 同域名：如都是http://jirengu.com/a 和http://jirengu.com/b
            - 同端口：如都是80端口
    - [实现一下 JSONP](https://zhuanlan.zhihu.com/p/22600501)
    - [阮一峰谈 CORS](http://www.ruanyifeng.com/blog/2016/04/cors.html)
8. 常考： async/await 怎么用，如何捕获异常？

`async function` 用来定义一个返回`AsyncFunction`对象的异步函数。异步函数是指通过事件循环异步执行的函数，他会通过一个隐式的 `Promise` 返回其结果。如果你在代码中使用了异步函数，就会发现他的语法和结构会更像是标准的同步函数。

`try { await xxx() }catch {} `

[Async await 代码](https://codesandbox.io/s/pensive-agnesi-3ftdz?fontsize=14&hidenavigation=1&theme=dark)

[Async MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)
9. 常考： 如何实现深拷贝？
    - 递归
    - 判断类型
    - 检查循环引用（环）
    - 不可能拷贝 `__proto__`
    ```javascript
    JSON.parse(JSON.stringfiy(obj))
    ```

背代码
10. 常考： 如何使用正则实现 trim()？
```javascript
function trim(str) {
    return str.replace(/^\s+|\s+$/g, '')
}
```

[30分钟入门正则表达式](https://deerchao.cn/tutorials/regex/regex.htm)
11. 常考： 不用 class 如何实现继承？用 class 又如何实现？


```javascript
// 方式1
function Animal() {
    this.name = 'animal'; this.b = 'gua'
}
Animal.prototype.move = function() {console.log('move')}
function Dog() {}
Dog.prototype = new Animal()
// 无法实现多继承
// 父类新增原型方法/原型属性，子类都能访问到

// 方式2
function Animal() {
    this.name = 'animal'; this.b = 'gua'
}
Animal.prototype.move = function() {console.log('move')}
function Dog(){
  Animal.call(this);
}
//可以实现多继承
// 但是只能继承父类的实例属性和方法，不能继承原型属性/方法

// 方式3
function Animal() {
    this.name = 'animal'; this.b = 'gua'
}
Animal.prototype.move = function() {console.log('move')}
function Dog(){
  Animal.call(this, arguments);
  this.d = 2
}
let f = function() {}
f.prototype = Animal.prototype
Dog.prototype = new f()

Dog.prototype.constructor = Dog

Dog.say = function(){}

// 使用 class
class Dog extends Animal{
    constructor() {
        super()
    }
}
// 可以继承实例属性/方法，也可以继承原型属性/方法
// 但是实例化了两个A的构造函数
```
12. 常考： 如何实现数组去重？
```javascript
const arr = [12, 32, 89, 12, 12, 12, 78, 12, 32]

function unique1(array) {
    const n = []
    for (let i = 0; i < array.length; i++) {
        if (n.indexOf(array[i]) === -1) {
            n.push(array[i])
        }
    }
    return n
}
// 速度最快 空间换时间
function unique2(array) {
    const n = {}, r = [], type
    for(let i = 0; i < array.length; i++) {
        type = typeof array[i]
        if (!n[array[i]) {
            n[array[i]] = [type]
            r.push(array[i])
        } else if (n[array[i]].indexOf(type) < 0) {
            n[array[i]].push(type)
            r.push(array[i])
        }
    }
    return r
}
// 数组下标判断法
function unique3(array) {
    const n = [array[0]]
    for (var i = 1; i < array.length; i++) {
        if (array.indexOf(array[i]) === i) {
            n.push(array[i])
        }
    }
    return n
}
// es6
arr = [... new Set(arr)]
// or
function dedupe(array) {
    return Array.form(new Set(array))
}
```
13. 放弃： == 相关题目（反着答）
14. 送命题： 手写一个 Promise (一定要背代码)
```javascript
```
15. 浏览器事件有哪些过程? 为什么一般在冒泡阶段, 而不是在捕获阶段注册监听?`addEventListener`参数分别是什么?
16. 面向对象如何实现? 需要复用的变量怎么处理?
17. 移动端300ms延时的原因? 如何处理?

历史原因: 07年safari 为了支持双击缩放造成的

处理方法1
```html
<meta name="viewport" content="user-scalable=no">
<meta name="viewport" content="initial-scale=1,maximum-scale=1">
```
处理方法2
```js
window.addEventListener( "load", function() {
FastClick.attach( document.body );
}, false );
// 那FastClick的原理是什么呢？ 其实就是FastClick在检测到touchend事件之后，会通过 DOM 自定义事件立即触发一个模拟 click 事件，并把浏览器在 300 毫秒之后真正触发的 click 事件阻止掉。
```
18. 实现一个函数，判断输入是不是回文字符串。
```javascript
function isPalindrome(str) {
    if (typeof str !== 'string') {
        return false
    }
    return str.split('').reverse().join('') === str
}
```
19. JS 有哪些数据类型? 如何判断? null 和 undefined 区别? 应用场景?

`null undefined string boolean object number symbol`
20. new String('a') 和 'a' 是一样的么?
21. 移动端如何实现下拉到底部跟随移动结束后回弹的动画?
22. 移动端如何优化首页白屏时间过长
23. ES6 generator函数简述
24. JS浮点数运算不精确如何解决?
25. 请简单实现双向数据绑定mvvm
```html
<input id="input"/>
<script>
const data = {};
const input = document.getElementById('input');
Object.defineProperty(data, 'text', {
  set(value) {
    input.value = value;
    this.value = value;
  }
});
input.onchange = function(e) {
  data.text = e.target.value;
}
</script>
```
26. 实现Storage，使得该对象为单例，并对 localStorage 进行封装设置值setItem(key,value)和getItem(key)
```javascript
var instance = null;
class Storage {
  static getInstance() {
    if (!instance) {
      instance = new Storage();
    }
    return this.instance;
  }
  setItem = (key, value) => localStorage.setItem(key, value),
  getItem = key => localStorage.getItem(key)
}
```
27. 进度条文字反色

当时我给的是js的方案，在进度条宽度变化的时候，计算盖过每一个文字的50%，如果超过，设置文字相反颜色。

当然css也有对应的方案，也就是 mix-blend-mode，我并没有接触过。

对应html也有对应方案，也就设置两个相同位置但是颜色相反的dom结构在重叠在一起，顶层覆盖底层，最顶层的进度条取overflow为hidden，其宽度就为进度。
28. 用 JS 递归的方式写1到100求和？
```javascript
function sum(n) {
    return n === 1 ? 1 : n + sum(n-1)
}
sum(100)
```
29. umd 是什么？

前端有一个历史问题 包管理系统 js全局变量互相影响
    
- requireJS define() amd 异步模块定义 浏览器
- nodeJS Module.exports = {} commonJS NodeJS
- UMD 都能用
- [ES6 Module](http://es6.ruanyifeng.com/#docs/module#%E4%B8%A5%E6%A0%BC%E6%A8%A1%E5%BC%8F)
30. slice slipce的函数签名
31. 向数组首位加入一个子项，如何避免修改原数组
32. for...In和for...of的区别？如何用for...of遍历对象？
33. async 函数的实现原理
## DOM
1. 必考： 事件委托

```javascript
ul.addEventListener('click', function(event) {
    if (event.target.tagName.toLowerCase() === 'li') { // 我可以不判断标签 去判断类名啊
        console.log('点击了 li')
    }
})
```
事件流分为两种，捕获事件流和冒泡事件流。
冒泡事件流从目标节点开始执行，一直往父节点冒泡查找执行，直到查到到根节点。
捕获事件流从根节点开始执行，一直往子节点查找执行，直到查找执行到目标节点。
2. 曾考： 用 mouse 事件写一个可拖曳的 div
```javascript
let dragging = false;
let position = {};
app.onmousedown = e => {
  dragging = true;
  const { clientX: x, clientY: y } = e;
  position = [x, y];
};
document.onmousemove = e => {
  if (!dragging) {
    return;
  }
  const { clientX: x, clientY: y } = e;
  const deltaX = x - position[0];
  const deltaY = y - position[1];
  const left = parseInt(app.style.left || 0);
  const top = parseInt(app.style.top || 0);
  app.style.left = left + deltaX + "px";
  app.style.top = top + deltaY + "px";
  position = [x, y];
};
document.onmouseup = () => {
  dragging = false;
};
```
[代码](https://codesandbox.io/s/exciting-maxwell-6295c?fontsize=14&hidenavigation=1&theme=dark)
3. DOM事件中target和currentTarget的区别
4. getBoundingClientRect获取的top和offsetTop获取的top区别 
## HTTP
1. 必考： HTTP 的状态码有哪些？分别什么意思？
    1. 100 Continue
    2. 200 Ok
    3. 201 Created
    4. 202 Accepted
    5. 204 No Content
    6. 300 Multiple Choices
    7. 301 Moved Permanently
    8. 302 Found
    9. 303 See Other
    10. 304 Not Modify
    11. 400 Bad Request
    12. 401 Unauthorized
    13. 403 Forbidden
    14. 404 Not Found
    15. 405 Method Not Allow
    16. 414 Request-URI Too Long
    17. 422 Unprocessable Entity
    18. 500 Internal Server Error
    19. 501 Not Implement
    20. 502 Bad Gateway
    21. 503 Service Unavailable
2. 大公司必考： HTTP 缓存有哪几种？

浏览器缓存机制有两种，一种为强缓存，一种为协商缓存。
对于强缓存，浏览器在第一次请求的时候，会直接下载资源，然后缓存在本地，
第二次请求的时候，直接使用缓存。
对于协商缓存，第一次请求缓存且保存缓存标识与时间，
重复请求向服务器发送缓存标识和最后缓存时间，服务端进行校验，如果失效则使用缓存。

强缓存方案
`Expires`：服务端的响应头，第一次请求的时候，告诉客户端，该资源什么时候会过期。
`Expires` 的缺陷是必须保证服务端时间和客户端时间严格同步。
上一句 => Expires 的 bug 是如果用户调整了本地时间那么文件将不会正常过期
Cache-control：max-age，表示该资源多少时间后过期，解决了客户端和服务端时间必须同步的问题，

协商缓存方案
If-None-Match/ETag：缓存标识，对比缓存时使用它来标识一个缓存，第一次请求的时候，
服务端会返回该标识给客户端，客户端在第二次请求的时候会带上该标识与服务端进行对比并
返回If-None-Match标识是否表示匹配。
Last-modified/If-Modified-Since：第一次请求的时候服务端返回Last-modified表明请求的资源上次
的修改时间，第二次请求的时候客户端带上请求头If-Modified-Since，表示资源上次的修改时间，服务端拿到这两个字段进行对比。
3. 必考： GET 和 POST 的区别
    1. POST 安全 GET 不安全
    2. GET 长度限制(1024) POST 没有(4M / 10M)
    3. GET 参数放在 URL 上，POST 放在消息体里
    4. GET 只需要一个报文，POST 需要两个以上
    5. GET 幂等， POST 不幂等
    6. GET 获取数据 POST 提交数据
4. Cookie vs LocalStorage vs SessionStorage vs Session
    1. Cookie 服务器发给浏览器的一段字符串 浏览器在每次访问相关域名的时候都需要带上这段字符串
    2. Seesion 浏览器与服务器进行的一段时间内的对话
    3. Cookie 存储于浏览器 Seesion 存储于服务器
    4. Seesion 基于 Cookie 实现 将 SessionId 存放在 Cookie 中
    5. Cookie 和 LocalStorage 的区别 
        - Cookie 的大小是 4k LocalStorage 5M
        - Cookie 用来存用户信息 LocalStorage 用来存储一些没有那么重要的信息
        - Cookie 会发送到服务器 LocalStorage 不会
    6. SessionStorage 和 LocalStorage 有什么区别
        - SessionStorage 会过期 LocalStorage 不会
5. HTTP 报文头部有哪些字段? 有什么意义?
6. HTTP code?
7. TCP 三次握手的过程
8. 静态文件的浏览器缓存如何实现?
9. HTTP1 和 HTTP2 的区别
    1. 屈光宇 博客
        - 多路复用
        - 服务端推送
        - 强制开启 HTTPS
## 框架 Vue
1. 必考： watch 和 computed 和 methods 区别是什么？
    - 监听数据 计算属性
    - computed 是有缓存的只有在值变化时会触发 watch 没有缓存 页面重新渲染时必定触发
2. 必考： Vue 有哪些生命周期钩子函数？分别有什么用？
    1. beforeCreate
    2. created
    2. beforeMount
    3. mounted
    4. beforeUpdate
    5. upodated
    6. beforeDestroy
    7. destroyed

[好好再看看文档](https://cn.vuejs.org/v2/guide/instance.html#%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90)
3. 必考： VUe 如何实现组件通信？
    1. 父子组件通信 $emit
    2. 爷孙 eventBus 或者两对父子组件
    3. 兄弟组件尽量不要通讯 可以把通过数据提升
    4. Vuex
4. 必考： Vue 数据响应式怎么做到的？

`Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，
并返回这个对象。

当你把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。
5. 必考： Vue.set 是做什么用的？
6. Vuex 你怎么用的？
    1. Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。
        - state
        - getter
        - mutation
        - action
        - mudule
7. `Vue Router` 你怎么用的？
    1. 背下文档第一句：Vue Router 是 Vue.js 官方的路由管理器。
    2. 说出核心概念的名字和作用：History 模式/导航守卫/路由懒加载
    3. 说出常用 API：router-link/router-view/this.$router.push/this.$router.replace/this.$route.params
    
```javascript
    this.$router.push('/user-admin')
    this.$route.params
```

8. 路由守卫是什么？
9. Vue的如何实现双向绑定的？
    - Vue 根本不是双向绑定的
    - V-Model
    - 转换为数据响应式
10. 说一下vue<keep-alive>对应的生命周期？
11. 异步组件

[把有颜色的字 和 注意事项背下来就可以](https://cn.vuejs.org/v2/guide/reactivity.html)
10. Vue是如何实现绑定事件的?
11. 主流框架的数据单向/双向绑定实现原理?
12. Vue中Compile过程说一下？
## 框架 React (先不准备好了)
1. 必考： 受控组件 vs 非受控组件
2. 必考： React 有哪些生命周期函数？ 分别有什么用？（Ajax 请求放在哪个阶段？）
3. 必考： React 如何实现组件间通信？
4. 必考： shouldComponentUpdate 有什么用？
5. 必考： 虚拟 DOM 是什么？

首先说说为什么要使用Virturl DOM，因为操作真实DOM的耗费的性能代价太高，
所以react内部使用js实现了一套dom结构，在每次操作在和真实dom之前，
使用实现好的diff算法，对虚拟dom进行比较，递归找出有变化的dom节点，
然后对其进行更新操作。为了实现虚拟DOM，
我们需要把每一种节点类型抽象成对象，每一种节点类型有自己的属性，
也就是prop，每次进行diff的时候，react会先比较该节点类型，
假如节点类型不一样，那么react会直接删除该节点，
然后直接创建新的节点插入到其中，假如节点类型一样，
那么会比较prop是否有更新，假如有prop不一样，
那么react会判定该节点有更新，那么重渲染该节点，
然后在对其子节点进行比较，一层一层往下，直到没有子节点。
6. 必考： 什么是高阶组件？
7. React diff 的原理是什么
8. 必考： Redux 是什么？
9. connect 的原理是什么？
10. react 虚拟 DOM 是什么? 如何实现? 说一下diff算法?
11. React Diff 算法?
12. Diff 算法为什么是O(n)复杂度而不是O(n^3)
## TypeScript
1. never 的类型是什么？

不应该出现的类型
2. TypeScript 比起 JavaScript 有什么优点？

有类型（搜知乎）
## Webpack
1. 必考： 有哪些常见的 loader 和 plugin, 你用过哪些？
    1. loader
        - html pug-loader markdown-loader
        - css postcss-loader scss-loader less-loader style-loader
        - js babel-loader eslint-loader
        - 图片 image-loader
    2. plugin
        - html html-webpack-plugin
        - css extract-text-plugin
2. 英语题： loader 和 plugin 的区别是什么？
3. 必考： 如何按需加载代码？
```javascript
import("").then
```
4. 必考： 如何提高构建速度？

dll 、code split、HappyPack
5. 转译出的文件过大怎么办？
6. webpack的原理, loader 和 plugin 是干什么的? 有自己手写过么?
7. Rollup和webpack区别, treeshaking是什么?
8. 你说一下webpack的一些plugin，怎么使用webpack对项目进行优化。

正好最近在做webpack构建优化和性能优化的事儿，当时吹了大概15~20分钟吧，插件请见webpack插件归纳总结。

构建优化
1、减少编译体积 ContextReplacementPugin、IgnorePlugin、babel-plugin-import、babel-plugin-transform-runtime。
2、并行编译 happypack、thread-loader、uglifyjsWebpackPlugin开启并行
3、缓存 cache-loader、hard-source-webpack-plugin、uglifyjsWebpackPlugin开启缓存、babel-loader开启缓存
4、预编译 dllWebpackPlugin && DllReferencePlugin、auto-dll-webapck-plugin

性能优化
1、减少编译体积 Tree-shaking、Scope Hositing。
2、hash缓存 webpack-md5-plugin
3、拆包 splitChunksPlugin、import()、require.ensure

上面五题请参考[此篇文章](https://zhuanlan.zhihu.com/p/44438844)
## 安全
1. 必考： 什么是XSS？如何预防？
2. 必考： 什么是CSRF？如何预防？
## 开放题目
1. 必考： 你遇到最难的问题是怎样的？

回答这种问题讲究一波三折。

- 一开始没搞懂
- 去网上看了个答案
- 一试发现这个广为流传的答案是有坑的
- 于是自己看 issue
- 发现还有一个小细节
- 然后解决了
- 谁知道还是在某种 edge case有问题
- 于是自己看规范看源码，搞定

100分

面试官想看你有没有讲故事的能力。（有些面试官以为这是在考察技术，呵呵，其实是在考察讲故事能力）

实际上呢，全是在 stackoverflow 上搜的。包括看源码哪一行都是 stackoverflow 上的网友说的。

你说你不上 stackoverflow？ emmmm，不会面向 stackoverflow 编程的程序员我们不敢要，再见，下一位。

2. 你在团队中的突出贡献是什么？
3. 最近在关注什么新技术？
4. 有没有看什么源码，看了后有什么记忆深刻的地方，有什么收获？
5. 如何看待前端框架选型?
6. 工作中最出色的点, 和你最头疼的问题 如何解决的?
7. 平时如何学习, 最近接触了解了哪些新的知识?
8. 你觉得自己在前端工作的最大的优点是什么 拿实际工作的内容举例?

## 刁钻题目
1. 代码
```javascript
[1, 2, 3].map(parseInt)

 1
 NaN
 NaN
```
2. 代码
```javascrpt
a(124) = {name: 'gua'}
a(124).x = a(124) = (126){}

a(126).x? //undefinded
```
3. `(a== 1 && a == 2 && a== 3)` 可能为 true 嘛？
```javascript
a = {
  value: 0,
  toString(){
    a.value += 1
    return a.value 
  }
}
```
## 超纲题
1. JS垃圾回收机制
    - 什么是垃圾
        1. 没有被引用的变量可能是垃圾，三个变量互相引用形成了环是垃圾
    - 浏览器如何清除垃圾
        1. 标记清除算法
        [原文](https://javascript.info/garbage-collection)
2. Eventloop 说一下

[Node Eventloop 官方文档[英译汉]](https://zhuanlan.zhihu.com/p/34924059)

浏览器轮训操作系统触发的事件
```
-----js
-----js
ajax - 0.2s c++ 轮训 (eventloop NodeJS 的概念并不是浏览器的概念)
-----js
-----js
-----js
```

NodeJS  (3个阶段)

![image.png](https://i.loli.net/2019/11/20/uAyRjUV1YlBCS9e.png)

浏览器 (2个阶段 (一会儿(宏任务), 马上(微任务)))

首先，js是单线程的，主要的任务是处理用户的交互。
而用户的交互无非就是响应DOM的增删改，
使用事件队列的形式，一次事件循环只处理一个事件响应，使得脚本执行相对连续，
所以有了事件队列，用来储存待执行的事件，那么事件队列的事件从哪里被push进来的呢。
那就是另外一个线程叫事件触发线程做的事情了，
他的作用主要是在定时触发器线程、异步HTTP请求线程满足特定条件下的回调函数push到事件队列中，
等待js引擎空闲的时候去执行，
当然js引擎执行过程中有优先级之分，首先js引擎在一次事件循环中，
会先执行js线程的主任务，然后会去查找是否有微任务microtask（promise），
如果有那就优先执行微任务，如果没有，在去查找宏任务macrotask（setTimeout、setInterval）进行执行。

![image.png](https://i.loli.net/2019/11/20/WjCoicAeESPmzg8.png)
3. 观察者模式实现?
4. 前端性能优化
    1. 减少http请求：合并js文件、合并css文件、雪碧图的使用、base64表示简单的图片
    2. 减少资源体积：gzip压缩、js混淆、css压缩、图片压缩
    3. 缓存：DNS缓存、CDN部署与缓存、http缓存
    4. 移动端优化：使用长cache减少重定向、首屏优化、不滥用web字体
    DOM操作和渲染方面：
    
    1. 优化网页渲染：css文件放头部，js文件放在尾部或者异步、尽量避免内联样式
    2. DOM操作优化：避免在document上直接进行频繁的DOM操作、使用classname代替大量的内联样式修改、对于复杂的UI元素，设置position为absolute或fixed、尽量使用css动画、
    使用requestAnimationFrame代替setInterval操作、适当使用canvas、尽量减少css表达式的使用、使用事件代理
    3. 操作细节注意：避免图片或者frame使用空src、在css属性为0时，去掉单位、禁止图像缩放、正确的css前缀的使用、移除空的css规则、对于css中可继承的属性，如font-size，尽量使用继承，少一点设 置、缩短css选择器，多使用伪元素等帮助定位
    4. 移动端优化：长列表滚动优化、函数防抖和函数节流、使用touchstart、touchend代替click、HTML的viewport设置、开启GPU渲染加速
    数据方面：
    
    6. 图片加载处理：图片预加载、图片懒加载、首屏加载时进度条的显示
    7. 异步请求的优化：使用正常的json数据格式进行交互、部分常用数据的缓存、数据埋点和统计
    （这一题其实是上一题的懒加载没答出来，面试小哥哥的拓展延伸问的问题，说实话其实记得一些最常见的，但是这么详细的真的是记不住）

## 算法
### 排序
1. 快速排序
2. 计数排序
3. 冒泡排序
4. 选择排序
5. 归并排序
6. 插入排序
### 二分法
### 翻转二叉树
### 其他
1. 我现在有一个数组[1,2,3,4]，请实现算法，得到这个数组的全排列的数组，
如[2,1,3,4]，[2,1,4,3]。你这个算法的时间复杂度是多少？
2. 我现在有一个背包，容量为m，然后有n个货物，重量分别为w1,w2,w3...wn，每个货物的价值是v1,v2,v3...vn，w和v没有任何关系，请求背包能装下的最大价值。
3. 随机遍历数组。一个长度为n的数组，每次随机挑选一个元素，尽可能快地遍历到全部元素，最终返回一个新的数组。
## 个性化题目
- PWA
- echarts.js/d3.js
- three.js
- flutter
- SSR
## 收集了一些笔试题 

[阿里云](https://zhuanlan.zhihu.com/p/58352843)

## 还有一些有趣的问题

[P7 ](https://www.zhihu.com/question/277437814)
## 一份完整流程的面试题
### 基本问题（5")

1. 请简单介绍一下自己。
2. 介绍一下你的工作经历及做过的项目，以及用到了哪些技术。
### 基础（15")

1. 有三个元素，第一个与第三个宽度都为100px，中间元素占用剩余空间，怎么做到中间元素随着浏览器宽度的变化而变化
2. 讲讲box-sizing
3. 不知宽高的垂直水平居中
4. 如何解决使用 inline-block 引起的空白间隙的问题？
5. 分别举个现实中的应用场景。使用 CSS 创建一个三角形（一个箭头向右的三角图标）。
6. 讲讲 postion 定位
7. 脱离文档流的有哪些，不脱离的有哪些
8. H5 和 CSS3 用得多么？
9. 讲讲 CSS3 属性你用哪些比较多？ 
10. 关于图片，你了解哪些形式，你觉得哪种场合用哪种？它们优劣如何？然后这些图片的应用场景能说说不？
11. 了解过缓存这些吗
12. 什么场景使用那些技术？
13. 那 LocalStorage 会根据时间清空吗？还是会一直存在浏览器上？
14. 有一个长度为 100 的数组，请求出该数组的前 10 个元素之和。
15. 写一个程序打印 1 到 100 这些数字，遇到数字为 3 的倍数，打印 “A” 替代该数字；遇到 5 的倍数，用 “B” 代替；遇到即是 3 的倍数又是 5 的倍数，打印 “AB”。
16. 一句话介绍下 JavaScript 的闭包、原型链和 this 关键字吧
17. 闭包缺点？
18. 哪些常见操作会造成内存泄漏？
19. 如何改变 this 关键字？
20. 介bind apply call区别
21. 深浅拷贝的区别（分别有啥用户）
22. 描述网页从输入url到渲染的过程 
23. 同步异步或者事件机制
24. Ajax的原理，你平常怎么发送网络请求的
25. 那你能讲下 get 和 post 请求吗？
26. 跨域通信有哪些方案，各有什么不同？
27. 使用过 Promise 吗
28. 说说xss与csrf，怎么防止?
### 针对简历问（15")

1. 会ES6吗，什么是解构赋值？
2. 其他 ES6 语法你用过吗
3. 主流前端框架如 Angular/React/Vue 等之间有哪些差异及特点，选取一个描述其组件生命周期。
4. 讲下 v-if 与 v-show 的区别吗
5. v-for 你使用过程中，有遇到什么问题或者关注点吗
6. v-bind:class 有使用过吗？有什么要注意的吗？
7. 组件之间的传值通信？
8. vuex
9. Vue hash 路由和 history 路由的区别
10. 虚拟dom
11. JS 基础考察
    有如下代码
    ```javascript
    function fn(){
        return 1
    }
    ```
    请问 fn 和 fn() 的区别是什么？
12. JS 基础考察有如下代码
    ```javascript
    var name = 'x'
    var obj = {
        name: 'frank'
    }
    ```
    请问 obj[name] 的值是多少？
13. JS 基础考察有如下代码
    ```javascript
    var a = [1,2,3]
    ```
    请问，a.concat(4) 与 a.push(4) 的区别是什么？
14. JS 基础考察有如下未完成的代码
    ```javascript
    Array.prototype.self = function(){
      //未完成
    }
    let arr = [1,2,3,4,5]
    arr.self() // [1,2,3,4,5]
    ```
    请填写未完成的部分，使得 arr.self() 的值是 [1,2,3,4,5]
15. JS 基础考察JS 有哪几种数据类型？
16. debounce 和 throttle 的使用场景分别是什么？简单实现一个 debounce 或者 throttle。
17. map reducer filter 各自有什么作用
18. 讲一个你遇到的比较有困难的问题 你是怎么解决他的
19. 一个 web 项目如何做性能优化
20. 用 React 写一个 Hello World（要求能运行，你可以使用 jsbin.com 或者 codesandbox.io 或者 GitHub Pages 来写）如果你想看起来比其他应聘者厉害，你可以加各种其他的东西。
21. 用 Vue 写一个 Hello World（要求能运行，你可以使用 jsbin.com 或者 codesandbox.io 或者 GitHub Pages 来写）如果你想看起来比其他应聘者厉害，你可以加各种其他的东西。
22. 写出你觉得厉害的程序员的名字或者开源项目的名字，并说出理由，不少于五个。

### 收尾（5")
1. 有没有开源项目的参与经历？
2. 你有什么想问我们的问题吗？
## 另一份完整的面试题 
基本问题（5")

1、请简单介绍一下自己。
2、介绍一下你的工作经历及做过的项目，以及用到了哪些技术。

基础（15")

一句话介绍下 JavaScript 的闭包、原型链和 this 关键字吧
如何改变 this 关键字？
闭包缺点？
深浅拷贝的区别（分别有啥用户）
分别举个现实中的应用场景。
介绍下 ES 规范中的 Generator 吧（如果不会，可以改成介绍 Promise）
Generator 是如何运行的？（迭代器、yield 暂停）
可以用来做什么？（不仅仅是异步）
有用过吗？以及我们在什么场景可以用到他？
和 async + await 有啥区别？
遇到不支持的浏览器怎么办？比如我们要支持 IE 10。
组件里用到 Generator 怎么处理？（补丁方案）
介绍下 React 的 Hooks 吧。
你怎么看 hooks？有没有用过？能不能满足业务需求？
你觉得在哪些方面可能不满足需求？
全局数据如何处理？
有哪些社区基于 hooks 的库可以解决你的问题吗？
介绍下 Webpack 和 Babel 吧。
构建后项目运行慢怎么办？
prefetch 和 preload 的区别？
code-splitting。
Webpack 构建慢怎么办？
介绍下 tree-shaking。
使用 tree-shaking 有啥要注意的？
有些有副作用有些没副作用怎么办？
介绍下热更新。
React 应用的热更新是怎么处理的？
Babel 可以解决什么问题？你有用 Babel 解决过业务中的问题吗？

针对简历问（15")

介绍下你们的测试流程。
会做哪些方面的测试？业务代码测吗？视图层测吗？
Jest 你觉得相比其他测试工具的优点是什么？你最喜欢他哪个功能？
介绍下 Redux。
Redux 和 immer 如何结合？为啥要用 immer？
为什么用 Redux？
有用哪些 Redux 的扩展吗？选择原因？
相比 hooks，你觉得 Redux 还有优势吗？你对于 Redux 的未来怎么看？
Redux 是如何实现时间胶囊的？（即撤销、重做）
有用 TypeScript 吗？Redux 如何优雅地和 TypeScript 做结合？
介绍下你们的微前端方案。
职责连模式是什么意思？
你觉得微前端解决的是什么问题？
为什么要用微前端来解决？不用微前端还有其他什么方案？（多技术栈？如果是相同技术栈，还需要微前端吗？）
web component 是最好的方式吗？如果重新设计，你会用什么来做？
性能相关问题。
通讯相关问题。
介绍下前端发布打包的优化方案。
dfs 是什么？
平行预处理指啥？没有走 webpack 吗？
打包时间数据有统计吗？痛点是什么？
有更彻底的优化方案吗？

收尾（5")

有没有开源项目的参与经历？
你有什么想问我们的问题吗？
## 头条前端(未整理)
一轮
1.dom react原理 
2.css布局 
3.js原型链继承
4.fetch取消
5.eventloop
6.instanceof
7.promise封装setstate
8.redux基本组成和设计单向数据流
9.https协议的过程
10.https获取加密密钥的过程
11.http的方法有哪几种,每种方法的有用途
12.类式继承的方案
13.prototype继承的实现
14.数字千分位处理，正则和非正则都要实现
15.借用构造继承，几种组合继承方式
16.看编程代码说出运行结果：
      Process.nextTick，setImmediate 和promise.then 的优先级
      Process.nextTick，pronise, setImmediate的优先级
17.实现一个bind函数
18.千位加逗号
19.三个继承方式的优缺点  优化列出代码
20.odejs的事件循环
21.bfc
22.css实现正方形div水平垂直居中
23.koa1的原理,继承
24.最后是一个写代码 处理有依赖的异步任务 加重试
25. diff的原理
26. es6箭头函数
27. import和requre的区别
28. symbol
29. 函数实现正面模板
30. 正方形实现，三角形实现
31. CSS考了 伪类
32. 实现布局header,content,footer，上中下布局；当content 超出窗口可视区，不显示footer；当content 没超出可视区时，固定footer 在最下面
33. 算法:背包问题、闭包问题、函数柯里化
34. 宽是高的一半的垂直居中，里面有字体也要垂直居中类数组
35. promise async set time out先后次序
36.  event类 on once灯方法
37..  ==的隐式转化
38.什么是闭包，
39.最长子序列
40.二叉树中序遍历
41.http握手原理
42.react 新版本的特性
43. 多空格字符串格式化为数组
44、bind函数运行结果
45、点击table的td显示td内容
46、数字千分位处理
47、固定日期与当前时间格式化处理
48、上中下三栏布局
49、实现一个子类实例可以继承父类的所有方法
50.   Jsonp跨域，js原型继承 & 原型链，promise，二叉树搜寻算法，算法：前端做并发请求控制
51. 杭州一面:
     节流函数
       Koa中间件机制及代码实现
       React Fiber原理以及为什么componentWillRecievedProps会废弃
       给定一个数组，一个期望值，找到数组中两个相加等于期望值
52.深圳前端一面：
         react生命周期 deepClone 回流重绘 canvas
53.深圳前端一面：
          1. 数组去重           2. React Hook原理           3. 列表diff中key的作用           4. Vue v-model原理           5. 场景题：Vue CheckBoxGroup/CheckBox设计           6. Vue双向绑定原理
54.成都前端：
        1、换行字符串格式化
        2、屏幕占满和未占满的情况下，使footer固定在底部，尽量多种方法。
        3、日期转化为2小时前，1分钟前等
        4、多个bind连接后输出的值
        5、原码，补码，反码
        6、事件委托
55.成都前端：
     1，React Hook, Fiber Reconciler ,新的生命周期 getDerivedStateFromPros 为什么是Static
      2，redux 异步
      3，redux 异步中间件原理
      4，express koa 中间件原理
56.北京前端一面：
  1. 宏任务微任务
  2. libUA
  3. express ctx 中间键代码实现
  4. vue 发布订阅和虚拟dom代码实现
  5. 请实现如下的函数，可以批量请求数据，所有的 URL 地址在 urls 参数中，同时可以通过 max 参数      控制请求的并发度，当所有请求结束之后，需要执行 callback 回调函数。发请求的函数可以直接        使用 fetch 即可 

57. 南京前端1面：
 1.事件循环
2.react diff算法，key的作用，setData的机制，事件合成
3.vue的v-model原理
4.实现一个方法，参数是一个generator函数，执行结果是执行完所有generator中的yield
5.获取页面所有img并且下载
6.两个同源tab之间的交互，数据同步

58.上海前端一面：
1. 怎么将一个异步方法promise化，以及实现promise.all()方法
2. vue单页多页的区别，vue路由实现原理
3. vue数据驱动视图原理？更新视图的过程是否是同步的操作？
4. nodejs相关的应用（答：开发命令行工具、web服务，ssr，数据库操作等）
5. vue项目开发环境如何配置？wepack-dev-server 热更新功能实现原理
6. express、koa、redis等技术相关应用
7. [1,2,3].map(parseInt) 执行结果

59. 北京前端一面题：
64. css 如何实现元素a距离屏幕10px，高度无论宽度怎么改变都是其.5
65. 隐式转换，会问为什么这样
66. 同步异步输出的顺序
67. argument是数组吗，如果不是怎么变为数组
68. 如何实现for循环内定时器依次输出123
69. bind实现
70. 函数节流
71. 动态规划算法


59. 北京前端一面：
     1. function request(urls, maxNumber, callback) 要求编写函数实现，根据urls数组内的url地址进行并发网络请求，最大并发数maxNum   ber,当所有请求完毕后调用callback函数(已知请求网络的方法可以使用fetch api)

    2. throttle函数实现

     3.requestAnimationFrame 和 setTime、setInterval的区别，requestAnimationFrame 可以做什么

    4.二叉树路径总和（leetcode 112）

    5. 给定一个不含重复数字的数组arr,指定个数n,目标和sum,判断是否含有由n个不同数字相加得到sum的情况（leetcode 40 变种， 数   字不得重复使用）
60. 上海前端一面：
websocket 原理
http2如何实现多路复用
61.
 1. 冒泡算法
2. 前端安全 ， DOS
3. 前端缓存、回话机制
4. 跨域
5. 计算机网络知识 TCP UDP
6. 测试 单测、集成测试
7. 自动化集成
8. Docker 应用
9. Nodejs express koa

62.成都前端笔试：1、输入一个日期 返回几秒前 几天前或者几月前；
2、153812.7  转化153,812.7；
3、用两种方法 一种是正则；
4、还有关于 bind的一道题；

63. 北京前端一面
①['a','b'],['A','B'],['1','0']，输出['aA1','aA0','aB1','aB0','bA1','bA0','bB1','bB0']，算法的排列组合问题
②vue-router路由监听的原理
③webpack打包的原理，webpack有没有针对打包过程做一些优化提升打包速度
④请实现如下的函数，可以批量请求数据，所有的 URL 地址在 urls 参数中，同时可以通过 max 参数，控制请求的并发度，实现max个请求执行完之后再执行下max个请求，当所有请求结束之后，需要执行 callback 回调函数。发请求的函数可以直接 使用 fetch 即可
⑤vue双向绑定的原理
64.深圳抖音
写一个eventBus，元素水平垂直居中，vuex mobox，小程序架构优化 日志系统

二轮:
1.主要是围绕你的项目经历和技术，有一定的深度，主要还是要对项目全面熟悉；还有一个就是函数     柯理化的编码实现
2. 函数柯里化、Web安全、react性能优化、react算法原理
3.上来直接让写一个autocomplete 组件，可能是想考察业务思考点；
4. 后续的问题主要会接着业务场景问 扣实际场景 不问知识理论；
5. http网络协议 ；
6. tcp为什么是可靠的；
7. js设计模式；
8. solid原则；
9. 柯里化；
10. 
       curry函数实现
       https原理
      webpack打包原理
       babel原理
      node相关基础问题
     我能想到的就这些， 其他的都是项目中，见缝插针问的

11.深圳二面：
       1，一千个棋子，甲先取乙后取，每次最多取七个最少取一个，问是否有一个方案让甲一定赢
        2，3×7的格子，从左上角到右下角，只能往右或者往下，有多少种走法，
        3，一个不均匀硬币，如何抛出均匀概率
        4，然后有一个生成0到13随机数的算法，如何用它均匀生成0到9随机数
        5，两千万高考生成绩如何排序
        6，用链表表示的大数求和
12.杭州二面
   1. css 单行和多行截断
   2. 给一个由域名组成的字符串进行按子域名分组的反转，比如 news.toutiao.com 反转成 com.toutiao.news 需要 in place 做，                        3.其他技术问题都是穿插在我的业务项目里面的，有点针对实际情景给解决方案

13.深圳抖音二面：
最近在做项目（痛点，难点，怎么解决），ssr（ssr csr混合怎么处理），小程序架构（带来的优缺点），状态管理，异步编程（各个优缺点）

三轮：
1.自己做得最有成就的项目
2.自己主动承担并是核心的项目
3.项目深度:比如现场实现vue的数据代理等
4.技术广度:什么是微前端等
5.职业发展
6. 1. js实现依赖注入
    2. 接口攻击的方式和防御措施
    3. https握手过程
    4. 设计模式
    5. redux和 mobx的区别
    6. js多线程如何共享大的数据


