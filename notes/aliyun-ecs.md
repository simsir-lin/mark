#### 准备
1. yum update

#### nginx
1. 安装nginx源（要注意系统去选择源，这里是centos7版本）： yum localinstall http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
2. yum install nginx
3. service nginx start
4. 访问http://IP测试（项目地址/usr/share/nginx/html）

#### mysql
1. 安装mysql源(要注意系统去选择源，这里是centos7版本): yum localinstall 源地址(可上mysql官网获取)
2. yum install mysql-community-server
3. yum install mysql-community-devel
4. service mysqld start
5. mysql -uroot -p
6. 修改root初始密码

#### php
1. 下载php源码包：wget 下载地址(可上php官网获取)
2. 解压：tar -xvf 下载的包名
3. 进入目录
4. 配置(设置php主目录,php.ini位置,开启fpm)：~~./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc/ --enable-fpm~~
``` javascript
./configure \
--prefix=/usr/local/php \
--with-config-file-path=/usr/local/php/etc/ \
--enable-fpm \
--with-fpm-user=nginx  \
--with-fpm-group=nginx \
--enable-inline-optimization \
--disable-debug \
--disable-rpath \
--enable-shared  \
--enable-soap \
--with-libxml-dir \
--with-xmlrpc \
--with-openssl \
--with-mcrypt \
--with-mhash \
--with-pcre-regex \
--with-sqlite3 \
--with-zlib \
--enable-bcmath \
--with-iconv \
--with-bz2 \
--enable-calendar \
--with-curl \
--with-cdb \
--enable-dom \
--enable-exif \
--enable-fileinfo \
--enable-filter \
--with-pcre-dir \
--enable-ftp \
--with-gd \
--with-openssl-dir \
--with-jpeg-dir \
--with-png-dir \
--with-zlib-dir  \
--with-freetype-dir \
--enable-gd-native-ttf \
--enable-gd-jis-conv \
--with-gettext \
--with-gmp \
--with-mhash \
--enable-json \
--enable-mbstring \
--enable-mbregex \
--enable-mbregex-backtrack \
--with-libmbfl \
--with-onig \
--enable-pdo \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-zlib-dir \
--with-pdo-sqlite \
--with-readline \
--enable-session \
--enable-shmop \
--enable-simplexml \
--enable-sockets  \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--enable-wddx \
--with-libxml-dir \
--with-xsl \
--enable-zip \
--enable-mysqlnd-compression-support \
--with-pear \
--enable-opcache
```
5. make && make install
6. 添加 PHP 命令到环境变量: vi /etc/profile,在末尾加入PATH=$PATH:/usr/local/php/bin换行export PATH, 使立即生效 #source /etc/profile, 测试：php -v
7. 配置php-fpm: cp php.ini-production /usr/local/php/etc/php.ini
8. cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
9. cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
10. cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
11. 添加执行权限: chmod +x /etc/init.d/php-fpm
12. 启动fpm: /etc/init.d/php-fpm start

#### 配置nginx连接php
1. vi /etc/nginx/conf.d/nginx.conf
2. 以下配置
``` javascript
server{
    listen 80;
    server_name  php7.aaa.com;
    root /var/www/html/php7.aaa.com; # 该项要修改为你准备存放相关网页的路径
    location / {
        index  index.php index.html index.htm;
         #如果请求既不是一个文件，也不是一个目录，则执行一下重写规则
         if (!-e $request_filename)
         {
            #地址作为将参数rewrite到index.php上。
            rewrite ^/(.*)$ /index.php/$1;
            #若是子目录则使用下面这句，将subdir改成目录名称即可。
            #rewrite ^/subdir/(.*)$ /subdir/index.php/$1;
         }
    }
    #proxy the php scripts to php-fpm
    location ~ \.php {
            include fastcgi_params;
            ##pathinfo支持start
            #定义变量 $path_info ，用于存放pathinfo信息
            set $path_info "";
            #定义变量 $real_script_name，用于存放真实地址
            set $real_script_name $fastcgi_script_name;
            #如果地址与引号内的正则表达式匹配
            if ($fastcgi_script_name ~ "^(.+?\.php)(/.+)$") {
                    #将文件地址赋值给变量 $real_script_name
                    set $real_script_name $1;
                    #将文件地址后的参数赋值给变量 $path_info
                    set $path_info $2;
            }
            #配置fastcgi的一些参数
            fastcgi_param SCRIPT_FILENAME $document_root$real_script_name;
            fastcgi_param SCRIPT_NAME $real_script_name;
            fastcgi_param PATH_INFO $path_info;
            ###pathinfo支持end
        fastcgi_intercept_errors on;
        fastcgi_pass   127.0.0.1:9000;
    }    
}
```
3. 重启nginx: service nginx reload
