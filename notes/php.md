#### Header
* header("Refresh:3;url=register.php") -- 3秒后自动跳转到register.php, header前面不能有输出(echo, var_dump)
* header("location:../index.php") -- 跳转到上级页面的index
* header("Access-Control-Allow-Origin: \*") -- 允许其它所有网站请求,允许跨域
* header("content-type:text/html;charset=utf8") -- 设置中文
* <meta http-equiv="refresh" content="10; /> -- 定时刷新

#### 变量
* 只有int和float两种数字类型
* define(key, value) -- 常量
* global variable -- 全局是对一个变量的引用或定义，但是不能直接赋值，如果外面有的就是引用，没有就是定义
* static variable = value -- 静态变量，一旦被定义赋值，就一直在内存中了
* 可变变量，$name = '你好';  $temp = 'name'; echo $$temp; -- 输出  '你好'
* 引用变量赋值，在赋值的时候前面加&
* 函数引用传值，在参数前加&

#### 文件
* 文件上传：表单添加enctype=”multipart/form-data”
* php上传文件时会先把文件放在一个临时文件夹里，等到脚本结束就删除文件
* 上传的文件信息会存在$\_FILES, 里面是一个二维数组, 一维数组的字符索引是表单的名字, 二维数组里有["name"]用户本地文件名，["type"]文件mime类型(image/jpg)，["tmp_name"]文件上传到临时目录的文件名，包含路径，还有["error"]和["size"]
* 移动文件：Move_uploaded_file(原目录，目标)  
* require(文件相对路径)   include(文件相对路径) -- 两个都是连接(包含)php文件，区别：只有出错时处理的方式不一样，其他都一样
* include -- 如果包含的文件中存在错误代码，包含进来后，会输出一个“警告错误信息”，但程序会继续向下运行
* require -- 如果包含的文件中存在错误代码，包含进来后，会输出一个“致命错误信息”，但程序不会继续向下运行

#### 数组
* $arr["name"] = "linhaoyu"; -- 直接声明arr数组并为key为name赋值linhaoyu
* 字符串下标跟数值下标的索引值不是同一个索引值
* $arr[] = 'simsir' -- 直接给数组的最大的数值索引+1的那个位置赋值

#### 数据库
* mysql_connect(ip，username，pwd); -- 连接成功就返回资源标识，连接失败返回false
* mysql_select_db(db_name, [连接资源]) -- 返回值bool，如果没有连接资源参数，则拿上一次连接成功的资源
* mysql_query(sql语句) -- 返回资源标识符
* mysql_fetch_row(query返回资源) -- 返回一行索引数组
* mysql_fetch_array(query返回资源) -- 返回一行索引和字符数组
* mysql_num_rows(资源) -- 取得资源的行数
* mysql_fetch_assoc(query返回资源) -- 返回一行字符数组

#### Common
* php以秒为单位 date('Y/m/d H:i:s',time())
* Array_walk_recursive(数组，方法名) -- 对数组的每个值进行调用传入的方法
* addslashes() -- 对字符串中的特殊符号进行转义（防sql注入）

#### Tips
* 单引号运行比较快
* if(1)进得去if的
* $str = <<<text  大量字符串   text
* === 比较的不只是值还有类型要相等
* 函数前加@可以忽略错误。不报错
