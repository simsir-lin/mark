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

### 模块化 CommonJS、AMD/CMD、ES6 Modules
#### CommonJS
* Node.js是`commonJS`规范的主要实践者，它有四个重要的环境变量为模块化的实现提供支持：`module`、`exports`、`require`、`global`。实际使用时，用module.exports定义当前模块对外输出的接口，用`require`加载模块。

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

* 但是我们并没有直接定义 `module`、`exports`、`require`这些模块，以及 Node 的 API 文档中提到的`__filename`，`__dirname`。那么是从何而来呢？其实在编译的过程中，Node 对我们定义的 JS 模块进行了一次基础的包装：

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
