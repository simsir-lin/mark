#### html5mode开启
1. `$locationProvider.html5Mode({
  enabled: true,
  requireBase: false
});`
2. 在首页html中添加 `<base href="/" />`

#### 设置超链接安全名单
* `$compileProvider.aHrefSanitizationWhitelist(/^\s*(mailto|mqq|http|https):/);`
