# Sass基础

## 1、Sass安装

直接使用yarn安装包

> `yarn global add sass`

可以使用`sass -v`检测是否安装成功



## 2、SCSS文件转化为CSS文件

在终端输入

> `sass sass/style.scss:css/style.css`





## 3、自动编译SASS

每次修改SASS都要重新编译转换一遍css十分不方便，可以使用wath 监视sass目录

> sass --watch （scss所在目录）:（css所在目录）
>
> 如:`sass --watch sass:csss`





## 4、CSS嵌套模式

* nested ， 嵌套
* compact ，紧凑
* expanded ， 扩展
* compressed ， 压缩

使用方法：

> sass --watch sass:csss --style compact





## 5、变量

在SASS中可以定义变量，定义变量需要使用$开头

> 如：&first-color = #0000e0;

变量可以在其他地方被调用。





## 6、嵌套套用父选择器

 若选择器，如hover嵌套在子类中，输出会变成 子类 :hover，但若想使用父类作为

调用选择器，则需要在:hover前加个&表示父选择器。

> ```
> .nav {
> 	height:200px;
> 	a {
> 		display:block;
> 		:hover{
> 		
> 		}
> }
> ```
>
> 结果会变成.nav a :hover{}，这时是a在调用hover。
>
> 在:hover前加&会将调用对象变为父级。
>
> ```
> .nav {
> 	height:200px;
> 	a {
> 		display:block;
> 		&:hover{
> 		
> 		}
> }
> ```
>
> 结果为：.nav a:hover{}，此时是nav在调用hover。



## 7、属性嵌套

属性如font  bord会有许多子类属性，如font-size等，

使用属性嵌套，可以直接在父属性中添加子属性，

> ```
> font{
> 	size:12px;
> 	color:red;
> }
> ```
>
> 






## 8、mixin

### 定义方式

SASS中定义好的样式，类似于function(){}函数

> @mixin 名字（参数1，参数2...）{
>
> }

使用方法，.定义名字-定义名字{}

> .print-picture{}

@include + 定义的名字

> .print-picture{
>
> ​		@include print;
>
> }
>
> 

输出结果：

```
.print-picture{
	XXX//@mixin中写的内容
}
```

### 参数

参数的定义也需要使用$开头

参数调用也和function函数类似

>  @mixin test($text-color,$background){
>
>   color: $text-color;
>
>   background:$background;
>
> }
>
> 
>
> .test-maintain{
>
> ​	@include test(#000001,#000002); 
>
> }





## 9、继承

使用@extend继承

> ```
> .test{
>     border: 10px;
> }
> 
> .test-info{
>     @extend .test;
>     background-color: aqua;
> }
> ```

继承的属性会在群组选择器之中

结果：

> ```
> .test, .test-info {
>   border: 10px;
> }
> 
> .test-info {
>   background-color: aqua;
> }
> ```
>
> 





## 9、import和Partials

SASS中的import可以在一个SASS文件中将所有的SASS包含进来，然后编译成

一个css文件。实现方法是将一个项目的样式分割个多个小的css文件，这种小部分

的css文件称为partials（以_为开头）

创建partials文件，_base.scss

> ```
> body{
>     height: 10px;
>     width: 20px;
> }
> ```



在主scss中导入_base.scss

> ```
> @import "base";
> .test{
>     border: 10px;
> }
> 
> .test-info{
>     @extend .test;
>     background-color: aqua;
> }
> ```



结果：

> ```
> body {
>   height: 10px;
>   width: 20px;
> } //导入的partial模块
> 
> .test, .test-info {
>   border: 10px;
> }
> 
> .test-info {
>   background-color: aqua;
> }
> 
> ```



## 10、数据类型

可以在终端中输入sass-i，这样可以直接在终端进行简单的代码调试。

> type-of()  可以判断数据类型

### 数字

在SASS中，除了基本的数字以外，带单位的数字，如5px，也会定义为数字。

且进行数字运算时，也可以带上单位。

PS：除法运算需要带上括号，否则会保留原有的样式。如：（10/2）=> 5  ， 10 / 2=>10 /2

一些常用的数字函数：

> `abs()`//求绝对值
>
> `round()`//四舍五入
>
> `ceil()`//进位
>
> `floor()`//退位
>
> `percentage()`//百分比化
>
> `min()`//最小值
>
> `max()`//最大值



### 字符串

字符串加上任意数据类型会变为字符串

> ni + "hao" => "nihao"

"-"会将两边相连

> ni - hao => ni-hao

基本函数

> `to-upper-case(字符串)`//变大写
>
> `to-lower-case(字符串)`//变小写
>
> `str-length()`//求字符串长度
>
> `str-index(字符串1,字符串2)`//求第二个字符串在第一个字符串所处位置
>
> `str-insert(字符串1,字符串2,数字)`//将字符串2以数字的大小插入到字符串1中



### 颜色

 颜色函数

> `rgb(红,绿,蓝,透明度)`
>
> `hsl(色相,饱和度,明度)`
>
> `hsla(色相,饱和度,明度,透明度)`
>
> `lighten(颜色,明度)`//明度在0-100%
>
> `darken(颜色,明度)`//明度在0-100%
>
> `saturate(颜色,饱和度)`//饱和度为0-100%
>
> `desaturate(颜色,饱和度)`//饱和度为0-100%
>
> `opacify(颜色,透明度)`//透明度为0-100%
>
> `transparentize(颜色,透明度)`//透明度为0-100%





### 列表

列表类似于数组

padding: 50px 20px 10px 0;就是一个列表

> `length()`//测定列表长度
>
> `nth()`//求列表第几位的数
>
> `index(列表, 参数)`//求参数在列表的位置，从0开始
>
> `append(列表，参数)`//将参数加到列表之后
>
> `join(列表a,列表b)`//将两个列表拼凑





### Map

 `$map(key1:value1，key2:value2，key3:value3)`

> `map-get(map对象,键)`//得到对应的value
>
> `map-keys(map对象)`//得到map中所有key
>
> `map-values(map对象)`//得到map中所有value
>
> `map-has-key(map对象,参数)`//判断map中是否有该参数的key
>
> `map-merge(map对象,参数对象)`//将参数对象添加到map对象中
>
> `map-remove(map对象,参数对象)`//将参数对象从map对象中去除





## 11、Interpolation

> #{}

将一个值插入到另一个值，可以在选择器或属性上使用变量或表达式。

如 变量&POST:"0.0.0.1"。

若想要直接使用引号中的0.0.0.1，可以#{$POST}

POST为：#{$POST}   => POST为：0.0.0.1





## 12、控制指令

### @if

> ```
> @if 条件{
> 	...
> }
> ```





### @for

> ```
> @for $var from <开始值> to <结束值>{
> 	...
> }//循环不包含结束值
> 
> @for $var from <开始值> through <结束值>{
> 	...
> }//循环包含结束值
> ```





### @each

> ```
> @each $var in $list{
> 	...
> }//循环执行列表
> ```





### @while

> ```
> @while 条件{
> 	...
> }
> ```





## 13、自定义函数

> ```
> @function 名称(参数1,参数2){
> 	...
> }
> ```







## 14、警告与错误

> `@warn "内容"`

输出会在命令行出现

> WARNING:"内容"