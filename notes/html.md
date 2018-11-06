### 页面导入样式几种方法
* link标签引入，也是当下用的最多的一种方式，它属于XHTML标签，除了能加载css外，还能定义rel、type、media等属性
* @import引入，@import是CSS提供的，只能用于加载CSS
* style 嵌入方式引入，减少页面请求(优点)，但只会对当前页面有效，无法复用、会导致代码冗余，不利于项目维护(缺点)，此方式一般只会项目主站首页使用（腾讯、淘宝、网易、搜狐）等大型网站主页，之前有看到过都是这种方式，但后来有些也舍弃了
* 小结：link页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载,且link是XHTML标签，无兼容问题; link支持动态js去控制DOM节点去改变样式，而@import不支持

### cookies，sessionStorage 、 localStorage
* cookie是网站为了标示用户身份而储存在用户本地终端上的数据（通常经过加密），cookie数据始终在同源的http请求中携带，会在浏览器和服务器间来回传递
* sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存
* 大小： cookie数据大小不能超过4k,sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大
* 时效：localStorage 存储持久数据，浏览器关闭后数据不丢失除非用户主动删除数据或清除浏览器/应用缓存；sessionStorage 数据在当前浏览器窗口关闭后自动删除。cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
* 如何让cookie浏览器关闭就失效？——不对cookie设置任何正、负或0时间的即可
* sessionStorage在浏览器多窗口之间 (同域)数据是否互通共享? ——不会，都是独立的，localStorage会共享
