# Vue基础

## 安装使用

Vue有Vue2和Vue3两种版本，使用需要安装不同的包。

> `yarn add vue-latest` //安装Vue3包
>
> `yarn add vue2`//安装Vue2包

通过导入CDN进入html使用Vue

> ```
>     <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
>     <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.6.13/vue.js"></script>
> ```

之后即可在html中使用。



## 简单的使用

>  ```
>  <head>
>      <meta charset="UTF-8">
>      <meta http-equiv="X-UA-Compatible" content="IE=edge">
>      <meta name="viewport" content="width=device-width, initial-scale=1.0">
>      <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
>      <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.6.13/vue.js"></script>
>      <title>Document</title>
>  </head>
>  <body>
>      <div id="root">
>          <h1>Hello, {{name}}!</h1>
>      </div>
>  
>      <script type="text/javascript">//  vue2写法
>          new Vue({
>              el:'#root',
>              data:{
>                  name:'Sam',
>              }
>          });    
>  
>          Vue.createApp({//   Vue3写法
>              data() {
>                  return {
>                      data: 'sam'
>                  }
>              }
>          }).mount('#root')
>      </script>
>  </body>
>  </html>
>  ```

Vue的语句是一一对应的，一个萝卜一个坑。第一个Vue选取了一个Div后，基本第二个Vue选取，也不会有任何意义



## 快速生成.vue模板

在文件->首选项->配置用户代码片段

在vue.json文件中将以下代码复制进入即可

> ```
> {
> 	"vue3 template": {
> 		"prefix": "vue3",
> 		"body": [
> 			"<template>",
> 			"$2",
> 			"</template>",
> 			"",
> 			"<script>",
> 			"$1",
> 			"</script>",
> 			"",
> 			"<style>",
> 			"$3",
> 			"</style>"
> 		],
> 		"description": "vue3基础模板"
> 	}
> }
> ```



## 模板语法



### 插值语法

功能:用于解析标签休内容。

> 插值语法{{}}中可以包含表达式，而不能包含JS代码(语句)
>
> 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方。
>
> 如：a；a+b；x===y?'a':'b'
>
> JS代码
>
> 如:for循环  if语句





### 指令语法

功能:用于解析标签(包括:标签属性、标签体内容、绑定事件..)。

> v-bind:    可以简写成 :  

绑定标签，将标签内的值当作JS表达式在Vue中识别。





## 数据绑定

使用指令语法:bind进行绑定的是单项绑定，修改Vue中的值，html的值会变化，但反过来却不会。使用`v-model`可以实现双向绑定。

注：`v-model`只能应用在表单类元素(输入元素)上。

语法：v-mode:value="xxx" 或简写为 v-model="xxx"





## 数据代理

当对象中的属性a和对象外的属性b需要进行绑定时，可以让a=b，但这样每次修改b，则需要对a进行重新赋值。这样十分不方便，可以直接数据代理来实现改变b就改变a；

> Object.defineProperty(对象,对象属性,{对象属性的内容，如方法，变量})

在{}中可以设定getter,setter等方法，方便修改或获取值。



> ```
> <script>
>         let number = 18;
>         let person = {
>             name:'Sam',
>             sex:'男'
>         }
>         Object.defineProperty(person ,'age', {
>             // value: 18,
>             // enumerable:true,//决定是否可被枚举
>             // writable:true,//是否可以被修改
>             // configurable:true,//是否可以被删除
> 
> 
>             get:function(){
>                 return number;
>             },
> 
>             set:function(value){
>                 number = value;
>             }
> 
>         })
>     </script> 
> ```

![image-20220924135843496](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220924135843496.png)





## 事件处理

### 事件

使用v-on:xxx或@xxx绑定事件，xxx为时间名；

事件的回调需要配置在methods对象中；

methords中配置的函数，都是被Vue所管理的函数，this的指向时vm或组件实例对象；

@click="demo"和@click="demo($event)"效果一样，但后者可以传参；

> ```
> <body>
>     <div id = "root">
>         <h2>欢迎来{{name}}学习</h2>
>         <button v-on:click="showInfo1">点我</button> 
>         <button @click="showInfo2($event,555)">点我</button> 
>     </div>
>         <!-- v-on:click简写  =>  @click -->
>         <script>
>             const vm1 = new Vue({
>                 el:"#root",
>                 data:{
>                     name:'北京',
>                 },
>                 methods:{
>                     showInfo1(){//此处this为vue
>                         alert('同学你好');
>                     },
>                     showInfo2(event , number){//此处this为vue
>                         alert('同学你好~~~');
>                     }
>                 }
>             })
>         </script>
>     </div>
> </body>
> ```

### 事件修饰符

> 1、prevent:阻止默认事件
>
> 2、stop：组织事件冒泡
>
> 3、once：事件只触发一次
>
> 4、capture：使用事件的捕获模式
>
> 5、self：只有event.target时当前操作的元素才触发事件
>
> 6、passive：事件的默认行为立即执行，无需等待事件回调执行完毕；



## 键盘事件

> 1.Vue中常用的按键别名
>
> ​	回车=>enter ; 删除=>delite；退出=>esc；空格=>space；换行=>tab（必须配合keydown使用）；上=>up；下=>down；左=>left；右=>right；
>
> 2、Vue未提供的别名按键可以用按键原始的key（键名）去绑定，但要转为kebab-case(短横线命名)如CapsLock=>caps-lock
>
> 3、系统修饰键（用法特殊）：ctrl、alt、shift、meta
>
> ​	（1）配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其它键，事件才触发
>
> ​	（2）配合keydown使用：正常触发事件
>
> 4、可以使用keyCode去指定具体的按键
>
> 5、Vue.config.keyCodes.自定义按键 = 键码，可以去定制按键别名



## 计算属性

定义：要使用的属性不存在，要通过已有的属性进行计算得到。

原理：底层借助了Object.defineProperty方法提供的getter和setter。

computed中get调用时机：1、初次读取  2、依赖数据发生改变；

PS：1、计算属性最终会出现在VM上，直接读取即可；

​    	2、如果计算属性要被修改，那必须写set函数去相应修改，且set中要引起计算时依赖的数据发生变化。

> ```
> <body>
>     <div id = "root">
>         姓：<input type="text" v-model="firstName"><br/></br>
>         名：<input type="text" v-model="lastName"><br/></br>
>         全名：<span>{{fullName}}</span>
>     </div>
> 
>     <script>
>         const vm = new Vue({
>             el:'#root',
>             data:{
>                 firstName:'张',
>                 lastName:'三',
>             },
>             computed:{
>                 fullName:{
>                     get(){
>                         return this.firstName + '-' + this.lastName;
>                     },
>                     set(value){
>                         const arr = value.spilt('-');
>                         this.firstName = arr[0];
>                         this.lastName = arr[1];
>                     }
>                 }
>                 //get调用时机：1、初次读取  2、依赖数据发生改变
>                 
>             }
>         })
>     </script>
> ```

简写方法（只读情况可用）：

