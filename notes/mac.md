#### Safari插件
 * mama2 —— 转html5播放(http://zythum.github.io/mama2/)
 * Stylish -- 给某些特定的网站配置样式
 * Adblock Plus —— 去广告

#### 技巧
 * control + command + 空格 —— 调出emoji表情
 * Command + L —— 快速跳到地址栏
 * 比如“肏”这个字不知道，输入“ru rou”，按shift＋空格，就会出现“肏”这个字的拼音
 * 在终端的命令行里输入"open ."，会用Finder打开当前目录
 * command + shift + . —— 显示隐藏文件

#### 命令
 * U盘在 /Volumes 目录下

#### 源码安装nginx
 * 下载 Nginx 源码包：[Nginx 1.14.0](http://nginx.org/en/download.html)
 * 下载编译选项中的依赖包：[zlib](http://zlib.net), [pcre](http://www.pcre.org)，[openssl](https://www.openssl.org/source/)
 * 解压源码包：tar zxvf xxx.tar.gz
 * 编译安装 Nginx
   * 这里会将各依赖的源码编译进 Nginx, 所以 --with-zlib 和 --with-pare 后为对应的依赖源码目录路径。此外, 编译选项中还开启了 HTTPS 的协议支持 --with-http_ssl_module, 若不需要 HTTPS, 可取消该选项

   ```
   ./configure --prefix=/usr/local/nginx --with-zlib=../zlib-1.2.11 --with-pcre=../pcre-8.32 --with-http_ssl_module --with-openssl=../openssl-1.1.0h
   ```

  * make  
  * sudo make install

 * 安装目录： /usr/local/nginx
 * 启动：sudo sbin/nginx，浏览器访问 127.0.0.1 测试是否成功启动
 * 重启：sudo sbin/nginx -s reload
 * 停止：sudo sbin/nginx -s stop
