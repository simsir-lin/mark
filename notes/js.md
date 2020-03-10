## 变量
### 类型
* 原始类型
1. Null：只包含一个值：null
2. Undefined：只包含一个值：undefined
3. Boolean：包含两个值：true和false
4. Number：整数或浮点数，还有一些特殊值（-Infinity、+Infinity、NaN）
5. String：一串表示文本值的字符序列
6. Symbol：一种实例是唯一且不可改变的数据类型（es6）
(在es10中加入了第七种原始类型BigInt，现已被最新Chrome支持)
* 对象类型
1. Object：自己分一类丝毫不过分，除了常用的Object，Array、Function等都属于特殊的对象

### 不可变性
* 在JavaScript中，每一个变量在内存中都需要一个空间来存储。内存空间又被分为两种，栈内存与堆内存。JavaScript中的`原始类型`的值被直接存储在栈中，在变量定义时，栈就为其分配好了内存空间。由于栈中的内存空间的大小是固定的，那么注定了存储在栈中的变量就是不可变的。

### 值传递和引用传递
* 值传递：即函数参数仅仅是被传入变量复制给了的一个局部变量，改变这个局部变量不会对外部变量产生影响。
* `ECMAScript`中所有的函数的参数都是按值传递的。

### 精度丢失
* 计算机中所有的数据都是以二进制存储的，所以在计算时计算机要把数据先转换成二进制进行计算，然后在把计算结果转换成十进制。在计算0.1+0.2时，二进制计算发生了精度丢失，导致再转换成十进制后和预计的结果不符。

### 包装类型
* 为了便于操作基本类型值，ECMAScript还提供了几个特殊的引用类型，他们是基本类型的包装类型：
```javascript
true === new Boolean(true); // false
123 === new Number(123); // false
'ConardLi' === new String('ConardLi'); // false
console.log(typeof new String('ConardLi')); // object
console.log(typeof 'ConardLi'); // string
// 引用类型和包装类型的主要区别就是对象的生存期，使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中，而自基本类型则只存在于一行代码的执行瞬间，然后立即被销毁，这意味着我们不能在运行时为基本类型添加属性和方法。
```
* 装箱转换：把基本类型转换为对应的包装类型；拆箱操作：把引用类型转换为基本类型
* 每当我们操作一个基础类型时，后台就会自动创建一个包装类型的对象，从而让我们能够调用一些方法和属性，例如下面的代码：
```javascript
var name = "ConardLi";
var name2 = name.substring(2);
// 实际上发生了以下几个过程：
// 1. 创建一个String的包装类型实例
// 2. 在实例上调用substring方法
// 3. 销毁实例
// 也就是说，我们使用基本类型调用方法，就会自动进行装箱和拆箱操作，相同的，我们使用Number和Boolean类型时，也会发生这个过程。
```
* 从引用类型到基本类型的转换，也就是拆箱的过程中，会遵循ECMAScript规范规定的toPrimitive原则，一般会调用引用类型的valueOf和toString方法，你也可以直接重写toPeimitive方法。一般转换成不同类型的值遵循的原则不同，例如：
1. 引用类型转换为`Number`类型，先调用`valueOf`，再调用`toString`
2. 引用类型转换为`String`类型，先调用`toString`，再调用`valueOf`

### 判断JavaScript数据类型的方式
* `typeof`操作符可以准确判断一个变量的原始类型
* `instanceof` 可以帮助我们判断引用类型具体是什么类型的对象：
```javascript
[] instanceof Array // true
new Date() instanceof Date // true
new RegExp() instanceof RegExp // true
```
* `toString`每一个引用类型都有toString方法，默认情况下，toString()方法被每个Object对象继承。如果此方法在自定义对象中未被覆盖，toString() 返回 "[object type]"，其中type是对象的类型
```javascript
const obj = {};
obj.toString() // [object Object]
// 上面提到了如果此方法在自定义对象中未被覆盖，toString才会达到预想的效果，事实上，大部分引用类型比如Array、Date、RegExp等都重写了toString方法。
// 我们可以直接调用Object原型上未被覆盖的toString()方法，使用call来改变this指向来达到我们想要的效果。
Object.prototype.toString.call(true)  // [object Boolean]
```