> ```
> fullName(){
> 	return this.firstName + '-' + this.lastName;
> }
> ```





## 监视属性

监视属性watch：

1、当被监视的属性变化，回调函数自动调用，进行相关操作

2、监视的属性必须存在，才可以进行监视

3、监视的两种写法 

​	（1）new Vue中传入watch配置

​	（2）通过vm.$watch监视

> ```
> <body>
>     <div id="root">
>         <h2>今天天气{{info}}</h2>
>         <button @click="change">切换天气</button>
>     </div>
>     <script>
>         const vm = new Vue({
>             el:'#root',
>              
>             data:{
>                 isHot:true,
>             },
>             watch:{
>               isHot:{
>                 immediate:true,//初始化时让handler调用一下
>                 handler(newVaule,oldVaule){
>                     return this.isHot?'炎热':'凉爽';
>                 }
>               }
>             },
>             methods: {
>                 change(){
>                     this.isHot = !this.isHot;
>                 }
>             },
>             computed:{
>                 info(){
>                     return this.isHot?'炎热':'凉爽';
>                 }
>             }
>         })
> 
>         vm.$watch('isHot',{});
>     </script>
> ```

**深度监视**：监视多级结构中所有属性的变化，watch默认不能监视多层级改变。

> ```
> data:{
> 	isHot:true;
> 	numbers:{//只监视numbers中存放a b的地址，地址不变化，默认numbers没变化
> 		a=1,//内部（多层）,监视a b
> 		b=2
> 	}
> }
> ```
>
> 

1、Vue中的watch默认不检测对象内部值的改变（一层）

2、配置deep:true可以检测对象内部值改变（多层）

注：

1、Vue自身可以检测对象内部值的改变，但Vue提供的watch默认不可以！

2、使用watch时根据数据的具体结构，决定是否采用深度监视



**简写形式**(不需要其他配置项)

> ```
> watch:{
> 	isHot(newValue,oldValue){
> 		...
> 	}
> }
> 
> or
> 
> vm.$watch('isHot',function(newValue,oldValue){
> 	...
> })
> ```



## 绑定class/style样式

1、class样式

​	写法：class="xxx" , xxx可以是字符串、对象、数组

​			字符串写法用于：类名不确定，要动态获取。

​			对象写法用于：要绑定多个样式，个数不确定，名字不确定。

​			数组写法用于：要绑定多个样式，个数确定，名字确定，但不确定用不用。

2、style样式

​	写法：

​		:style="{fontSzie : xxx}",xxx为动态值

​		:stlye="[a,b]"其中a、b为样式对象，样式对象即key写法必须是存在的CSS属性，如fontSize、color、backgroundColor等。如{fontSize:'40px'}

> ```
> <body>
>     <div id="root">
>         <!-- 绑定class样式 --字符串写法，适用于：样式的类名不确定，需要动态指定-->
>         <div class="basic" :class="mood" @click="changeMood">{{name}}</div><br/></br>
> 
>         <!-- 绑定class样式 --数组写法，适用于：样式的类名不确定、个数也不确定-->
>         <div class="basic" :class="classArr">{{name}}</div><br/></br>
> 
>         <!-- 绑定class样式 --对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用-->
>         <div class="basic" :class="classObj" >{{name}}</div><br/></br>
> 
>         <!-- 绑定stlye样式 --对象写法--所存内容为对象，可通过指定key和value的值进行改变-->
>         <div class="basic" :class="{fontSize : fsize +'px'}" >{{name}}</div><br/></br>
>     </div>
> 
>     <script>
>         const vm = new Vue({
>             el:'root',
>             data:{
>                 name:'Sam',
>                 mood:'normal',
>                 classArr:['sam1','sam2','sam3'],
>                 classObj:{
>                     sam1:false,
>                     sam2:false,
>                 }
>             },
>             methods: {
>                 changeMood(){
>                     const arr = ['happy','sad','normal']
>                     this.mood = arr[Math.floor(Math.random()*3)]
>                 }
>                
>             },
>         })
>     </script>
> </body>
> ```





## 条件渲染

**1、v-show**

​	写法：v-show = ""

​	适用于：切换频率较高的场景

​	特点：不展示的DOM元素未被移除，仅是display：none效果



**2、v-if**

​	写法：

​		（1）v-if=""

​		（2）v-else-if=""

​		（3）v-else=""

​	适用于：切换频率低

​	特点：不展示DOOM元素直接移除

​	PS：可以和v-else-if、v-else一起使用



注：当需要给一大堆结构做条件渲染，而又不能破坏结构时，可以使用template模板作为包裹结构。在解析代码时，template不会出现在最终结构上。



> ```
> <body>
>     <div id = "root">
>         <h2 v-show = "a">欢迎光临~{{name}}</h2>
>         <h2 v-if = "b===1">慢走不送~</h2>     
>         <h2 v-else-if = "b===2">吃个饭再走~</h2>     
>         <h2 v-else>SEE SEE</h2>
>         <button @click = "change">点我</button>
> 
>         <template v-if = "true">
>             <h2>1</h2>
>             <h2>2</h2>
>             <h2>3</h2>
>         </template>
> 
> 
>     </div>
> 
>     <script>
>         const vm = new Vue({
>             el:'#root',
>             data:{
>                 name:'Sam',
>                 a: true,
>                 b: 0,
>             },
>             methods: {
>                 change(){
>                     this.a = !this.a;
>                     this.b++;
>                     if(this.b > 2){
>                         this.b = 0;
>                     }
>                 }
>             },
>         })
>     </script>
>     
> ```



## 列表渲染

**v-for指令**

​	1、用于展示列表数据

​	2、语法：v-for="(item,index) in xxx"  :key="yyy"

​	3、可遍历：数组、对象、字符串、指定次数



> ```
> <body>
>     <div id = "root">
>         <!-- 遍历数组 -->
>         <ul>
>             <li v-for = '(p,index) in Persons' :key="p.id">
>                 {{p.name}}--{{p.age}}
>             </li>
>         </ul>
>         <!-- 遍历对象 -->
>         <ul>
>             <li v-for = '(value, key) in Car' :key="key">
>                 {{key}}--{{value}}
>             </li>
>         </ul>
>     </div>
> 
>     <script>
>         const vm = new Vue({
>             el:'#root',
>             data:{
>                 Persons:[
>                     {id:'001',name:'张三',age:18},
>                     {id:'002',name:'李四',age:19},
>                     {id:'003',name:'王五',age:20},
>                 ],
>                 Car:{
>                     name:'BMW 5',
>                     price:'300k',
>                     color:'白色',
>                 }
>             }
>         })
>     </script>
> ```

watch实现

> 

## 列表筛选

可使用watch或computed实现

> 基本body代码
>
> ```
>     <div id = "root">
>         <input type="text" placeholder="请输入名字" v-model="keyWord">
>         <!-- 遍历数组 -->
>         <ul>
>             <li v-for = '(p,index) in filPersons' :key="p.id">
>                 {{p.name}}--{{p.age}}--{{p.sex}}
>             </li>
>         </ul>
>     </div>
> ```

