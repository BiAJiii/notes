# AJAX

AJAX即异步JS和XML，无刷新获取数据。

优点：1、无需刷新即可实现通信 2、允许根据用户事件来更新部分页面内容

缺点：1、没有浏览历史 2、有跨域问题 3、SEO不友好

## XML

XML为可扩展标记语言，没有类似HTML的预定义标签，（如：<a><div>），全为自定义

> ```
> <student>
> 	<name>tom<name/>
> 	<age>18<age/>
> <student/>
> ```

现一般用JSON替代



## HTTP

### 请求报文

行：请求类型/url/http协议版本  => POST / s?ie=utf-8 HTTP/1.1

头：Host：baidu.com

​		Cookies: name=baidu

​		Content-type: application/x-www-form-urlcoded

​		User-Agent: Chorme 80

空行

体：GET为空 POST可以不为空 => username=admin&password=admin



## 响应报文

行：协议版本/响应状态码/响应状态字符串  => HTTP/1.1   200   OK

头：Content-type: text/html

​		Content-length: 2048

​		Content-encoding: gzip

​		//对响应一些属性的描述

空行

体：<html>

​			<head><head/>

​			<body>

​				<h1>hello<h1/>

​			<body/>

​		<html/>



## XMLHttpRequest

​		使用XMLHttpRequest (XHR)对象可以与服务器交互。您可以从URL获取数据，而无需让整个的页面刷新。这使得Web页面可以只更新页面的局部，而不影响用户的操作。XMLHttpRequest在 Ajax 编程中被大量使用。



### onreadystatechange

只要 readyState 属性发生变化，就会调用相应的处理函数。这个回调函数会被用户线程所调用。

|  值  |       状态       |                       描述                        |
| :--: | :--------------: | :-----------------------------------------------: |
|  0   |      UNSENT      |       代理被创建，但尚未调用 open() 方法。        |
|  1   |      OPENED      |              open() 方法已经被调用。              |
|  2   | HEADERS_RECEIVED | send() 方法已经被调用，并且头部和状态已经可获得。 |
|  3   |     LOADING      |   下载中； responseText 属性已经包含部分数据。    |
|  4   |       DONE       |                 下载操作已完成。                  |



## express框架

直接添加express依赖，并导入，即可使用

> ```
> //1.引入express
> const express = require('express');
> 
> //2.创建应用对象
> const app = express();
> 
> //3.创建路由规则
> //request是对请求报文的封装
> //response是对响应报文的封装
> app.get('/',(request,response)=>{
> 	//设置允许跨域
>     response.setHeader('Access-Control-Allow-Origin','*');
>     response.send('Hello world!');
> });
> 
> 
> 
> //4. 监听端口启动服务
> app.listen(8000,()=>{
>     console.log("服务已启动，8000端口监听中...");
> });
> ```
>
> node express 启动服务





## 基本请求交互

后端：

> ```
> //1.引入express
> const express = require('express');
> 
> //2.创建应用对象
> const app = express();
> 
> //3.创建路由规则
> //request是对请求报文的封装
> //response是对响应报文的封装
> app.get('/server',(request,response)=>{
>     response.setHeader('Access-Control-Allow-Origin','*');
>     response.send('Hello world!');
> });
> 
> app.post('/server',(request,response)=>{
>     response.setHeader('Access-Control-Allow-Origin','*');
>     response.send('Hello POST!');
> });
> //4. 监听端口启动服务
> app.listen(8000,()=>{
>     console.log("服务已启动，8000端口监听中...");
> });
> ```





前端：