### Symbol
```javascript
var sym1 = Symbol();  // Symbol()
var sym2 = Symbol('ConardLi');  // Symbol(ConardLi)
var sym3 = Symbol('ConardLi');  // Symbol(ConardLi)
var sym4 = Symbol({name:'ConardLi'}); // Symbol([object Object])
console.log(sym2 === sym3);  // false
```
* 独一无二，我们用两个相同的字符串创建两个Symbol变量，它们是不相等的，可见每个Symbol变量都是独一无二的
* 不可枚举
* 应用场景
1. 防止XSS
2. 私有属性，借助Symbol类型的不可枚举，我们可以在类中模拟私有属性，控制变量读写：
```javascript
const privateField = Symbol();
class myClass {
  constructor(){
    this[privateField] = 'ConardLi';
  }
  getField(){
    return this[privateField];
  }
  setField(val){
    this[privateField] = val;
  }
}
```
3. 防止属性污染，在某些情况下，我们可能要为对象添加一个属性，此时就有可能造成属性覆盖，用Symbol作为对象属性可以保证永远不会出现同名属性。
```javascript
Function.prototype.myCall = function (context) {
  if (typeof this !== 'function') {
    return undefined; // 用于防止 Function.prototype.myCall() 直接调用
  }
  context = context || window;
  const fn = Symbol();
  context[fn] = this;
  const args = [...arguments].slice(1);
  const result = context[fn](...args);
  delete context[fn];
  return result;
}
```

## 设计模式
### 23种设计模式基于以上6大基本原则结合具体开发实践总结出来的，万变不离其宗，有了这些基本的意识规范，你写出来的，搞不好就是某种设计模式٩(๑>◡<๑)۶
* 单一原则 （SRP）-- 实现类要职责单一,一个类只做一件事或者一类事，不要将功能无法划分为一类的揉到一起，答应我好吗
* 里氏替换原则（LSP）-- 不要破坏继承体系，子类可以完全替换掉他们所继承的父类，可以理解为调用父类方法的地方换成子类也可以正常执行调用，爸爸打下的江山儿子继位得无压力好吗
* 依赖倒置原则（DIP）-- 我说下我的理解，如果某套功能或者业务逻辑可能之后会出现并行的另外一种模式或者较大的调整，那不如把这部分逻辑抽象出来，创建一个包含相关方法的抽象类，而实现类继承这个抽象类来重写抽象类中的方法，完成具体的实现，调用这些功能方法的类不需要关心自己调用的这些个方法的具体实现，只管调用这些抽象类中定义好的形式上的方法即可，不与实际实现这些方法的类发生直接依赖关系，方便之后的实现逻辑的替换更改；
* 接口隔离原则(ISP) : 在设计抽象类的时候要精简单一,白话说就是，A需要依赖B提供的一些方法，A我只用B的3个方法，B就尽量不要给A用不到的方法啦；
* 迪米特法则（LoD）降低耦合,尽量减少对象之间的直接的交互，如果其中一个类需要调用另一个类的某一个方法的话，可通过一个关系类发起这个调用，这样一个模块修改时，就可以最大程度的减少波及。
* 开放-封闭原则（OCP）告诉我们要对扩展开放，对修改关闭，你可以继承扩展我所有的能力，到你手里你想咋改咋改，但是，别 动我 本人 好吗？好的

## MVVM
* 把Model和View关联起来的就是ViewModel。ViewModel负责把Model的数据同步到View显示出来，还负责把View的修改同步回Model。
* MVVM表示视图状态的操作变量的定义应当在VM当中，相关的逻辑交互也应当在VM当中。如果说View提供了视图的所有展示元素；那么VM则可以确定某个视图模块某一时刻某一个状态下的呈现内容。
* 一个VM不一定只和一个View存在关联，它可能同时协调多个视图。