watch实现

> ```
>         const vm = new Vue({
>             el:'#root',
>             data:{
>                 keyWord:'',
>                 Persons:[
>                     {id:'001',name:'马冬梅',age:18,sex:'女'},
>                     {id:'002',name:'周冬雨',age:19,sex:'女'},
>                     {id:'003',name:'周杰伦',age:20,sex:'男'},
>                     {id:'004',name:'温兆伦',age:21,sex:'男'},
>                 ],
>                 filPersons:[]
>             },
>             watch:{
>                 keyWord:{
>                     immediate:true,//进入立马执行，使得一开始所有列表可见
>                     handler(val){
>                         this.filPersons = this.Persons.filter((p)=>{
>                             return p.name.indexOf(val) !== -1;
>                         })
>                     }
>                 }
>                 
>             }
>         })
>     
> ```

computed实现

> ```
>         const Vm = new Vue({
>             el:'#root',
>             data:{
>                 keyWord:'',
>                 Persons:[
>                     {id:'001',name:'马冬梅',age:18,sex:'女'},
>                     {id:'002',name:'周冬雨',age:19,sex:'女'},
>                     {id:'003',name:'周杰伦',age:20,sex:'男'},
>                     {id:'004',name:'温兆伦',age:21,sex:'男'},
>                 ],
>                 filPersons:[]
>             },
>             computed:{
>                 filPerson(){
>                     return this.Persons.filter((p)=>{
>                             return p.name.indexOf(this.keyWord) !== -1;
>                         })
>                 }
>             }
>         })
> ```

## key的原理

![image-20220927192546029](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220927192546029.png)

![image-20220927192600401](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220927192600401.png)

![image-20220927192651991](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220927192651991.png)





## Vue监视数据的原理

* 1、 vue会监视data中所有层次的数据。

* 2.如何监测对象中的数据?

  通过setter实现监视,且要在new Vuel时就传入要监测的数据。

  (1),对象中后追加的属性, Vue默认不做响应式处理

  (2).如需给后添加的属性做响应式,请使用如下API:

  Vue.set(target, propertyName/index, value)或

  vm.$set(target, propertyName/index, value)

* 3.如何监测数组中的数据?

  通过包裹数组更新元素的方法实现,本质就是做了两件事:

  (1).调用原生对应的方法对数组进行更新。

  (2),重新解析模板,进而更新页面。

* 4.在Vue修改数组中的某个元素一定要用如下方法:

  1.使用这些API:push()、pop()、 shift()、unshift()、 splice()、sort()、 reverse()

  2.Vue.set()或vm.$set()

* 5、特别注意：Vue.set()和vm.$set()不能给vm或者vm的根数据对象添加属性
* 6、一些数组方法并不会变更原始数组，而是总是返回一个新数组，当使用非变更方法时，可以使用新数组替代旧数组。



## 收集表单数据

![image-20220928203412744](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220928203412744.png)



## 过滤器

![image-20220928205615208](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220928205615208.png)



## V指令

### v-text

作用：向其所在的节点中渲染文本内容。

与插值语法的区别：v-text会替换掉节点中的内容,插值语法{{}}则不会



### v-html

支持结构解析，写入的结构参数也会被解析出来，而v-text只是当字符串处理。

![image-20220928211827088](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220928211827088.png)





### v-clock

> ```
> [v-cloak]{
> 	CSS内容
> }
> ```
>
> 

1、本质是一个特殊属性 ，Vue实例创建完毕并接管容器后，会删掉v-cloak属性

2、使用css配合c-clock可以解决网速慢时 页面显示{{}}的问题 





### v-once

1、v-once所在节点在初次动态渲染后，就视为静态内容

2、以后数据的改变不会引起v-once所在结构的更新。





### v-pre

1、跳过其所在节点的编译过程

2、可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。





## 自定义指令

   一、定义语法

​	（1）局部指令	

> ```
> new Vue({
> 	directives:{指令名:配置对象}
> })
> 或
> new Vue({
> 	directives{指令名:回调函数}
> })//方法定义
> ```



​	（2）全局指令(全局可以调用)

> ```
> Vue.directive(指令名,配置对象)
> 或
> Vue.diretive(指令名,回调函数)
> ```



二、配置对象中常用的3个回调

​	（1）bind:指令与元素成功绑定时调用

​	（2）inserted:指令所在元素被插入页面时调用

​	（3）update:指令所在模板结构被重新解析时调用



三、备注

​	1.指令定义不加v-，但使用时要v-

​	2.指令如果时多个单词，要用kebab-case命名方法，不要用camlCase命名





## 生命周期

![image-20220930113202446](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220930113202446.png)![image-20220930113329392](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220930113329392.png)

![image-20220930113433188](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220930113433188.png)







## 非单文件组件

![image-20220930203516889](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220930203516889.png)

> ```
> <body>
>     <div id = "root">
>         //3、使用组件
>         <hello></hello>
>         <school></school>
>         <hr/>
>         <student></student>
>     </div>
> 
>     <div id = "root2">
>         <hello></hello>
>     </div>
> 
>     <script>
>         //1、定义组件
>         const school = Vue.extend({
>             template:`
>             <div>
>                 <h2>学校:{{schoolName}}</h2>
>                 <h2>地址:{{address}}</h2>
>             </div>
>             `,
>             data(){
>                 return{
>                     schoolName:'暨南大学', 
>                     address:'广州'
>                 }
>             }
>         })
> 
> 
>         const student = Vue.extend({
>             template:`
>             <div>
>                 <h2>学生:{{studentName}}</h2>
>                 <h2>性别:{{gender}}</h2>
>             </div>
>             `,
>             data(){
>                 return {
>                     studentName:'Sam',
>                     gender:'男'
>                 }
>             }
>         })
> 
>         const Hello = Vue.extend({
>             template:`
>                 <button @click="hi">点我说你好！</button>
>             `,
>             methods: {
>                 hi(){
>                     console.log('你好！');
>                 }
>             },
>         })
>         // 全局注册
>         Vue.component('hello',Hello);
> 
>         const vm = new Vue({
>             el:'#root',
>             //注册组件（局部注册）
>             components:{
>                 school,
>                 student
>             }
>             }
>         )
> 
>         const vm2 = new Vue({
>             el:'#root2'
>         })
> 
>     </script>
> </body>
> ```

注意点：

![image-20220930205020814](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220930205020814.png)



## VueComponent构造函数

![image-20221003172440167](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221003172440167.png)

![image-20221003172755596](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221003172755596.png)

![image-20221003172825469](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221003172825469.png)









## 单文件组件

单文件组件是以.vue为后缀的组件。

创建后，存在<template>、<script>、<style>三个配置项，可以将组件结构放入<template>，组件交互相关代码放入<script>，组件样式放入<style>。

再用App.vue汇总所有组件，用main.js文件建立vm实例，最后导入到index.html中。





## Vue脚手架

安装

> `yarn global add @vue/cli`

生成一个vue的helloworld项目

> `vue create '项目名'`

运行安装好的脚手架

