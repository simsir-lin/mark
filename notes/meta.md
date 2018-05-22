### 概要
* meta标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。
* content属性：定义与http-equiv或name属性相关的元信息，必填
* http-equiv属性：	content-type / expire / refresh / set-cookie	把content属性关联到HTTP头部。
* name属性：author / description / keywords / generator / revised / others	把 content 属性关联到一个名称。

### SEO优化
* 关键词，不应超过 874 个字符
```html
<meta name="keywords" content="your tags" />
```
* 页面描述，每个网页都应有一个不超过 150 个字符且能准确反映网页内容的描述标签
```html
<meta name="description" content="150 words" />
```
* 搜索引擎索引方式
```html
<meta name="robots" content="index,follow" />
<!--
    all：文件将被检索，且页面上的链接可以被查询；
    none：文件将不被检索，且页面上的链接不可以被查询；
    index：文件将被检索；
    follow：页面上的链接可以被查询；
    noindex：文件将不被检索；
    nofollow：页面上的链接不可以被查询。
 -->
```
* 页面重定向和刷新：content内的数字代表时间（秒），既多少时间后刷新。如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）
```html
<meta http-equiv="refresh" content="0;url=" />
```

### 移动设备
* viewport：能优化移动浏览器的显示。如果不是响应式网站，不要使用initial-scale或者禁用缩放。
```html
<meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
<!--
width：宽度（数值 / device-width）（范围从200 到10,000，默认为980 像素）
height：高度（数值 / device-height）（范围从223 到10,000）
initial-scale：初始的缩放比例 （范围从>0 到10）
minimum-scale：允许用户缩放到的最小比例
maximum-scale：允许用户缩放到的最大比例
user-scalable：用户是否可以手动缩 (no,yes)
-->
```
* WebApp全屏模式：伪装app，离线应用
```html
<!-- 启用 WebApp 全屏模式 -->
<meta name="apple-mobile-web-app-capable" content="yes" />
<!-- 隐藏状态栏/设置状态栏颜色：只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent -->
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<!-- 添加到主屏后的标题 -->
<meta name="apple-mobile-web-app-title" content="标题">
<!-- 忽略数字自动识别为电话号码 -->
<meta content="telephone=no" name="format-detection" />
<!-- 忽略识别邮箱 -->
<meta content="email=no" name="format-detection" />
<!-- 添加智能 App 广告条 Smart App Banner：告诉浏览器这个网站对应的app，并在页面上显示下载banner -->
<!-- 详细文档：https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html -->
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
```
* 其他功能
```html
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
```

### 网页相关
* 申明编码
```html
<meta charset='utf-8' />
```
* 优先使用 IE 最新版本和 Chrome
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 关于X-UA-Compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->
<meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 使用IE7 -->
<meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->
```
* 浏览器内核控制：国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器选择何种内核渲染
```html
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```
