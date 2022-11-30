# Node

## fs文件系统模块

fs模块由node提供，用于操作文件模块。提供了一系列的方法和属性，用于满足用户对文件的操作需求。如：

* fs.readfile()，用于读取指定文件的内容

* fs.writefile()，用于向指定文件写入内容

  导入方法：

`const fs = require('fs')`

读取语法格式：

`fs.readFile(path[,options], callback)`

 path:字符串，表文件路径

options:可选，以什么编码格式读取文件（默认utf8）

callback:回调，文件读取完毕后，通过回调拿到读取结果

> `fs.readFile('', '', function(err, dataStr))`

成功：err为null

失败：err为错误对象，dateStr为undefined



写入语法格式：

`fs.writefile(file, data[, options], callback)`

file:字符串，存放路径

data:写入内容

options:默认utf8

callback:回调，文件写入完毕后的回调函数

> `fs.readFile('', '', function(err){}`

err函数一定会被调用输出

写入成功，err为null

PS：运行时，会以执行node命令所处目录，动态拼接出被操作文件的完整路径

出现路径拼接错误的问题，是因为提供了./ 或 ../开头的相对路径

解决方法：直接提供完整的文件存放路径'C:\\Users\\\...' 或使用 __dirname + '路径'



## path路径模块

![image-20221101203518997](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101203518997.png)

![image-20221101203554084](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101203554084.png)

![image-20221101203647065](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101203647065.png)

![image-20221101204125441](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101204125441.png)

![image-20221101204134706](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101204134706.png)

![image-20221101204310406](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101204310406.png)

![image-20221101204413342](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101204413342.png)





## http模块

![image-20221101210620695](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101210620695.png)

![image-20221101211030512](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101211030512.png)

![image-20221101211217989](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221101211217989.png)



## 创建web服务器

![image-20221102191226307](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102191226307.png)![image-20221102191247210](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102191247210.png)

![image-20221102191310079](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102191310079.png)

![image-20221102191329847](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102191329847.png)

![image-20221102192423715](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102192423715.png)

![image-20221102192438573](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102192438573.png)

![image-20221102192815022](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102192815022.png)

![image-20221102193241938](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102193241938.png)

![image-20221102193317406](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102193317406.png)



## 模块化

![image-20221102202346444](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102202346444.png)

![image-20221102203113301](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102203113301.png)

![image-20221102203753267](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102203753267.png)

![image-20221102204017908](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102204017908.png)





## 包

![image-20221102205040893](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205040893.png)

![image-20221102205121717](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205121717.png)

![image-20221102205159129](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205159129.png)

![image-20221102205303178](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205303178.png)

![image-20221102205418308](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205418308.png)



## 包的分类

![image-20221102205613058](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205613058.png)

![image-20221102205709851](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205709851.png)

![image-20221102205941737](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102205941737.png)

![image-20221102210029917](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102210029917.png)



## 自定义包

![image-20221102210457307](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102210457307.png)

![image-20221102210507546](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102210507546.png)

![image-20221102210834700](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102210834700.png)

![image-20221102210919422](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102210919422.png)

![image-20221102211013762](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221102211013762.png)



## 模块加载机制

![image-20221103112214895](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103112214895.png)

![image-20221103112225692](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103112225692.png)

![image-20221103112528632](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103112528632.png)

![image-20221103114018886](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103114018886.png)

![image-20221103114817303](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103114817303.png)



## Express

![image-20221103115141889](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115141889.png)



### 基本使用

![image-20221103115200481](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115200481.png)

![image-20221103115209315](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115209315.png)

![image-20221103115313282](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115313282.png)

![image-20221103115339057](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115339057.png)

![image-20221103115519871](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115519871.png)

![image-20221103115611076](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103115611076.png)

![image-20221103120119345](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103120119345.png)

### 静态资源托管

![image-20221103120415103](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103120415103.png)

![image-20221103120559630](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103120559630.png)

![image-20221103120626691](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103120626691.png)

![image-20221103120827003](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103120827003.png)



### nodemon

![image-20221103121045878](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103121045878.png)

![image-20221103121102195](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103121102195.png)

![image-20221103121141761](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103121141761.png)

### 路由

![image-20221103191820356](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103191820356.png)

![image-20221103191912552](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103191912552.png)

![image-20221103192134016](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103192134016.png)

![image-20221103192442030](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103192442030.png)

![image-20221103192745924](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103192745924.png)

![image-20221103192755358](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103192755358.png)

![image-20221103193135945](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103193135945.png)

![image-20221103193509315](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103193509315.png)



### 中间件

![image-20221103194828934](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103194828934.png)

![image-20221103194947685](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103194947685.png)

![image-20221103195033212](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103195033212.png)

![image-20221103195543316](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103195543316.png)

