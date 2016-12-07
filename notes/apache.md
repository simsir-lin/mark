#### windows
1. C:/Windows/System32/drivers/etc/hosts
2. 安装Apache后,配置文件中默认的servername会被注释,需要去掉注释,如果安装的时候输入的域名是localhost就不会出现问题。修改配置文件的Directory,添加Allow from all
3. apache默认的网站根目录 htdocs
4. apache需要加载php才能解析php，要通过修改apache配置文件httpd.conf
插入：LoadModule php5_module "D:/server/php/php5apache2_2.dll"
addType application/x-httpd-php .php
5. php有自己的配置文件，不过需要自己指定路径，不然就放在C:/Window(不安全)
有两个php.ini，一个是开发环境，一个是生产环境，将所需要的环境复制一份，把后戳删掉就可以了，
6. 回到Httpd.conf添加：PHPIniDir "D:/server/php"
7. php还需要跟mysql关联：
在php的配置文件php.ini，查找extension，找到php与mysql的关系，把前面的；去掉，这是注释
因为默认的扩展文件的目录是找不到，要配置扩展路径：extension_dir = "D:/server/php/ext"；
8. 还有一个时区的问题：在php.ini文件找，找到一个属性date.timezone，让它等于PRC
9. 如果配置虚拟主机，localhost会被虚拟主机覆盖掉，如果想继续使用localhost就继续添加一个localhost的虚拟主机

#### 虚拟机
