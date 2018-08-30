### 笔记
* 电子书：http://webpack.wuhaolin.cn
* webpack就是把入口文件(entry.js)执行一遍，识别出源码中的模块化导入语句， 递归的寻找出入口文件的所有依赖，把入口和其所有依赖打包到一个单独的文件中。过程中通过配置好的Loader去解析依赖文件类型后导入，而Plugin在 Webpack 构建流程中的特定时机注入扩展逻辑来改变构建结果或做你想要的事情。

* 想让源文件加入到构建流程中去被 Webpack 控制，配置 entry。
* 想自定义输出文件的位置和名称，配置 output。
* 想自定义寻找依赖模块时的策略，配置 resolve。
* 想自定义解析和转换文件的策略，配置 module，通常是配置 module.rules 里的 Loader。
* 其它的大部分需求可能要通过 Plugin 去实现，配置 plugin。
