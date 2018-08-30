### 注意事项
* setData 最大1m

### 音频
* 权限判断
* 录音和播放音频的情况下 切换后台+锁屏都会触发暂停事件（onPause）
* 录音时超过限制的时长是不会触发Error事件只会触发Stop事件

### 小程序自动化构建设计
* 必须实现功能
  1. 新增预处理样式文件scss，将 px 单位转换为 rpx 单位，插件 postcss-px2units，修改文件后缀名为 .wxss 输出
  2. ESLint检查语法错误 （必须分号结束）
  3. 资源自动上传到cdn，并替换开发时引用的路径
  4. 压缩js
  5. 可切换为mock环境
  6. 可实现开发模式下在微信开发者工具中实时预览
  7. 构建时不构建mock文件


* 考虑实现功能
  1. 支持mixins
  2. ...


* 项目目录
```
├─project                项目目录
  ├─src                  开发目录
  ├─dist                 构建目录（小程序开发者工具添加项目路径）
  ├─gulp                 gulp脚本
    ├─build.js
    ├─config.js
    ├─....
  ├─package.json         npm配置文件
  ├─gitignore            git忽略文件
  ├─gulpfile.js          gulp主脚本
  ├─eslintrc             eslint配置
  ├─....
```

* src开发目录
```
├─src                    开发目录
  ├─mock                   数据模拟
    ├─index.js
  ├─js                   共用js
    ├─config.js
    ├─const.js
  ├─images               图片资源（小程序限制的本地资源）
  ├─resource             需要上传至 CDN 的资源文件
  ├─utils                工具集
    ├─lib                第三方类库
    ├─date.js
    ├─proxy.wxs
    ├─....
  ├─components         组件
    ├─dialog           弹窗组件
  ├─pages                小程序页面
    ├─index              首页
      ├─index.wxml
      ├─index.js
      ├─index.json
      ├─index.scss
    ├─login              登录页
    ├─....
  ├─app.js               入口文件
  ├─app.json             配置文件
  ├─app.scss             主 CSS 文件...
```

* dist构建目录
```
├─dist                   构建目录
  ├─js                   共用js
  ├─lib                  第三方类库
  ├─images               图片资源（小程序限制的本地资源）
  ├─utils                工具集
  ├─components           组件
    ├─dialog             弹窗组件
  ├─pages                小程序页面
    ├─index              首页
      ├─index.wxml
      ├─index.js
      ├─index.json
      ├─index.wxss
    ├─login              登录页
    ├─....
  ├─app.js               入口文件
  ├─app.json             配置文件
  ├─app.wxss             主 CSS 文件...
```