### EventLoop
```javascript
console.log('1');
setTimeout(() => {
  console.log('2');
})
setTimeout(() => {
  console.log('3');
}, 1000)
Promise.resolve().then(() => {
  console.log('4');
})
console.log('5');
// ===> 1,5,4,2,3
```
* 先执行微任务（Promise），再执行宏任务（setTimeout）

### debounce 防抖 -- 把触发非常频繁的事件合并成一次去执行，即在指定时间内只执行一次回调函数，如果在指定的时间内又触发了该事件，则回调函数的执行时间会基于此刻重新开始计算。
```javascript
var debounce = function(fn, delayTime) {  
  var timeId;
  return function () {
    var context = this, args = arguments;
    timeId && clearTimeout(timeout);
    timeId = setTimeout(function {
      fn.apply(context, args);
    }, delayTime)
  }
}
// 执行debounce函数之后会返回一个新的函数，通过闭包的形式，维护一个变量timeId
// 每次执行该函数的时候会结束之前的延迟操作，重新执行setTimeout方法，也就实现了上面所说的指定的时间内多次触发同一个事件，会合并执行一次。
```

### throttle 节流 -- 是指频繁触发事件时，只会在指定的时间段内执行事件回调，即一段时间内只会执行第一次执行的事件
```javascript
var throttle = function(fn, delayTime) {
  var _lastTime = null;
  return function () {
    let _nowTime = +new Date()
    if (_nowTime - _lastTime > delayTime || !_lastTime) {
      fn.apply(this, arguments)
      _lastTime = _nowTime
    }
  }
}
```

### 获取视频封面
```javascript
let video = document.createElement('video')
video.addEventListener('loadeddata', function () {
  file.raw.videoHeight = this.videoHeight
  file.raw.videoWidth = this.videoWidth
  let canvas = document.createElement('canvas')
  canvas.width = 120
  canvas.height = 120
  canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height)
  canvas.toBlob((blob) => {
    let thumbUrl = URL.createObjectURL(blob)
  }, 'image/png')
  video = null
})
video.src = file.url
```

### 重复的定时器
* 当你使用setInterval重复定义多个定时器的时候，可能会出现某个定时器代码在代码再次被添加到执行队列之前还没有完成执行，导致定时器代码连续执行多次。
* 机智Javascript引擎解决了这个问题，使用setInterval()的时候，仅当没有该定时器的其他代码实例时，才会将定时器代码添加到队列中。但这还会导致一些问题：某些间隔被跳过、间隔可能比预期的小
* 为了避免这个两个问题，你可以使用链式setTimeout()调用
```javascript
setTimeout(function(){
    TODO();

    setTimeout(arguments.callee, interval);
}, interval)
```
* arguments.callee获取了当前执行函数的引用，然后为其设置另外一个定时器，这样就确保在下一次定时器代码执行前，必须等待指定的间隔。

### 范围内的随机数
```javascript
const randomInRange = (min, max) => Math.random() * (max - min) + min;
// randomInRange(2,10) -> 6.0211363285087005

// 随机化数组的顺序
const shuffle = arr => arr.sort(() => Math.random() - 0.5);
// shuffle([1,2,3]) -> [2,3,1]
```

### URL参数
```javascript
const getUrlParameters = url => {
  url.match(/([^?=&]+)(=([^&]*))/g).reduce(
    (a, v) => (a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1), a), {}
  )};
// getUrlParameters('http://url.com/page?name=Adam&surname=Smith') -> {name: 'Adam', surname: 'Smith'}
```

### UUID生成器
```javascript
const uuid = _ =>
  ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, c =>
    (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
  );
// uuid() -> '7982fcfe-5721-4632-bede-6000885be57d'
```