![image-20221103195701988](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103195701988.png)

![image-20221103200346257](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103200346257.png)

![image-20221103200446679](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103200446679.png)

![image-20221103201055909](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103201055909.png)

![image-20221103201119986](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103201119986.png)

![image-20221103201223137](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103201223137.png)

![image-20221103201854213](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103201854213.png)

![image-20221103202519536](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103202519536.png)

![image-20221103202539094](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103202539094.png)

![image-20221103202556437](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103202556437.png)

![image-20221103202928157](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103202928157.png)

![image-20221103203240598](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103203240598.png)

![image-20221103203445838](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103203445838.png)

![image-20221103203750062](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103203750062.png)

![image-20221103204031916](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103204031916.png)



### 编写接口

![image-20221103204524794](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103204524794.png)

![image-20221103204549368](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103204549368.png)

![image-20221103204844993](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103204844993.png)

![image-20221103204920127](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103204920127.png)

#### 跨域问题

![image-20221103205116247](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205116247.png)

![image-20221103205133460](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205133460.png)

![image-20221103205357767](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205357767.png)

![image-20221103205415943](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205415943.png)

![image-20221103205510768](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205510768.png)

![image-20221103205534161](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205534161.png)

![image-20221103205548966](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205548966.png)

![image-20221103205614264](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205614264.png)

![image-20221103205637134](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205637134.png)

![image-20221103205654559](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205654559.png)

![image-20221103205715408](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205715408.png)

![image-20221103205757937](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205757937.png)



#### JSONP接口

![image-20221103205852760](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205852760.png)

![image-20221103205906246](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103205906246.png)

![image-20221103210002249](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103210002249.png)

![image-20221103210009112](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103210009112.png)

![image-20221103210200507](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221103210200507.png)





## MySQL Workbench

![image-20221105143444259](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105143444259.png)

![image-20221105143556894](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105143556894.png)

![image-20221105144055965](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105144055965.png)

![image-20221105144719852](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105144719852.png)

![image-20221105145035130](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105145035130.png)

 

## MySQL语法

### 基本语法

![image-20221105150226909](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105150226909.png)

![image-20221105150319300](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105150319300.png)

![image-20221105150711504](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105150711504.png)

### where子句

![image-20221105151149370](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105151149370.png)

![image-20221105151327407](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105151327407.png)

![image-20221105151417392](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105151417392.png)

![image-20221105151635729](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105151635729.png)

![image-20221105152003644](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152003644.png)





### COUNT(*)函数

![image-20221105152312112](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152312112.png)

![image-20221105152327325](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152327325.png)



## 项目中操作MySQL

![image-20221105152458248](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152458248.png)

![image-20221105152732492](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152732492.png)

![image-20221105152754604](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152754604.png)

![image-20221105152830234](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105152830234.png)

![image-20221105153039597](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105153039597.png)

![image-20221105153421508](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105153421508.png)

  

![image-20221105153903041](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105153903041.png)

![image-20221105154057290](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105154057290.png)

![image-20221105154143820](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105154143820.png)

![image-20221105154308645](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105154308645.png)

![image-20221105154407135](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105154407135.png)



## Web开发模式

![image-20221105163657583](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105163657583.png)

![image-20221105163723558](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105163723558.png)

![image-20221105164012909](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105164012909.png)

![image-20221105164057543](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105164057543.png)

![image-20221105164311242](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105164311242.png)

![image-20221105164424976](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105164424976.png)



### session认证机制

![image-20221105170033480](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105170033480.png)

![image-20221105170256087](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105170256087.png)

![image-20221105170452104](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105170452104.png)

![image-20221105170800166](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105170800166.png)

![image-20221105171035829](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105171035829.png)

![image-20221105171149584](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105171149584.png)

![image-20221105171333139](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105171333139.png)

![image-20221105171740113](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105171740113.png)

![image-20221105172128135](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105172128135.png)

![image-20221105172345243](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105172345243.png)

![image-20221105172829129](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105172829129.png)

![image-20221105172917803](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105172917803.png)



### JWT认证机制

![image-20221105173424632](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173424632.png)

![image-20221105173441480](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173441480.png)

![image-20221105173556502](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173556502.png)

![image-20221105173644257](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173644257.png)

![image-20221105173719944](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173719944.png)

![image-20221105173759607](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105173759607.png)



#### 使用方法

![image-20221105174224355](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105174224355.png)

![image-20221105174248533](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105174248533.png)

![image-20221105174345720](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105174345720.png)

![image-20221105174558493](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105174558493.png)     

![image-20221105174835610](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105174835610.png)

![image-20221105175134521](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105175134521.png)

![image-20221105175221409](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105175221409.png)

![image-20221105175619525](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221105175619525.png)