# Webpack基本使用

## 基本介绍

webpack是一个前端构建工具。前端构建工具就是把开发环境的代码转化成运行环境代码。一般来说，开发环境的代码是为了更好的阅读，而运行环境的代码则是为了能够更快地执行。例如使用node.js编写js/html/css代码，再通过webpack打包成浏览器可以识别的js/html/css代码。

- 代码压缩

将JS、CSS代码混淆压缩，让代码体积更小，加载更快

- 编译语法

编写CSS时使用Less、Sass，编写JS时使用ES6、TypeScript等，这些标准目前都无法被浏览器兼容，因此需要构建工具编译，例如使用Babel编译ES6语法。

- 处理模块化：

CSS和JS的模块化语法，目前都无法被浏览器兼容。因此开发环境可以使用既定的模块化语法，但是需要构建工具将模块化语法编译为浏览器可识别形式。例如使用webpack、Rollup等处理JS模块化。





## 安装使用

> ```
> yarn init -y // 初始化配置文件
> yarn add webpack webpack-cli --dev//将webpack的依赖安装到开发者依赖中
> ```



在当前目录创建src文件，存放源代码。

![image-20220921113123576](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220921113123576.png)

> ```
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta http-equiv="X-UA-Compatible" content="IE=edge">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <title>Document</title>
> </head>
> <body>
>     <h1>hello world</h1>
>     <script src="./src/index.js"></script>
> </body>
> </html>
> ```

## 代码打包

> npx webpack   

打包完成后，当前目录会生成一个dist文件，dist文件中存在一个main.js，其为index.js的转义代码。

![image-20220921201612312](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220921201612312.png)

可以将index.html的导入文件改为main.js的路径。



## webpack配置文件

创建配置文件webpack.package.json可以修改入口JS文件，判断从哪个文件开始寻找依赖的路径；可以配置出口文件，即出口JS文件生成的信息；通过loader加载不同类型的文件；再通过plugins，在打包过程中对代码进行优化。



> ```
> {
> "name": "blog",
> "version": "1.0.0",
> "main": "index.js",
> "scripts": {
> //可以通过build命令直接执行webpack
>     "build": "webpack"
>   },
> "license": "MIT",
> "devDependencies": {
>  "webpack": "^5.74.0",
>  "webpack-cli": "^4.10.0"
> }
> } 
> ```



## 加载配置loader

npx webpack无法直接转移css文件，需要安装两个loader

> yarn add --dev style-loader css-loader

之后需要在配置文件中进行配置loader进行文件匹配，以何种扩展名结尾的文件对应应用何种loader。

> ```
> module:{
>      rules:[{
>      	 //test指定的是规则生效的文件
>          test: /\.css$/i,
>          //要使用的loader
>          use: ["style-loader","css-loader"],
>          //要排除的文件
>          exclude: /node-modules/
>      }
>      ],//数组中每个元素对应一个loader配置
>  }
> ```

对于图片这种静态类型文件，不需要使用loader匹配。

直接在配置文件中配置即可。

> ```
> rules:[{
>             test: /\.css$/i,
>             use: ["style-loader","css-loader"],
>         },{
>             test: /\.(png|svg|jpg|jpeg|gif)&/i,
>             type:"asset/resource",
>         }
>         ]
> ```





## 插件使用

### 1、html插件

手动编写html文件的插件，html-webpack-plugin

> yarn add --dev html-webpack-plugin

在配置文件中进行配置

首先导入

> `const HtmlWebpackPlugin = require("html-webpack-plugin");`

再在module.exports中写入Plugin

> ```
> module.exports = {
>     ...
>     plugins:[new HtmlWebpackPlugin()],
>    	...
>     }
> ```

HtmlWebpackPlugin()中也可以进行配置=>HtmlWebpackPlugin({title: " ",template:"模板路径"})





### 2、兼容性插件

可以使用babel-loader @babel/core @babel/preset-env实现

> `yarn add --dev babel-loader @babel/core @babel/preset-env`

在配置文件中配置

> ```
> {
>             test:/\.js&/,
>             exclude:/node_modules/,
>             use:{
>                 loader: "babel-loader",//使用对象形式，方便给loader传递自定义配置
>                 options:{
>                     presets:["@babel/preset-env"],//自定义配置
>                 },
>             }
> ```



### 3、压缩打包后代码容量插件

使用terser-webpack-plugin

>  yarn add --dev terser-webpack-plugin

在配置文件中配置

> ```
> const TerserPlugin = require("terser-webpack-plugin");
> 
> module.exports = {
>     ...
>     optimization: {
>         minimize:true,
>         minimizer:[new TerserPlugin()],
>     },
>    	...
>     }
> ```





## 自动打包

安装webpack-dev-server

> yarn add --dev webpack-dev-server

在配置文件中配置

> ```
> const TerserPlugin = require("terser-webpack-plugin");
> 
> module.exports = {
>     ...
>     devServer:{
>         static:"./dist",
>     },
>    	...
>     }
> ```

在package.json中添加一个script用于启动webpack-server开发服务器

> ```
>   "scripts": {
>     "start": "webpack serve --open"
>   },
> ```

然后在命令行中运行`yarn start`即可启动服务。



## 避免浏览器缓存

由于浏览器会根据dist.js文件名进行缓存，为了避免此情况。给浏览器生成随机字符，每次更新js都会生成随机字符。

在配置文件中的filename进行修改

> ```
> filename: "[name].[contenthash].js"
> ```



## 给访问路径设置别名

为了避免访问其他文件的JS，而写入十分麻烦的相对路径。

webpack可以指定路径别名去取代相对路径。

> ```
> reslove:{
> 	alias:{
> 		别名:path.resolve(__dirname,"真实路径");
> 	}
> }
> ```





## 可视化打包分析工具

webpack-bundle-analyzer

>`yarn add --dev webpack-bundle-analyzer`

在配置文件中配置

> ```
> const BundleAnalyzerPlugin = require("webpack-bundle-analyzer").BundleAnalyzerPlugin;//BundleAnalyzerPlugin是对象，需要调用里面的构造函数所以加.BundleAnalyzerPlugin
> 
> 
> module.exports = {
>     ...
>     plugins:[
>         new HtmlWebpackPlugin({
>             title:"Blog!"
>         }),
>         new WebpackBundleAnalyzerPlugin.WebpackBundleAnalyzerPlugin(),
>     ],
>    	...
>     }
> ```

![image-20220921230409594](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220921230409594.png)