### RGB到十六进制
```javascript
const rgbToHex = (r, g, b) => ((r << 16) + (g << 8) + b).toString(16).padStart(6, '0');
// rgbToHex(255, 165, 1) -> 'ffa501'
```

### 16进制颜色代码生成
```javascript
function() {  
  return '#' + ('00000' + (Math.random()*0x1000000<<0).toString(16)).slice(-6);
}
```

### 驼峰命名转下划线
```javascript
'componentMapModelRegistry'.match(/^[a-z][a-z0-9]+|[A-Z][a-z0-9]*/g).join('-').toLowerCase();
```

### 将argruments对象转换成数组
```javascript
var argArray = [...arguments];
```

### Array.prototype.slice.call() & Array.from()
* Array.from() 能将类数组(arguments,NodeList)，可迭代对象(Set,Map)，字符串(String)转换成数组
* Array.from(arrayLike, mapFn, thisArg) -->  Array.from(arrayLike).map(fn(), thisArg)
* Array.prototype.slice.call() 能将类数组(arguments,NodeList)，字符串(String)转换成数组
* Array.prototype.slice.call(arrayLike, index) 从第index个开始转换成数组

### 滚动到顶部
* 使用document.documentElement.scrollTop或document.body.scrollTop获取到顶部的距离。从顶部滚动一小部分距离。
```javascript
const scrollToTop = _ => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }
};

// scrollToTop()
```

### 获取滚动位置
```javascript
const getScrollPos = (el = window) => {
  return {
    x: (el.pageXOffset !== undefined) ? el.pageXOffset : el.scrollLeft,
    y: (el.pageYOffset !== undefined) ? el.pageYOffset : el.scrollTop
  };
};

getScrollPos() -> {x: 0, y: 200}
```

### 测试一个函数所花费的时间
```javascript
const timeTaken = callback => {
  console.time('timeTaken');
  let r = callback();
  console.timeEnd('timeTaken');
  return r;
};
// timeTaken(() => Math.pow(2, 10)) -> 1024
// (logged): timeTaken: 0.02099609375ms
```

### 通过定义固定的JSON scheme ，然后拼接生成

### 数组操作
* 删除数组尾部元素,一个简单的用来清空或则删除数组尾部元素的简单方法就是改变数组的length属性值
```javascript
const arr = [11, 22, 33, 44, 55, 66];
arr.length = 3;
console.log(arr);  // => [11, 22, 33]
arr.length = 0;
console.log(arr);  // => []
```
* 使用对象解构来处理数组
```javascript
const csvFileLine = '1997,John Doe,US,john@doe.com,New York';
const { 2: country, 4: state } = csvFileLine.split(',');
console.log(state);  // => New York
```
* 从数组中移除重复元素，无法去除重复的对象
```javascript
console.log([...new Set([42, 'foo', 42, 'foo', true, true])])  // => [42, foo, true]
```
* 使用reduce同时实现map和filter
```javascript
// 将数列中的值翻倍，然后挑选出那些大于50的数
const numbers = [10, 20, 30, 40];
const doubledOver50 = numbers.reduce((finalList, num, index)=>{
  num = num * 2;
  if (num > 50){
    finalList.push(num);
  }
  return finalList;
}, []);
console.log(doubledOver50)    // => [60, 80]
```

### Spread 运算符 (...)
* ...[1, 2] => 1 2
```javascript
var a, b, c, d, e;  
a = [1,2,3];  
b = "dog";  
c = [42, "cat"];  

// Using the concat method.  
d = a.concat(b, c);  
// Using the spread operator.  
e = [...a, b, ...c];  

console.log(d);  // 1, 2, 3, "dog", 42, "cat"
console.log(e);  // 1, 2, 3, "dog", 42, "cat"
```

