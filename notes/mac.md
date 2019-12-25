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


#### git 分支显示、自动补全
 * 下载本地git对应版本的 `git-completion.bash` 和 `git-prompt.sh`
 ```bash
 curl -O https://raw.githubusercontent.com/git/git/v2.23.0/contrib/completion/git-completion.bash
curl -O https://raw.githubusercontent.com/git/git/v2.23.0/contrib/completion/git-prompt.sh
 ```
 * 移动git-completion.bash、git-prompt.sh到～目录下
 * cd ~/ , vi .bash_profile
 ```bash
 # Prompt
 red='\[\033[0;31m\]'
 brown='\[\033[0;33m\]'
 ubrown='\[\033[4;33m\]'
 green='\[\033[0;32m\]'
 lblue='\[\033[1;34m\]'
 blue='\[\033[0;34m\]'
 purp='\[\033[0;35m\]'
 cyan='\[\033[0;36m\]'
 nocol='\[\033[0m\]'

 # workstation prompt
 PSW="[$brown\u$nocol@$brown\h$nocol:$purp\w$nocol] "

 # server prompt
 PSS="[$lblue\$(date +%H:%M)$nocol][$brown\u$nocol@$ubrown\h$nocol:$purp\w$nocol] "

 # standard prompt
 if [ -f "$HOME/.git-prompt.sh" ]; then
   . "$HOME/.git-prompt.sh"
   PSW="[$brown\u$nocol@$brown\h$nocol:$purp\w$nocol]$green\$(__git_ps1)$nocol "
   PSS="[$lblue\$(date +%H:%M)$nocol][$brown\u$nocol@$brown\h$nocol:$purp\w$nocol]$green\$(__git_ps1)$nocol "
 fi

 export PS1=$PSW

 if [ -f "$HOME/.git-completion.sh" ]; then
   . "$HOME/.git-completion.sh"
 fi

 source ~/.git-completion.bash
 ```

#### 深色模式
* 打开终端，输入指令：`defaults write -g NSRequiresAquaSystemAppearance -bool Yes`，让你只将菜单栏和程序坞使用深色模式，而其他保持浅色模式不变。注销并重新登录
* 如果你想恢复成系统的深色模式，那么在终端输入defaults delete -g NSRequiresAquaSystemAppearance，再注销并重新登录即可

#### iterm2
* SF Mono 字体
```bash
cd /Applications/Utilities/Terminal.app/Contents/Resources/Fonts/`, `cp *.otf ~/Library/Fonts/`
```
* 颜色配置
```bash
git clone https://github.com/dracula/iterm.git
```