>```
>$ cd vue_test
>$ yarn serve
>```

可以在生成的地址中访问

> ```
>   App running at:
>   - Local:   http://localhost:8080/
>   - Network: http://172.18.56.215:8080/
> ```



可以将单文件组件放入脚手架中使用。

将.vue组件放入components中，将app替代src中的原文件app.vue即可



> PS：组件需要命名为驼峰形式，否则会报错。



### render函数

![image-20221007191508147](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221007191508147.png) 





### 脚手架文件结构

![image-20221007193904228](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221007193904228.png)

### vue.config.js配置文件

使用`vue inspect > output.js`可以查看到Vue脚手架的默认配置

使用`vue.config.js`可以对脚手架进行个性化定制，且该文件与`package.json`同级同目录。



### ref属性

1、被用来给元素或子组件注册引用信息（id的替代者）

2、应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象(vc)

3、使用方法

> ```
> //打标识:
> <h1 ref="XXX">...</h1>或<School ref="XXX"></School>
> //获取：
> this.$refs.xxx
> ```



### props配置

![image-20221008144517117](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221008144517117.png)





### mixin配置

可以将多个组件公用的配置，提取成一个混入对象。

1、定义混入

> ```
> {
> 	data(){...},
> 	methods:{...},
> 	...
> }
> ```

2、使用混入

（1）全局混入：`Vue.mixin(xxx)`

（2）局部混入：`mixins:['xxx']`

 

### 插件

包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

定义插件：

> ```
> 对象.install = function(Vue,options){
> //1、添加全局过滤器
> 	Vue.filter(...)
> 	
> 	//2.添加全局指令
> 	Vue.diretive(...)
> 	
> 	//3.配置全局混入（合）
> 	Vue.mixin(...)
> 	
> 	//4.添加实例方法
> 	Vue.prototype.$myMethod = function(){..}
> 	Vue.prototype.$myProperty = XXX
> }
> 
> //使用插件
> 	Vue.use()
> ```





### scoped样式

让样式在局部生效，防止重名冲突

写法：`<style scoped>`





## 数据间通信（todolist）

父组件要将数据传给子组件时候，可以使用props。

但若要让兄弟组件之间，相互传递数据，则需要使用其他方法。

其中一个最基础的是：（1）将数据存放于父组件中（2）将子组件A的数据传递给父组件的数据（3）父组件数据通过props方法传递给A的兄弟组件B进行数据更新

步骤一：

> ```
> data(){
>             return{
>                 todos:[
>                     {id:'001' , title:'吃饭', done:true},
>                     {id:'002' , title:'玩游戏', done:false},
>                     {id:'003' , title:'睡觉', done:true}
>                 ]
>             }
>         }
> 数据存放于App组件中
> ```



步骤二：需要在父组件中定义一个方法如`receive(obj){}`，该方法需要将获取的数据传入到父组件中的data中。然后将该方法传递给子组件，子组件以props接受，这样子组件就可以调用父组件中的receive方法。当子组件将调用receive方法，并将子组件的数据传入到receive中，父组件自然会得到子组件的数据，并且将父组件中的数据更新。

> 父组件
>
> ```
> //将方法传递给子组件A
> <ToAdd :addTodo="addTodo"/>
> 
> 
> //定义方法：
> 	methods:{
>             addTodo(todoOjb){
>                 this.todos.unshift(todoOjb)
>             }
> ```
>
> 子组件A
>
> ```
> //接受父组件传递的方法，并调用，将子组件数据更新至父组件
> 	props:["addTodo"],
>     methods:{
>         add(e){
>             if(!e.target.value.trim()) return alert("输入不可为空")//添加的数组不可为空
>             const todoobj = {id:nanoid(), title:e.target.value , done:false}
>              this.addTodo(todoobj);
>             }
>         }
>     }
> ```





步骤三：当父组件的数据通过接受子组件A的数据而进行更新后，会传入给子组件B。这样就完成了兄弟组件之间的数据传递

> 父组件
>
> ```
> //将数据传递给子组件   
>    <ToList :todos="todos"/>
>    
>    
> 	data(){
>             return{
>                 todos:[
>                     {id:'001' , title:'吃饭', done:true},
>                     {id:'002' , title:'玩游戏', done:false},
>                     {id:'003' , title:'睡觉', done:true}
>                 ]
>             }
>         },
> ```
>
> 子组件B
>
> ```
>         props:["todos"]
> ```







## 组件自定义事件

1、一种组件间通信方式，适用于：子组件=>父组件

2、使用场景，A是父组件，B是子组件，B想给A传数据，那么就在A中给B绑定自定义事件（事件回调在A）

3、绑定自定义事件：

​	1、在父组件中：`<Demo @haha = "test">`或`<Demo v-on:haha="test">`

​	2、在父组件中：

> ```
> <Demo ref="demo"/>
> ....
> mounted(){
> 	this.$refs.xxx.$on('haha' , this.test)
> }
> ```

4、触发自定义事件:`this.$emit('haha',数据)`

5、解绑自定义事件:`this.$off('haha')`  

6、组件上也可以绑定原生DOM事件，需要用native修饰符

7、注意：通过this.$refs.xxx.$on('haha' , this.test)绑定自定义事件时**，回调要么配置在methods中，要么用箭头函数**，否则this指向会出问题/





## 全局事件总线

1、一种组件间通信的方式，适用于任意组件间通信。

2、安装全局事件总线：

> ```
> new Vue({
> 	...
> 	beforeCreate(){
> 		Vue.prototype.$bus = this
> 	},
> 	...
> })
> ```

3、使用事件总线

​	1、组件A接收数据：A组想接收数据，则A组件中给$bus绑定自定义事件，事件的回调在A组件自身。

> ```
> methods(){
> 	demo(data){...}
> }
> ....
> mounted(){
> 	this.$bus.$on('XXX',this.demo)
> }
> ```

​	2、组件B提供数据:`this.$bus.$on('XXX',数据)`

4、最好在beforeDestroy钩子中，用$off去解绑当前组件所用的事件。





## 消息订阅与发布

1、一种组件间通信的方式，适用于任意组件间通信

2、使用步骤：

​	1、安装pubsub:`yarn add pubsub-js`

​	2、引入：`import pubsub from 'pubsub-js'`

​	3、接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身

> ```
> methods(){
> 	demo(data){...}
> }
> ..
> mounted(){
> 	this.pid = pubsub.subcribe('xxx',this.demo)//订阅消息
> }
> ```

4、提供数据`pubsub.publish('xxx',this.demo)`

5、最好在beforeDestroy钩子中，用`PubSub.unsubscribe(pid)`去<span style="color：red">取消订阅<span>



## nextTick

1、语法：`this.$nextTick(回调函数)`

2、作用：在下一次DOM更新结束后执行其指定的回调

3、什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。 





## 动画效果

在将需要动漫的样式放入<transition>标签中

> ```
> <transition name="hello" :appear="true">
>        <h1 v-show="isShow">哈喽~</h1>
> </transition>
> ```

name为该动画的名称，appear为刷新立即使用页面

