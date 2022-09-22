# Less

## 1、Less安装使用

### 法一：yarn安装

使用yarn直接安装less，在终端输入

> yarn global add less

安装后可以通过检测版本，观测是否成功

> lessc -v



之后可以在VScode的扩展组件中，找到Easy Less安装

![image-20220920204451564](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220920204451564.png)

安装完毕后，可以直接使用.less文件，less文件会自动生成并转译成css文件。





### 法二：引入LESS文件使用

将LESS文件直接下载到本地。

把CSS内容复制出来，到自己的项目目录里面创建一个`less.js`文件放进去。然后再引入。

> ```
> <link rel="stylesheet/less" type="text/css" href="./css/my.less" />
> <script src="./js/less.js"></script>
> ```





## 2、less注释

以//开头注释不会被编译到css中；

以/**/包含的注释会被编译到css中;





## 3、变量

在LESS中可以定义变量，定义变量需要使用@开头

1、定义普通属性

> 如：@first-color = #0000e0;

变量可以在其他地方被调用。

2、定义选择器或属性变量，

> 如：@m:margin ; @seletor:# warp;
>
> 但调用时需要用@{}括住变量
>
> @{m}

3、定义URL

> @{url}

4、变量延迟加载

> ```
> @var:0;
> .class {
> 	@VAR:1;
> 	.brass{
> 		@var:2;
> 		three:@var;//3 less会在块级作用域运行完后，再将变量进行赋值。
> 		@var:2;
> 	}
> 	one:@var;
> }
> ```



## 4、嵌套规则

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

加&表示让&后的属性和所在的块区域平级

即：&为平级





## 5、混合

混合就是将一些列属性从一个规则集引入到另一个规则集的方式

### 1、普通混合

> ```
> .mix{
> 	...
> }
> 
> body{
> 	inner1{
> 		mix;
> 	}
> 	inner2{
> 		mix;
> 	}
> }
> 
> ```

普通混合会输出到CSS中

### 2、不带输出的混合

> ```
> .mix(){
> 	...
> }
> 
> body{
> 	inner1{
> 		mix;
> 	}
> 	inner2{
> 		mix;
> 	}
> }
> ```

CSS不会出现.mix



### 3、带参数的混合

需要传参

> ```
> .mix(@参数1,@参数2){
> 	...
> 	height:@参数1;
> 	weight:@参数2
> }
> 
> body{
> 	inner1{
> 		mix(100px,200px);
> 	}
> 	inner2{
> 		mix(200px,300px);
> 	}
> }
> 
> ```



### 4、带参数并有默认值的混合

> ```
> .mix(@参数1:20px,@参数2:30px){
> 	...
> 	height:@参数1;
> 	weight:@参数2
> }
> 
> body{
> 	inner1{
> 		mix(100px,200px);
> 	}
> 	inner2{
> 		mix(200px,300px);
> 	}
> }
> 
> ```

调用时候可以不用传参。



### 5、命名参数

在调用带有默认值的混合时，可以指定某一个参数进行修改。

> ```
> .mix(@参数1:20px,@参数2:30px){
> 	...
> 	height:@参数1;
> 	weight:@参数2
> }
> 
> body{
> 	inner1{
> 		mix(@参数2：500px);
> 	}
> 	inner2{
> 		mix(@参数1：600px);
> 	}
> }
> 
> ```





### 6、匹配模式

根据调用的形式，自动匹配混合。

> ```
> .tri(@_){
> 	...
> }//只要传入任意一个参数，该属性就会被调用
> 
> .tri(L,@W,@c){
> 	...
> }
> 
> .tri(R,@W,@c){
> 	...
> }
> 
> .tri(B,@W,@c){
> 	...
> }
> 
> .tri(T,@W,@c){
> 	...
> }
> 
> 
> #warp .sanjiao{
> 	.tri(R,20px,red);
> }
> ```



### 7、arguments

混合会将输入的实参，以伪数组arguments的形式输出。

> ```
> .mix(@参数1,@参数){
> 	border:@arguments;//编译后会变成border:10px,20px;
> }
> 
> body{
> 	inner1{
> 		mix(10px,20px);
> 	}
> }
> ```





## 6、mixin和extend的区别

extend不能传入参数

> ```
> .warp{
> 	...
> }
> .inner{
> 	&:extend(.warp);
> }
> ```



>  extend(.xx all);可以将.xx后所有属性传入





## 7、LESS避免编译

> 避免编译方法：~"内容"

这样内容就不会从less编译到css中，而是直接原封不动的放入CSS里。