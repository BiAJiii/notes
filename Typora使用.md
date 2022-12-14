# 一、语法

## 1.1 标题

使用 `#` 可以表示标题，一级标题对应一个 `#` ，二级标题对应两个 `#` 号，最多至六级标题。注意：`#` 后要紧接着一个空格才能表示标题，否则就是普通字符。



## 1.2 字体

* 用*号或_括住表示斜体文字，   * test *  => *test*	，快捷键Ctrl+I。
* 两个**或__括住表示加粗文字 ,      快捷键Ctrl+B。
* 三个***或___括住表示加粗斜体文字 



## 1.3 线

* 三个*或-或+表示分割线， 如下

  ***

* 两个~~括住表示删除文本，如下

  ~~删除线~~

* 用<u>的html标签表示增加下划线文本。

  <u>下划线</u>

## 1.4 列表

### 无序标题

使用* + -表示无序列表，每一种符号表示一类

![image-20220916112815181](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916112815181.png)

结果：

* 第一项
* 第二项
+ 第一项
+ 第二项
- 第一项
- 第二项

### 有序列表

语法：数字+.+空格，且顺序不要求数字连续，只要大小排列即可

![image-20220916113008828](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916113008828.png)

结果：

1. 第一项

2. 第二项

3. 第三项

   

### 嵌套列表

首先使用`*`、`+`或`-`进入列表，然后回车换行，会发现系统自动生成列表第二项，此时按下**Tab**键，列表第二项变为第一项的子列表。**按回车退出当前列表**。可以在无序列表中嵌套有序列表。



- 一
  - 1.1
    - 1.1.1
      - 1.1.1.1
      - 1.1.1.2
    - 1.1.2
      - 1.1.2.1



## 1.5 区块

当想要引用别人的文章内容时，可以将其放在区块内。

可以使用`>`加空格来表示区块。两次空格在下端返回上一区块。

> 一级区块
>
> > 二级区块
> >
> > > ​	三级区块
> >
> > 二级
>
> 三级





## 1.6 代码

单行代码，使用段内代码块表示，用``括住代码

> `printf("hello,world！");`

代码段，则使用三个`加Enter+内容表示。

```
# include <stdio.h>
void main(){
	printf("Hello world!\n");
}
```



## 1.7 连接

连接使用有两种语法

```
1 、[链接文字](链接地址)
2 、<链接地址>
```

如：

```
[谷歌](https://www.google.com/)
<https://www.google.com>
```

> [谷歌](https://www.google.com/)
> <https://www.google.com>

链接除了可以打开相应的网页外，还可以**打开本地文件**，使用方式类似，不过链接地址需要使用本地文件的地址，相对地址、绝对地址均可。



## 1.8 图片

插入图片方法如下：

```
![alt 属性文本](图片地址)
或
![alt 属性文本](图片地址 "可选标题")
```

如：

```
![本地jpg图片](./img/PictureTest.jpg)
![网络图片](http://static.runoob.com/images/runoob-logo.png "菜鸟教程")
```



可以直接往Typora中粘贴图片，但图片需要有地址。



## 1.9 表格

> 使用 `|` 来分隔不同的单元格，使用 `-` 来分隔表头和其他行

```
|表头|表头|表头|
|---|---|----|
|单元格|单元格|单元格|
|单元格|单元格|单元格|
```

| 表头   | 表头   | 表头   |
| ------ | ------ | ------ |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |



对齐方式

- `:-`表示左对齐
- `-:`表示右对齐
- `:-:`表示中间对齐



在表头和单元格中间添加对齐方式

```
|左对齐|右对齐|中间对齐|
|:---|---:|:----:|
|单元格|单元格|单元格|
|单元格|单元格|单元格|
```



# 二、 HTML

## 2.1 改变字体

使用<font>标签改变字体颜色以及大小



如：``<font size=3 color="red">字体颜色为红色，大小为3</font>``

> <font size=3 color="red">字体颜色为红色，大小为3</font>



## 2.2 改变对齐方式

使用标签<p>配合属性align使用，

如：``<p align="center">中间对齐</p>``

> <p align="center">中间对齐</p>



## 2.3 插入图像

通过<img src=url /> 标签插入或修改图像

如：``<img src="img/1.jpg" />``

配合width和height设置大小

如：``<img src="img/1.jpg" width=100 height=100/>``





# 三、 其余用法

## 3.1 插入目录

>  当我们为使用标题将文分章节后，可以在输入`[toc]`命令的地方自动根据标题生成目录。



## 3.2 导出

> 选择文件 --> 导出，可以选择导出的文件格式，有pdf,html,word等格式。



## 3.3 文本高亮

> 可使用==括起需要高亮的文本
>
> 需要在偏好设置 --> Markdown扩展语法中设置

```
==高亮文本==
==文本高亮==
```

==要高亮的文本==
==背景会用黄色填充==



## 3.4 上下标

> 在Typora中，可以用一对`~`将下标括起来，如：`H~2~O`表示H2O
>
> 同样，我们也可以用一对`^`将上标括起来，如：`X^2^`表示X2
>
> 同样需要在偏好设置 --> Markdown扩展语法中设置。







