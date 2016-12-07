JQ选择器
JQUERY找无规律元素文本的办法
具有限定子节点选择器:$("mix1[mix2]"):返回包含mix2的mix1节点.如:$("div[a]"):包含a标签的div.
这个和$("div a")不相同.后者表示div中的a标签,返回的是a标签对象,前者返回的是div标签对象
冒号限定结点选择器:$("mix:condition"):mix标签,并且满足限定条件.
E:root:类型为E,并且是文档的根元素
E:nth-child(n):是其父元素的第n个类型为E的子元素 ,基数从1开始
E:first-child:是其父元素的第1个类型为E的子元素
E:last-child:是其父元素的最后一个类型为E的子元素
E:only-child:且是其父元素的唯一一个类型为E的子元素
E:empty:没有子元素（包括text节点）的类型为E的元素
E:enabled
E:disabled:类型为E,允许或被禁止的用户界面元素
E:checked:类型为E,处于选中状态的用户界面元素（例如单选按钮或复选框）
E:visible:选择所有可见元素(display值为block或visible,visibility值为visible元素,不包括hide域)
E:hidden:选择所有隐藏元素(非Hide域,且display值为block或visible,visibility值为visible的元素)
E:not(s):类型为E,不匹配选择器s
E:eq(n),E:gt(n),E:lt(n):元素限定
E:first:相当于E:eq(0)
E:last:最后一个匹配的元素
E:even:从匹配的元素集中取序数为偶数的元素
E:odd:从匹配的元素集中取序数为奇数的元素
E:parent:选择包含子元素（包含text节点）的所有元素
E:contains('test'):选择所有含有指定文本的元素
表单选择器:
E:input:选择表单元素(input,select,textarea,button)
E:text:选择所有文本域(type="text")
E:password:选择所有密码域(type="password")
E:radio:选择所有单选按钮(type="radio")
E:checkbox:选择所有复选框(type="checkbox")
E:submit:选择所有提交按钮(type="submit")
E:image:选择所有图像域 (type="image")
E:reset:选择所有清除域(type="reset")
E:button:选择所有按钮(type="button")
当然包括E:hidden

8.xPath路径查询:

先介绍下xPath的语法:
/:选取根节点
//:选取文档中所有符合条件的节点,不管该节点位于何处
.:选取当前节点
..:选取单前节点的父节点
@:选取属性,这个在之前说过了(属性选择器)
nodename:选取节点下的所有节点
jQuery中的应用:
根节点是很少用到的,常用的如下面的例子:
$("div/p")相当于$("div>p")
$("div//p")相当于$("div p")
$("//div/../p"):所有div节点的父节点下的p标签
还有相对路径的写法以及支持的Axis选择器,还不是会应用,不介绍了...已经一大堆了

$的其他用法:

$(html节点):根据提供的原始HTML标记字符串,动态创建由jQuery对象包装的DOM元素.如:
$("Hello").appendTo("#body");//把Hello添加到body元素中
$(document):网页文档对象
$(document.body):网页body对象,和$("body")是一样的
$(函数):DOM载入后就执行该函数.所以$(document).ready()可以写做$()
$(选择器部分,选择器来源):这个举例说明
$("input:radio",document.forms[0]):在文档的第一个表单中,搜索所有单选按钮
$("div",xml.responseXML):查询指定XML文档中的所有div元素
选择器来源可以是:作为上下文的DOM元素,文档或jQuery对象
还有两个:$.extend(prop)和$.noConflict()是和插件以及和其他库兼容的使用,以后再写

下拉框,单选框,多选框整理

 1,下拉框:
var cc1  = $(".formc select[@name='country'] option[@selected]").text(); //得到下拉菜单的选中项的文本(注意中间有空格)
var cc2 = $('.formc select[@name="country"]').val();  //得到下拉菜单的选中项的值
var cc3 = $('.formc select[@name="country"]').attr("id"); //得到下拉菜单的选中项的ID属性值
$("#select").empty();//清空下拉框//$("#select").html('');
$("1111").appendTo("#select")//添加下拉框的option
稍微解释一下:
1.select[@name='country'] option[@selected] 表示具有name 属性，
并且该属性值为'country' 的select元素 里面的具有selected 属性的option 元素；
可以看出有@开头的就表示后面跟的是属性。

2,单选框:
$("input[@type=radio][@checked]").val();  //得到单选框的选中项的值(注意中间没有空格)
$("input[@type=radio][@value=2]").attr("checked",'checked'); //设置单选框value=2的为选中状态.(注意中间没有空格)

3,复选框:
$("input[@type=checkbox][@checked]").val(); //得到复选框的选中的第一项的值
$("input[@type=checkbox][@checked]").each(function(){ //由于复选框一般选中的是多个,所以可以循环输出
  alert($(this).val());
  });

$("#chk1").attr("checked",'');//不打勾
$("#chk2").attr("checked",true);//打勾
if($("#chk1").attr('checked')==undefined){} //判断是否已经打勾