在css样式中，需要添加三个属性

> ```
> .名-enter-active{
>     animation: qiehuan 1s;
> }
> 
> .名-leave-active{
>     animation: qiehuan 1s reverse;
> }
> 
> @keyframes qiehuan {
>     from {
>         transform: translateX(-100px);
>     }
>     to {
>         transform: translateX(0px);
>     }
> }
> ```

若未定义名，默认为v



写法：

![image-20221017210058250](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221017210058250.png)



第三方动漫引入：

在子组件中引入第三方动漫

`import 'animate.css'`

在div样式中使用即可

> ```
> <transition-group 
>     :appaer="true" 
>     name="animate__animated animate__bounce" 
>     enter-active-class="animate__swing" 
>     leave-active-class="animate__backOutUp">
>     <h1 v-show="isShow" key="1">第三方动漫</h1>
>     <h1 v-show="isShow" key="2">一起来</h1>
> </transition-group>
> ```

具体使用可见https://animate.style/



## 关闭语法校验

在vue.config.js文件中加入`lintOnSave:false`



## vue-cli配置代理

### 法一

在vue.config.js中添加如下配置

> ```
> devServer:{
>     proxy: 'http://localhost:5000'
>   }
> ```

PS：

​	1、优点：配置简单，请求资源时，直接发给前端8080即可。

​	2、缺点：不能配置多个代理，不能灵活控制请求是否走代理

​	3、工作方式：当请求了前端不存在的资源(如：public中的资源)，那么该请求会转发给服务器（优先匹配前端资源）



### 法二

在vue.config.js中添加如下配置

> ```
> devServer: {
>     proxy: {
>       '/api': {//匹配所有以'/api'开头的路径请求
>         target: '<url>',//代理目标的基础路径
>         pathRewrite:{'^/atguigu':''},
>         ws: true,//用于支持websocket
>         changeOrigin: true//是否在请求地址上说谎
>       },
>       '/foo': {
>         target: '<other_url>'
>       }
>     }
>   }
> ```





## 插槽

1、作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于

父组件 ===> 子组件

2、分类：默认插槽、具名插槽、作用于插槽

3、使用方式

​	1、默认插槽

> ```
> 父组件：
> <myCategory titleName="美食">
>   <div>结构1</div>
> </myCategory>
> 
> 
> 子组件：
> <template>
>     <div>
>         <slot></slot>
>     </div>
> </template>
> ```

​	2、具名插槽

> ```
> 父组件：
> <myCategory>
> 	<template slot="top">
>         <div>结构1</div>
>     </template>
> </myCategory>
> 或
> <myCategory>
> 	<template v-slot:wuwu>
>         <div>结构2</div>
>     </template>
> </myCategory>
> 
> //v-slot写法一定要在template标签中
> 
> 子组件：
> <template>
>     <div>
>         <slot name="haha"></slot>
>         <slot name="wuwu"></slot>
>     </div>
> </template>
> ```

​	3、作用域插槽

​	数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。

> ```
> 父组件：
> <myCategory>
> 	<template scope="top">//top接受的是一个对象，内包含数据
>         <ul>
>           <li v-for="(g,index) in top.games" :key="index">{{g}}</li>
>         </ul>
>     </template>
> </myCategory>
> 
> <myCategory>
> 	<template scope="top">
>         <h4 v-for="(g,index) in top.games" :key="index">{{g}}</h4>
>     </template>
> </myCategory>
> 
> 
> 子组件：
> <template>
>     <div class="category">
>         <h3>{{titleName}}分类</h3>
>         <slot :top="games"></slot>
>     </div>
> </template>
> 
> <script>
>  export default {
>     name:'myCategory',
>     props:['titleName'],
>     data() {
>       return {
>         // foods:['鸡','鸭','鱼','猪'],
>         // films:['阿凡达','哆啦A梦','阿童木','蓝猫'],
>         games:['lol','dota','csgo','dnf']
>       } 
>     }
>  }
> </script>
> ```





## Vuex

### 概念

![image-20221021202450390](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221021202450390.png)

### 搭建

1、创建文件store/index.js

> ```
> //创建Store
> import Vue from 'vue'
> import Vuex from 'vuex'//由于脚手架中都是先运行import，所以需要在该文件中先创建vuex，在使用Vue.use(Vuex)，否则如果在main.js中使用Vue.use会报错。
> Vue.use(Vuex)
> 
> //actions:用于相应组件中的动作
> const actions = {}
> //mutations:用户操作数据(state)
> const mutations = {}
> //state:用于存储数据
> const state = {}
> 
> //创建暴露Store
> export default new Vuex.Store({
>     actions,
>     mutations,
>     state
> })
> ```

2、在`main.js`中创建vm时，传入store配置项

> ```
> import Vue from 'vue'
> import App from './App.vue'
> import Vuex from 'vuex'
> import store from './store/index'
> Vue.config.productionTip = false
> 
> 
> new Vue({
>   render: h => h(App),
>   store,
>   beforeCreate(){
>     Vue.prototype.$bus = this
>   }
> }).$mount('#app')
> ```



### vuex的核心概念

 1). state

  vuex管理的状态对象

  它应该是唯一的

> ```
> const state = {
> 
> ​    xxx: initValue
> 
>   }
> ```

 2). mutations

  包含多个直接更新state的方法(回调函数)的对象,谁来触发: action中的commit('mutation名称'),只能包含同步的代码, 不能写异步代码

> ```
> const mutations = {
> 
> ​    yyy (state, data) { 
> 
> ​      // 更新state的某个属性
> 
> ​    }
> 
>   }
> ```
>
> 

 3). actions

  包含多个事件回调函数的对象，通过执行: commit()来触发mutation的调用, 间接更新state

  谁来触发: 组件中: $store.dispatch('action名称')  // 'zzz'

  可以包含异步代码(定时器, ajax)

> ```
>  const actions = {
> 
>    zzz ({commit, state}, data1) {
> 
>      commit('yyy', data2)
>      
>      }
> 
>   }
> ```

 4). getters

  包含多个计算属性(get)的对象，类似计算属性

  谁来读取: 组件中: $store.getters.xxx

> ```
> const getters = {
> 
> ​    mmm (state) {
> 
> ​      return ...
> 
> ​    }
> 
>   }
> ```

 5). modules

  包含多个module

  一个module是一个store的配置对象

  与一个组件(包含有共享数据)对应



 6). 向外暴露store对象

> ```
>  export default new Vuex.Store({
> 
> ​    state,
> 
> ​    mutations,
> 
> ​    actions,
> 
> ​    getters
> 
>   })
> ```



 7). 组件中:

> ```
>  import {mapGetters, mapActions} from 'vuex'
> 
>   export default {
> 
> ​    computed: mapGetters(['mmm'])
> 
> ​    methods: mapActions(['zzz'])
> 
>   }
> 
> 
> 
>   {{mmm}} @click="zzz(data)"
> 
> ```



 8). 映射store

