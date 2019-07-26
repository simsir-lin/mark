#### 特别处理
 * -webkit-tap-highlight-color: rgba(0,0,0,0)  ——  去掉点击时出现的黑色背景
 * -webkit-user-select: none  ——  禁止用户进行选择（就是不出现复制那个菜单）
 * -webkit-touch-callout: none —— 长按禁止弹出浏览器默认会出现的菜单

#### font-family
 * font-family: -apple-system, BlinkMacSystemFont, "PingFang SC","Helvetica Neue",STHeiti,"Microsoft Yahei",Tahoma,Simsun,sans-serif;
 * 小米：font: 14px/1.5 "Helvetica Neue",Helvetica,Arial,"Microsoft Yahei","Hiragino Sans GB","Heiti SC","WenQuanYi Micro Hei",sans-serif;   小米公司优先使用Helvetica Neue这款字体以保证最新版本Mac用户的最佳体验，选择了Arial作为Win下默认英文字体及Mac的替代英文字体；中文字体方面首选了微软雅黑，然后选择了冬青黑体及黑体-简作为Mac上的替代方案；最后使用文泉驿微米黑兼顾了Linux系统。
 * 淘宝：font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;   其实从图中明显看出淘宝网的导航及内容有着大量的衬线字体，鉴于淘宝网站大部分字号比较小，显示效果也还可以接受。代码中可以看出淘宝使用了Tahoma、Arial作为首选英文字体，中文字体首选了冬青黑体，由于Win下没有预装该款字体，所以显示出了后面的宋体（5b8b4f53为汉字宋体用 unicode 表示的写法，不用SimSun是因为 Firefox 的某些版本和 Opera 不支持 SimSun的写法）
 * 简书：font-family: "lucida grande", "lucida sans unicode", lucida, helvetica, "Hiragino Sans GB", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;   自认为简书的阅读体验很棒，我们看看简书所用的字体，简书优先选择了lucida家族的系列字体作为英文字体，该系列字体在Mac和Win上都是预装的，并且有着不俗的表现；中文字体方面将冬青黑体作为最优先使用的字体，同样考虑了Linux系统。

 * 微软雅黑为Win平台上最值得选择的中文字体，但非游览器默认，需要设置；西文字体的选择以Arial、Tahoma等无衬线字体为主。

#### 伪类和伪元素
* 单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素

### Chrome、Safari等浏览器，当表单提交用户选择记住密码后，下次自动填充表单的背景变成黄色，影响了视觉体验是否可以修改？
```css
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
  background-color: #fff;//设置成元素原本的颜色
  background-image: none;
  color: rgb(0, 0, 0);
}
/* 方法2 */
input:-webkit-autofill {
    -webkit-box-shadow: 0px 0 3px 100px #ccc inset; //背景色
}
```

### 多行文本溢出显示...
```
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```
适用范围：因使用了WebKit的CSS扩展属性，该方法适用于WebKit浏览器及移动端；
1. -webkit-line-clamp 用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。常见结合属性：
2. display: -webkit-box; 必须结合的属性，将对象作为弹性伸缩盒子模型显示
3. -webkit-box-orient 必须结合的属性，设置或检索伸缩盒对象的子元素的排列方式


### 布局
#### 一边固定一边自适应
* flex：把外容器设为display:flex并指定宽度，给一个子容器指定一个宽度，那么另一个子容器的设置为flex:1;
* 标准的w3c标准提供了自适应宽度的标准方法。把外容器设为display:table并指定宽度，然后把左右两个子容器设为display:table-cell；然后只给一个子容器指定一个宽度，那么另一个子容器的宽度就变成自适应了。
* BFC

#### flex布局采用space-around这种方法，但是最后一行如何让他左对齐
* 后面添加空白占位元素

### 弹窗使用fixed布局
