### 注意点
* v-on:click.stop 可以阻止点击事件继续传播
* 计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数
* 当 v-bind:style 使用需要添加浏览器引擎前缀的 CSS 属性时，如 transform，Vue.js 会自动侦测并添加相应的前缀。
* v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
* 注意在 JavaScript 中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。

### 接入微信
* 分享接口的link参数需要encodeURIComponent
* 所有域名都应该在公众号的白名单中

### 组件类型
* 纯展示：数据进，dom出
* 业务型（接入型）：通过serve层获取数据，修改数据源，数据再往下传递
* 交互型：通用的交互逻辑，比如form表单
* 功能型：抽象逻辑类组件，作为扩展，比如router

### 代码
* 剪贴板

```javascript
  <input type="text" v-model="clipboardText" ref="clipboard">

  export default {
    data() {
      return {
        clipboardText: ''
      }
    },
    methods: {
      copyToClipboard(text) {
        this.clipboardText = text
        // $nextTick 在这里没用
        setTimeout(() => {
          this.$refs.clipboard.select()
          document.execCommand('Copy')
        })
      }
    }
  }
```