> ```
> <body>
>     <button>发送请求</button>
>     <div class="result"></div>
>     <script>
>         var btn = document.querySelector('button');
>         var result = document.querySelector('.result');
>         btn.onclick = function(){
>             //1.创建对象
>             const xhr = new XMLHttpRequest();
>             //2.初始化 设置请求方法和请求对象的url
>             //传参是在server后面加个?然后设置
>             //如：http://127.0.0.1:8000/server?a=100
>             xhr.open('get','http://127.0.0.1:8000/server');
>             //设置请求头
>             xhr.setRequestHeader('Content-type'，'text/html)
>             //3.发送
>             //send中可以传入请求体 如xhr.send('a=1&b=2')
>             xhr.send();
>             //4.事件绑定 处理服务端返回的结果
>             // readystate是xhr对象中的属性，表示状态0 1 2 3 4
>             // 0：未初始化  1：open方法调用完毕  2：send方法调用完毕  3：服务端返回部分结果 4：服务端返回所有结果
> 
>             xhr.onreadystatechange = function(){
>                 //判断服务器是否返回了所有结果
>                 if(xhr.readyState===4){
>                     //判断响应状态码 200 404 403 500
>                     //2xx 都是成功
>                     if(xhr.status >=200 && xhr.status <300){
>                         //处理结果 行 头 空行 体
>                         // xhr.status为状态码
>                         // .statusText为状态字符串
>                         // .getAllRespenseHeaders为所有响应头
>                         // .response为响应体
>                         result.innerHTML = xhr.response;
>                     }
>                 }
> 
>             }
>         }
>     </script>
> </body>
> ```





## 服务端响应JSON

可以通过设置响应体数据类型完成JSON自动转换。

> xhr.responseType = 'JSON'L





## 请求超时与网络异常

* 超时设置

> `xhr.timeout = 2000;`

* 超时回调

> `xhr.ontimeout = function(){};`

* 网络异常回调

> `xhr.onerror = function(){};`

* 取消请求

> `xhr.abort();`



## jQuery发送AJAX

> ```
> $('button').eq(0).click(function(){
>             $.请求类型('url',参数,回调函数,响应体数据类型)
>         })
> ```

如:

> ```
> $('button').eq(0).click(function(){
>             $.get('http://127.0.0.1:8000/server',{a:2,b:3},function(data){
>                 console.log('jQuery Hi~')
>             },'json')
>         })
> ```



* 通用方法发送请求

> ```
> $('button').eq(0).click(function(){
>             $.ajax({
>             	url:'',
>             	//参数
>             	data: {},
>             	//请求类型
>             	type:'',
>             	//响应体类型
>             	dataType:'',
>             	//成功的回调
>             	success:function(){
>             		console.log('')
>             	},
>             	//超时事件
>             	timeout:1000,
>             	//失败的回调
>             	error:function(){
>             	
>             	},
>             	//头信息
>             	headers: {
>             		
>             	}
>             })
>         })
> ```



## Axios

* POST类型配置

> ```
> // Send a POST request
> axios({
>   method: 'post',
>   url: '/user/12345',
>   //请求体
>   data: {
>     firstName: 'Fred',
>     lastName: 'Flintstone'
>   }
> });
> ```



* GET类型配置

> ```
> // GET request for remote image in node.js
> axios({
>   method: 'get',
>   url: 'https://bit.ly/2mTM3nY',
>   responseType: 'stream'
> })
>   .then(function (response) {
>     response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
>   });
> ```



不同请求类型配置

> ```
> axios#request(config)
> axios#get(url[, config])
> axios#delete(url[, config])
> axios#head(url[, config])
> axios#options(url[, config])
> axios#post(url[, data[, config]])
> axios#put(url[, data[, config]])
> axios#patch(url[, data[, config]])
> axios#getUri([config])
> ```



## 跨域问题

### JSONP

只支持get请求，通过script标签的跨域能力实现跨域发送请求的

请求端：

> ```
> $('button').eq(0).click(function(){
> 	//?callback=?为固定写法
> 	$.getJSON('http://127.0.0.1:8000/jquery-server?callback=?',function(data){
> 		console.log(${data.name})
> 	})
> })
> ```

服务端：

> ```
> app.all('/jquery-server',(request,response)=>{
>     response.setHeader('Access-Control-Allow-Origin','*');
>     response.setHeader('Access-Control-Allow-Header','*');
>     const data1 = {name:'sam'};
>     //将数据转化为字符串
>     let str = JSON.stringify(data1);
>     //接受callback的参数,为一段字符串,其实就是某一函数的名字
>     let cb = request.query.callback;
>     //返回结果 一段JS代码 这段代码在前端执行后其实就行后端返回的data1对象，既data1==data
>     response.end(`${cb}(${str})`);
> });
> ```



### CORS

官方跨域解决方案，在服务端进行处理，支持get和post请求。

CORS新增了一组HTTP首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源。

工作原理：通过设置一个响应头告诉浏览器，该请求允许跨域，浏览器收到该响应后会对响应放行。

> response.setHeader("Access-Control-Allow-Origin","*")