### Promise
* 添加finally方法
```javascript
Promise.prototype.finally = function (callback) {
  let P = this.constructor;
  return this.then(
    value  => P.resolve(callback()).then(() => value),
    reason => P.resolve(callback()).then(() => { throw reason })
  );
};
```
* 简单实现Promise
```javascript
class MyPromise {
    constructor(fn) {
        this.resolvedCallbacks = [];
        this.rejectedCallbacks = [];
        this.state = "PADDING";
        this.value = "";
        fn(this.resolve.bind(this), this.reject.bind(this));
    }
    resolve(value) {
        if (this.state === "PADDING") {
            this.state = "RESOLVED";
            this.value = value;
            this.resolvedCallbacks.forEach(cb => cb());
        }
    }
    reject(value) {
        if (this.state === "PADDING") {
            this.state = "REJECTED";
            this.value = value;
            this.rejectedCallbacks.forEach(cb => cb());
        }
    }
    then(resolve = function() {}, reject = function() {}) {
        if (this.state === "PADDING") {
            this.resolvedCallbacks.push(resolve);
            this.rejectedCallbacks.push(reject);
        }
        if (this.state === "RESOLVED") {
            resolve(this.value);
        }
        if (this.state === "REJECTED") {
            reject(this.value);
        }
    }
}
```

* async/await
```javascript
async function timeout(ms) {
  await new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint('hello world', 50);
```

* 深拷贝、浅拷贝 - 浅拷贝和深拷贝都只针对于引用数据类型，浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存；但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象；
1. 浅拷贝的实现方式
```javascript
function simpleCopy (initalObj) {
   var obj = {};
   for ( var i in initalObj) {
    obj[i] = initalObj[i];
   }
   return obj;
}

// ES6 的 Object.assign()
let newObj = Object.assign({}, obj);

// ES6 的对象扩展
let newObj = {...obj};
```
2. 深拷贝的实现方式
```javascript
function deepClone(obj) {
    let objClone = Array.isArray(obj) ? [] : {};
    if (obj && typeof obj === "object") {
        // for...in 会把继承的属性一起遍历
        for (let key in obj) {
            // 判断是不是自有属性，而不是继承属性
            if (obj.hasOwnProperty(key)) {
                //判断ojb子元素是否为对象或数组，如果是，递归复制
                if (obj[key] && typeof obj[key] === "object") {
                    objClone[key] = this.deepClone(obj[key]);
                } else {
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}

let newObj = JSON.parse(JSON.stringify(obj));

// 用 lodash 函数库提供的 _.cloneDeep 方法实现深拷贝。
var _ = require('lodash');
var newObj = _.cloneDeep(obj);
```


### 模块化 CommonJS、AMD/CMD、ES6 Modules
#### CommonJS
* Node.js是`commonJS`规范的主要实践者，它有四个重要的环境变量为模块化的实现提供支持：`module`、`exports`、`require`、`global`。实际使用时，用module.exports定义当前模块对外输出的接口，用`require`加载模块。
* CommonJS一个文件就是一个模块，拥有单独的作用域; 普通方式定义的变量、函数、对象都属于该模块内; 通过require来加载模块，通过exports和modul.exports来暴露模块中的内容
* 所有代码都运行在模块作用域，不会污染全局作用域；模块可以多次加载，但只会在第一次加载的时候运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果；模块的加载顺序，按照代码的出现顺序是同步加载的;

```javascript
// 定义模块 area.js
function area(radius) {
  return Math.PI * radius * radius;
}
// 在这里写上需要向外暴露的函数、变量
module.exports = {
  area: area
}

// 引用自定义的模块时，参数包含路径
var math = require('./math');
math.area(2);
```

* `__dirname`代表当前模块文件所在的文件夹路径，`__filename`代表当前模块文件所在的文件夹路径+文件名，但是我们并没有直接定义 `module`、`exports`、`require`这些模块，以及 Node 的 API 文档中提到的`__filename`，`__dirname`。那么是从何而来呢？其实在编译的过程中，Node 对我们定义的 JS 模块进行了一次基础的包装：

```javascript
(function(exports, require, modules, __filename, __dirname)) {
  ...
})
```