> ```
>   import store from './store'
> 
>   new Vue({
> 
> ​    store
> 
>   })
> ```



 9). store对象

  1.所有用vuex管理的组件中都多了一个属性$store, 它就是一个store对象

  2.属性:

   state: 注册的state对象

   getters: 注册的getters对象

  3.方法:

   dispatch(actionName, data): 分发action 



### 基本使用

1、初始化数据、配置actions、配置mutations、操作文件store.js

> ```
> //创建Store
> import Vue from 'vue'
> import Vuex from 'vuex'
> Vue.use(Vuex)
> 
> //actions:用于相应组件中的动作
> const actions = {
>     // jia(context,value) {
>     //     context.commit('JIA',value)
>     // },
>     // jian(context,value) {
>     //     context.commit('JIAN',value)
>     // },
>     jiaOdd(context,value) {
>         if(context.state.sum % 2){
>             context.commit('JIA',value)
>         }
>     },
>     jiaWait(context,value) {
>         setTimeout(() => {
>             context.commit('JIA',value)
>         }, 500);
>     }
> }
>     
> //mutations:用户操作数据(state)
> const mutations = {
>     JIA(state,value) {
>         state.sum += value
>     },
>     JIAN(state,value) {
>         state.sum -= value
>     }
> }
> //state:用于存储数据
> const state = {
>     sum:0
> }
> 
> //创建暴露Store
> export default new Vuex.Store({
>     actions,
>     mutations,
>     state
> })
> 
> ```

2、组件中读取vuex数据：`$store.state.sum`

3、组件中修改vuex的数据：`$store.dispatch('action中方法名',数据)`或`$store.commit('mutations中的方法名',数据)`

PS：若没有网络请求或其他业务逻辑，组件中可以直接跨过actions，即不写dispatch，戒指编写commit



### getters的使用

1、当state中数据需要进行加工在使用，可以用getters

2、在`store.js`中追加getters配置

> ```
> const getters = {
>     bigSum(state) {
>         return state.sum * 10
>     }
> }
> ...
> export default new Vuex.Store({
>     ...
>     getters
>     ...
> })
> ```

3、组件中读取：`$store.getters.bigSum`





### 四种Map方法

1、mapState方法:用于帮助我们映射`state`中数据为计算属性

> ```
> computed: {
>     //借助mapstate生成计算属性，从state中读取数据
>     ...mapState({school:'school',subject:'subject'}),
>     //数组写法
>     //...mapState(['school','subject'])
> }
> ```



2、mapGetters方法:用于帮助我们映射`getters`中数据为计算属性

> ```
> computed: {
>     //借助mapstate生成计算属性，从state中读取数据
>     ...mapGetters({bigSum:'bigSum'})
> }
> ```





3、mapActions方法:用于帮助我们生成与`actions`对话的方法，即`$store.dispatch(XXX)`的函数

> ```
> methods: {
>     // increment(){
>     // 	this.$store.commit('JIA',this.n)
>     // },
>     // decrement(){
>     // 	this.$store.commit('JIAN',this.n)
>     // },
> 
>     //借助mapMuatations生成对应的方法，方法中会调用commit去联系mutations（对象写法）
>     ...mapMutations({increment:'JIA', decrement:'JIAN'}),
>     //数组写法
>     //...mapMutations(['JIA', 'JIAN'])
> }
> ```



4、mapMutations方法:用于帮助我们生成与`mutations`对话的方法，即`$store.commit(XXX)`的函数

> ```
> methods: {
>     // incrementOdd(){
>     // 	this.$store.dispatch('jiaOdd',this.n)
>     // },
>     // incrementWait(){
>     // 	this.$store.dispatch('jiaWait',this.n)
>     // }
>     ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
> }
> ```
>
> 



### 模块化 /命名空间

1、目的：让代码更好维护，让多种数据分类更明确。

2、修改`store.js`

> ```
> 
> const countAbout = {
>     namespaced:true,//开启命名空间
>     state:{x:1},
>     mutations:{},
>     actions:{},
>     getters:{}
> }
> 
> const personAbout = {
>     namespaced:true,
>     state:{...},
>     mutations:{},
>     actions:{},
>     getters:{}
> }
> 
> const store = new Vuex.Store({
>     modules:{
>         countAbout,
>         personAbout
>     }
> })
> ```

3、开启命名空间后，组件中读取state数据

> ```
> //方式一：自己直接读取
> this.$store.state.personAbout.list
> //方法二：借助mapState读取
> ...mapState('countAbout',['sum','school','subject']),
> ```

4、开启命名空间后，组件中读取getters数据：

> ```
> //方式一：自己直接读取
> this.$store.getters['personAbout/firstPersonName']
> //方法二：借助mapState读取
> ...mapState('countAbout',['bigSum']),
> ```

5、开启命名空间后，组件中调用dispatch：

> ```
> //方式一：自己直接dispatch
> this.$store.dispatch('personAbout/addPersonWang',person)
> //方法二：借助mapState读取
> ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'}),
> ```

6、开启命名空间后，组件中调用commit

> ```
> //方式一：自己直接commit
> this.$store.commit('personAbout/ADD_PERSON',person)
> //方法二：借助mapMutations读取
> ...mapActions('countAbout',{incrementOdd:'JIA',decrement:'JIAN'}),
> ```





## vue-router

​		vue-router是一个插件库，专门用于实现SPA。需要安装-use 

​		SPA：

​				1、单页Web应用

​				2、整个应用只有一个完整的页面

​				3、点击页面中的导航链接不会刷新页面，只做页面的局部更新

​				4、数据需要通过ajax请求获取

### 路由概念

1、一个路由就是一组映射关系（key-value），key为路径，value为function或component

2、路由分类

​	1.后端路由：

​		1）value是function，用于处理客户端提交的请求

​		2）工作过程：服务器收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

​	2.前端路由：

​		1）理解：value是一个component，用于展示页面内容

​		2）工作过程：当浏览器的路径改变时，对应的组件就会显示。





### 基本使用

1、安装vue-router：`yarn add vue-router`

2、应用插件：`Vue.use(VueRouter)`

3、编写router配置项

> ```
> import VueRouter from "vue-router";
> 
> import About from '../components/About'
> import Home from '../components/Home'
> 
> //新建暴露一个路由器
> export default new VueRouter({
>     routes:[
>         {
>             path:'/about',
>             component:About
>         },
>         {
>             path:'/home',
>             component:Home
>         },
>     ]
> })
> ```

4、实现切换(active-class可配置高亮样式)

> ```
> <router-link class="list-group-item" active-class="active" to="/about">About</router-link>
> ```

5、指定展示位置

> ```
> <router-view></router-view>
> ```



PS：

1、路由组件一般放再pages文件中，一般组件放在components中

2、通过切换，"隐藏"了路由组件，其实默认是被销毁了，需要的时候才去挂在

3、每个组件都有自己的`$route`属性，里面存储着自己的路由信息

4、整个应用只有一个router，可以通过组件的`$router`属性获得

### 多级路由

1、配置路由规则，使用children配置项