1.判断select选项中 是否存在Value="paraValue"的Item
$("#selectid option[@value='paraValue']").length>0
2.向select选项中 加入一个Item
$("#selectid").append("<option value=''>1111<option>");
3.从select选项中 删除一个Item
$("#selectid").remove("<option value=''>1111<option>");
4.修改select选项中 value="paraValue"的text为"paraText"
$("#selectid option:selected").attr("value","paraValue").attr("text","paraText");
5. 设置select中text="paraText"的第一个Item为选中
$("#selectid option[@text='paraText']").attr("selected","true")
6.设置select中 value="paraValue"的Item为选中
$("#selectid option[@value='paraValue']").attr("selected","true")

7.设置select中第一 个Item为选中
$("#selectid option").eq(0).attr('selected', 'true');

8. 得到select的当前选中项的value
$("#selectid").val();
9.得到select的当前选中项的text
$("#selectid").text();
10. 得到select的当前选中项的Index
document.getElementById("select1").selectedIndex;
$("#selectid").get(0).selectedIndex
11. 清空select的项
$("#selectid").empty();

$('#isanonymous').is(':checked');    //判断是否勾选




基本选择器：

　　#id　　　　　　　　　　　　根据Id匹配一个元素

　　.class　　　　　　　　　　  根据给定的类名匹配一个元素

　　element　　　　　　　　　  根据元素名匹配一个元素

　　*　　　　　　　　　　　　　匹配所有元素

　　selecttor1,selector2　　　  并集，返回两个选择器匹配到的元素

层次选择器：

　　ancestor descendant　　　根据祖先匹配所有的后代元素

　　parent>child　　　　　　　 根据父元素匹配所有的子元素，直接后代

　　prev+next　　　　　　　　 匹配下一个兄弟元素 相当于next()方法

　　prev~siblings　　　　　　   匹配后面的兄弟元素 相当于nextAll()方法     siblings()方法为匹配所有的兄弟元素

简单过滤选择器：

　　:first或first()　　　　　　　 匹配第一个元素

　　:last或last()　　　　　　  　匹配最后一个元素

　　:not(selector)　　　　　　  匹配非selector能匹配到的元素

　　:even　　　　　　　　　　  匹配索引值为偶数的元素，索引号从0开始

　　:odd　　　　　　　　 　　　匹配索引值为奇数的元素，索引号从0开始

　　:eq(index)　　　　　 　　　匹配指定索引号的元素，索引号从0开始

　　:gt(index)　　　　　  　　　匹配索引号大于给定索引值的元素，索引号从0开始

　　:lt(index)　　　　　　  　　 匹配索引号小于给定索引值的元素，索引号从0开始

　　:header　　　　　　　　　　匹配所有的标题元素  h1 h2 h3 h4 h5 h6

　　:animated　　　　　　　　  匹配所有正在执行动画的元素

内容过滤选择器：

　　:contains(text)　　　　　　匹配包含给定文本的元素

　　:empty　　　　　　　　　　匹配所有不包含子元素或者文本的空元素

　　:has(selector)　　　　　　  匹配后代中含有selector能匹配上元素的元素

　　:parent　　　　　　　　　　匹配含有子元素或者文本的元素

可见性过滤选择器：

　　:hidden　　　　　　　　　　匹配不可见元素，或者type="hidden"的元素　含有css样式:display:"none";的元素，无论CSS是内联，导入，链接式

　　:visible　　　　　　　　　　 获取所有的可见元素

属性过滤选择器：

　　[attribute]　　　　　　　　 匹配含有给定属性的元素

　　[attribute=value]　　　　   匹配含有属性=value的元素

　　[attribute!=value]　　　　  匹配含有属性但!=value的元素

　　[attribute^=value]　　　　 匹配属性值是以value开始的元素

　　[attribute$=value]　　　　  匹配属性值是以value结束的元素

　　[attribute*=value]　　　　  匹配属性值包含某些值的元素，部分前后，中间有也算

　　[selector][selector]　　　　 匹配属性选择器的交集

子元素过滤选择器：

　　:nth-child(eq|even|odd|index)　　获取所有父元素特定位置的子元素

　　:first　　　　　　　　　　　 获取所有父元素下的第一个子元素

　　:last　　　　　　　　　　　 获取所有父元素下最后一个子元素

　　:only-child　　　　　　　　 获取所有父元素下唯一的一个元素

表单对象属性过滤选择器：

　　:enabled　　　　　　　　    获取表单中所有可用的元素

　　:disabled　　　　　　　　　 获取表单中所有不可用的元素

　　:checked　　　　　　　　　获取表单张所有被选中的元素

　　:selected　　　　　　　　   获取表单中所有被选中的option的元素

表单选择器：

　　:input　　　　　　　　　　 获取所有的表单元素<input开头的，还有textarea select

　　:text　　　　　　　　　　   获取所有的单行文本框　　<input type="text" />

　　:password　　　　　　　　获取所有的密码框元素      <input type="password" />

　　:radio　　　　　　　　　　 获取所有的单选按钮　　　<input type="radio" />

　　:checkbox　　　　　　　　 获取所有的复选框　　　　<input type="checkbox">

　　:submit　　　　　　　　　 获取所有的提交按钮　　　<input type="submit" />

　　:image　　　　　　　　　　获取所有的图像按钮　　 <input type="image" />

　　:reset　　　　　　　　　　获取所有的重置按钮　　　 <input type="reset" />

　　:button　　　　　　　　    获取所有的按钮　　　　　<input type="button">

　　:file　　　　　　　　　　　 获取所有的文件上传框　　<input type="file" />