* 这样我们便可以访问这些传入的`arguments`以及隔离了彼此的作用域。`CommonJS` 的一个模块，就是一个脚本文件。`require`命令第一次加载该脚本，就会执行整个脚本，然后在内存生成一个对象。

```javascript
{
  id: '...',
  exports: { ... },
  loaded: true,
  ...
}
```

* 以后需要用到这个模块的时候，就会到`exports`属性上面取值。即使再次执行`require`命令，也不会再次执行该模块，而是到缓存之中取值。commonJS用同步的方式加载模块，只有在代码执行到`require`的时候，才回去执行加载。在服务端，模块文件都存在本地磁盘，读取非常快，所以这样做不会有问题。但是在浏览器端，限于网络原因，更合理的方案是使用异步加载。

#### AMD
* AMD 是 `RequireJS` 在推广过程中对模块定义的规范化产出。AMD 规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。说了这么多，来看一下一个AMD规范的`RequireJS` 是如何定义的：

```javascript
// 定义 moduleA 依赖 a, b模块
define(['./a','./b'],function(a,b){
   a.doSomething()
   b.doSomething()
})

// 使用
require(['./moduleA'], function(moduleA) {
  // ...
})
```

#### CMD
* CMD 是 `SeaJS` 在推广过程中对模块定义的规范化产出。AMD 推崇依赖前置、提前执行，CMD推崇依赖就近、延迟执行。比如`require.js`在申明依赖的模块时会在第一之间加载并执行模块内的代码，而CMD则是在使用的时候就近定义：

```javascript
define(function(require, exports, module) {
  var a = require('./a')
  a.doSomething()
  var b = require('./b')
  b.doSomething()
})
```

* 代码在运行时，首先是不知道依赖的，需要遍历所有的`require`关键字，找出后面的依赖。具体做法是将`function` `toString`后，用正则匹配出`require`关键字后面的依赖。显然，这是一种牺牲性能来换取更多开发便利的方法。而 AMD 是依赖前置的，换句话说，在解析和执行当前模块之前，模块作者必须指明当前模块所依赖的模块。代码在一旦运行到此处，能立即知晓依赖。而无需遍历整个函数体找到它的依赖，因此性能有所提升，缺点就是开发者必须显式得指明依赖——这会使得开发工作量变大，比如：当你写到函数体内部几百上千行的时候，忽然发现需要增加一个依赖，你不得不回到函数顶端来将这个依赖添加进数组。

#### ES6 Module
* ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，旨在成为浏览器和服务器通用的模块解决方案。其模块功能主要由两个命令构成：`export`和`import`。`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

```javascript
import a from './a'
import b from './b'

a.doSomething()
b.doSomething()

function c () {}

export default c
```

* ES6 Modules不是对象，`import`命令会被 `JavaScript` 引擎静态分析，在编译时就引入模块代码，而不是在代码运行时加载，所以无法实现条件加载。也正因为这个，使得静态分析成为可能。

#### ES6 模块与 CommonJS 模块的差异
* CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用
 1. CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值。
 2. ES6 Modules 的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令import，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。换句话说，ES6 的 `import` 有点像 Unix 系统的“符号连接”，原始值变了，`import`加载的值也会跟着变。因此，ES6 模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在的模块。
* CommonJS 模块是运行时加载，ES6 模块是编译时输出接口
 1. 运行时加载: CommonJS 模块就是对象；即在输入时是先加载整个模块，生成一个对象，然后再从这个对象上面读取方法，这种加载称为“运行时加载”。
 2. 编译时加载: ES6 模块不是对象，而是通过 export 命令显式指定输出的代码，`import`时采用静态命令的形式。即在`import`时可以指定加载某个输出值，而不是加载整个模块，这种加载称为“编译时加载”
* CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。

> 模块化 CommonJS、AMD/CMD、ES6 Modules 出处：https://github.com/muwoo/blogs/issues/28