> ```
> export default new VueRouter({
>     routes:[
>         {
>             path:'/about',
>             component:About
>         },
>         {
>             path:'/home',
>             component:Home,
>             children:[
>                 {
>                     path:'news',
>                     component:News,
>                 },
>                 {
>                     path:'message',
>                     component:Message,
>                 }
>             ]
>         },
>     ]
> })
> ```



2、跳转（要写完整路径）

> `<router-link *class*="list-group-item" *ative-class*="active" *to*="/home/news">News</router-link>`



### 路由的query参数

1、传递参数

> ```
> <!-- 跳转路由器并携带query参数的to的字符串写法 -->
> <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">{{m.title}}</router-link>&nbsp;&nbsp;
> 
> <!-- 跳转路由器并携带query参数的to的对象写法 -->
> <router-link :to="{
>     path:'/home/message/detail',
>     query:{
>         id: m.id,
>         title: m.title
>     }
> }">
>     {{m.title}}
> </router-link>
> ```



2.接受参数

> `$route.query.id`
>
> `$route.query.title`



### 命名路由

1、作用：可以简化路由的跳转

2、使用

   1、给路由命名：

> ```
> {
>     path:'/home',
>     component:Home,
>     children:[
>         {
>             path:'news',
>             component:News,
>         },
>         {
>             path:'message',
>             component:Message,
>             children:[
>                 {
>                 	name:'hello'//路由命名
>                     path:'detail',
>                     component:Detail,
>                 }
>             ]
>         }
>     ]
> },
> ```



​	2、简化跳转：

> ```
> <!-- 简化前，要写完整路径 -->
> <router-link to="/home/message/detail">{{m.title}}</router-link>
> 
> <!-- 简化后直接名字跳转 -->
> <router-link :to="{name:'hello'}">{{m.title}}</router-link>
> 
> <!-- 简化写法配合传递参数 -->
> <router-link 
> 	:to="{
>     name:'hello',
>     query:{
>         id: m.id,
>         title: m.title
>     }
> }">
>     {{m.title}}
> </router-link>
> ```





### params参数

> ```
> {
>     path:'/home',
>     component:Home,
>     children:[
>         {
>             path:'news',
>             component:News,
>         },
>         {
>             path:'message',
>             component:Message,
>             children:[
>                 {
>                 	name:'hello',
>                     path:'detail/:id/:title',//使用占位符申明接收params参数
>                     component:Detail,
>                 }
>             ]
>         }
>     ]
> },
> ```



2、传递参数

> ```
> <!-- 跳转路由器并携带params参数的to的字符串写法 -->
> <router-link :to="`/home/message/detail/${m.id}/${m.title}`">{{m.title}}</router-link>&nbsp;&nbsp;
> 
> <!-- 跳转路由器并携带query参数的to的对象写法 -->
> <!-- <router-link :to="{
>     name:'hello',
>     params:{
>         id: m.id,
>         title: m.title
>     }
> }">
>     {{m.title}}
> </router-link> -->
> ```

PS：路由携带params参数时，若使用to对象写法，则不用使用path配置项，需要用name配置。

3、接受参数

> ```
> $route.params.id
> $route.params.title
> ```





### 路由的props配置

作用：让路由组件更方便接收参数

用法：

> ```
> {
>     name:'detail',
>     path:'detail/:id/:title',
> //写法一：值为对象，该对象中所有key-value都会以props形式传给Detail组件
> 	props:{a:1 ,b:'ii'}
>                             
> // 写法二：值为布尔值,若布尔值为真，就把该路由组件收到的所有params参数（无法处理query），以props的形式传给Detail组件
> 	props:true,
> 
> 写法三：值为函数
> 	props($route){
> 		return {
> 			id:$route.query.id ,
> 			title:$route.query.title
> 		}
> 	}
> }
> ```



### router-link的replace属性

1、作用：控制路由跳转时操作浏览器历史记录的模式

2、浏览器的历史记录有两种写入方式：分别为push、replace，push是追加历史记录，replace是替代当前记录。路由跳转时默认为push

3、开启replace模式：`<router-link replace :to="`/home/`">111</router-link>`





### 编程式路由导航

1、作用：不借助<router-link>因为router-link会生成a标签，而有些场景需要通过其他标签如button去实现，编程式导航让转跳更灵活。

2、方法：

> ```
> //$router中两个API,其实就是routelink中:to中的配置项
> this.$router.push({
> 	name:'haha',
> 	params:{
> 		id：1,
> 		title:'232'
> 	}
> })
> 
> this.$router.replace({
> 	name:'haha',
> 	params:{
> 		id：1,
> 		title:'232'
> 	}
> })
> 
> this.$router.forward()//向前跳
> this.$router.back()//向后跳
> this.$router.go(数字)//向前跳几次
> ```

### 缓存路由组件

1、作用：让不展示的路由组件保持挂载，不被销毁

2、具体变化：

> ```
> <keep-alive include='News'>
> 	 <router-view></router-view>
> </keep-alive>
> ```
>
> PS:include中的为组件名，若不写该属性，router-viewer中所有组件都会被保留。



### 两个新的生命周期钩子

1、作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态

2、具体名字：

​	1、`activated(){}`路由组件被激活时触发

​	2、`deactivated(){}`路由组件被失活时触发





### 路由守卫

作用：对路由进行权限控制

分类：全局守卫、独享守卫、组件内守卫

全局守卫：

> ```
> //全局前置路由守卫——初始化时被调用、每次路由切换之前被调用
> router.beforeEach((to, from, next)=>{
>     if(to.meta.isAuth){//判断是否需要鉴权
>         if(localStorage.getItem('school')==='atguigu'){//权限控制规则
>             next()
>         }else{
>             alert('无权限！')
>         }
>     }else{
>         next()
>     }
> })
> 
> 
> //全局后置路由守卫——初始化时被调用、每次路由切换后被调用
> router.afterEach((to, from)=>{
>     document.title = to.meta.title || '主页'
> })
> 
> 
> export default router
> ```



独享守卫：

> ```
> beforeEnter: (to, from, next) => {
>     if(to.meta.isAuth){//判断是否需要鉴权
>         if(localStorage.getItem('school')==='atguigu'){
>             next
>         }else{
>             alert('无权限！')
>         }
>     }else{
>         next()
>     }
> }
> ```



组件内路由守卫：

> ```
> //进入守卫：通过路由规则，进入该组件时被调用
> beforeRouteEnter (to, from, next) {
>       
> }
> //离开守卫：通过路由规则，进入该组件时被调用
> beforeRouteLeave (to, from, next) {
>       
> }
> ```



### 路由器的两种工作模式

1、url的hash值：#及后面的内容就是hash值

2、hash值不会包含在HTTP请求中，即：hash值不会带给服务器

3、hash模式：

​	1、地址中永远带着#号

​	2、若以后将地址通过第三方手机app分享，若app校验严格，则地址会标记为不合法

​	3、兼容性较好

4、history模式

​	1、地址没有#

​	2、兼容性相对较差

​	3、应用部署上线需要后端支持，解决刷新服务端404问题





# Vue3

## vue-cli创建

