## JSON

## JSON类型

> ```
> {
> 	"key1":"a",//字符串
> 	"key2":123,//数字，长度不限
> 	"key3":{},//对象
> 	"key4":[],//数组
> 	"key5":[{},{},{}],//数组对象
> 	"key6":null,//空
> }
> 
> 取法：
> 普通类型：直接通过键名取得
> 对象类型：键名.属性
> 数组类型：键名[索引号]
> 
> ```
>
> 

## 键值对

JSON键值对是用于保存JS对象的一种方式，键值对组合中的键名写在前面并用双引号包裹，使用冒号分隔，再紧跟值。

> `{"name":"Tom"}`

JSON是JS对象的字符串表示法，使用文本表示一个JS对象的信息，本质是字符串。

> ```
> var obj = {name: 'Tom'};//对象
> var json = '{"name":"Tom"}';JSON字符串
> ```



## JSON与JS转换

JSON字符串 => JS对象，使用JSON.parse()方法

> `var obj = JSON.parse('{"name":"Tom"}') `//结果：var obj = {name: 'Tom'};

JS对象 => JSON字符串，使用JSON.stringify()方法

> `var json = JSON.stringify({name: 'Tom'})'`//结果：var json = '{"name":"Tom"}'