> ```
> //版本需要在4.5.0以上
> //安装vue-cli
> yarn add -g @vue/cli
> 
> //创建
> vue create vue_test
> 
> //启动
> cd vue_test
> yarn serve
> ```





## vite创建

> ```
> //全局安装vite
> yarn add global create-vite-app
> 
> //创建
> yarn create vite-app <project-name>
> 
> //进入目录
> cd <project-name>
> 
> //下载依赖
> yarn
> 
> //运行项目
> yarn dev
> ```



## Composition API

### setup

1、setup为Vue3中的一个新的配置项，值为一个函数

2、组件所需的数据、方法均要配置在setup中

3、setup中两种返回值

​	（1）若返回一个对象，则对象中的属性、方法在模板中均可以直接使用

> ```
> return {
> 	name,
> 	age,
> 	hi
> }
> ```

​	（2）若返回一个渲染函数，则可以自定义渲染内容

> ```
> return () => h('h1','哈喽')
> ```

渲染函数会覆盖普通对象

4、注意点

​	（1）尽量不要在Vue2.x配置混用

			* Vue2.x配置（data、methods....）可以访问到setup中属性、方法
			* 但在setup中不能访问到Vue2.x配置
			* 如果由重名，setup优先

​	（2）set不能是一个async函数，因为返回值不再是一个return对象，而是promise，模板看不到return对象中的属性。



### ref函数

* 用于定义一个响应式数据

* 语法：`const x = ref(initValue)`

  * 创建一个包含响应式数据的引用对象(reference对象 RefImpl)
  * JS中操作数据：`xxx.value`
  * 模板中读取数据：不需要.value，直接：`<div>{{xxx}}</div>`

  PS：

  1、接收数据可以是：基本类型或对象类型

  2、基本类型的数据：响应式依然是靠`object.defineProperty()`的get和set完成的

  3、对象类型的数据：内部请求了Vue3中的新函数—reactive函数

* 

### reactive函数

作用：定义一个对象类型的响应式数据

语法：`const x = reactive(initValue)`接收一个对象（或数组），返回一个代理对象（proxy对象）

reactive定义的响应式数据是深层次的

内部基于ES6的Proxy实现，通过代理对象操作元对象内部数据进行操作

 



## Vue3中响应式原理

### vue2响应式

![image-20221025210135445](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221025210135445.png)



### vue3响应式

![image-20221025215325767](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221025215325767.png)

## reactive对比ref

![image-20221025215542125](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221025215542125.png)

## setup的两个注意点

![image-20221025223143559](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221025223143559.png)



## 计算属性与监视

### computed函数

![image-20221025224127945](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221025224127945.png)



### watch函数

* 与Vue2中watch配置功能一直

* 两个坑

  1、监视reactive定义的响应式数据时，oldValue无法正确获取、强制开启了深度监视（deep配置失效）

  2、监视reactive定义的响应式数据中某个属性时，deep配置有效

![image-20221026194810705](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221026194810705.png)![image-20221026194822522](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221026194822522.png)



### watchEffect函数

![image-20221026200206161](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221026200206161.png)



## vue3生命周期

![img](https://img-blog.csdnimg.cn/a591b3781c3e4bc3be19b3383bc745b6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAeGlhb0xpYW5nIG8=,size_15,color_FFFFFF,t_70,g_se,x_16)



## 自定义hook函数

* hook：本质为一个函数，将setup函数中使用的Composition API进行封装
* 类似vue2中的minxin
* 自定义hook的优势：复用代码

## toRef

* 作用：创建一个ref对象，其value值指向另一个对象中的某个属性
* 语法：`const name = toRef(person, 'name')`
* 应用：要将响应式对象中的某个属性单独提供给外部使用时
* 扩展：`toRefs`和`toRef`功能一样，但可以批量创建多个ref对象 ；语法:`toRefs(person)`





## 其他Composition API

### shallowReactive和shallowRef

* shallowReactive：只处理对象最外层属性的响应式（浅响应式）

* shallowRef：值处理基本数据类型的响应式，不处理对象的响应式

* 使用场景：

  ** 如果有一个对象数据，结构比较深，但变化时只是外层属性变化===>shallowReactive

  ** 如果有一个对象数据，后续功能不会修改该对象中的属性，而是生成新的对象代替===>shallowRef



### readonly和shallowReadonly

* readonly：让一个响应式数据变为只读（深只读）
* shallowReadonly：同上（浅只读）



### toRaw与markRaw

* toRaw：

  作用：将一个由`reactive`生成的响应式对象转为普通对象

  使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。

* markRaw：

  作用：标记一个对象，使其永远不会再成为响应式对象

  应用场景：

  1、有些值不应被设置为响应式的

  2、当渲染具有不可变数据源的大列表，跳过响应式转换为可以提高性能





### customRef

作用：创建一个自定义的ref，并对其依赖项跟踪和更新触发进行显式控制。

喜欢防抖效果：

> ```
> import { customRef } from 'vue'
> 
> export function useDebouncedRef(value, delay = 200) {
>   let timeout
>   return customRef((track, trigger) => {
>     return {
>       get() {
>         track()//告诉vue这个value值是需要被追踪的
>         return value
>       },
>       set(newValue) {
>         clearTimeout(timeout)
>         timeout = setTimeout(() => {
>           value = newValue
>           trigger()//通知vue去重新解析模板
>         }, delay)
>       }
>     }
>   })
> }
> 
> ```



`customRef()` 预期接收一个工厂函数作为参数，这个工厂函数接受 `track` 和 `trigger` 两个函数作为参数，并返回一个带有 `get` 和 `set` 方法的对象。

一般来说，`track()` 应该在 `get()` 方法中调用，而 `trigger()` 应该在 `set()` 中调用。然而事实上，你对何时调用、是否应该调用他们有完全的控制权。



### provide和inject

作用：实现祖孙组件间通信

原理：父组件通过provide提供数据，子组件通过inject接收数据

写法：

> ```
> //父组件
> setup() {
> 	...
> 	let car = reactive({name:'奔驰',price:'400K'})
> 	provide('car',car)
> 	...
> }
> 
> //子组件
> setup() {
> 	...
> 	const car = inject('car')
> 	return {car}
> 	...
> }
> ```





### 响应式数据判断

* isRef:检查一个值是否为一个ref对象
* isReactive:检查一个对象是否由reactive创建的响应式代理
* isReadonly:检查一个对象是否由readonly创建的只读代理
* isProxy:检查一个对象是否由reactive或readonly创建的代理



## Vue3新组件

### Fragment

Vue2中组件必须有一个根标签div包含

Vue3中组件恶意没有根标签，内部会将多个标签包含再一个Fragment虚拟元素中



### Teleport

Teleport可以让我们组件html结构移动到指定位置的技术

>```
>  <teleport to='移动位置'>
>    <div v-if="isShow" class="mask">
>      <div class="dialog">
>        <h3>弹窗~</h3>
>        <button @click="isShow = false">关闭弹窗</button>
>      </div>
>    </div>
>  </teleport>
>```

