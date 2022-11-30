# TypeScript

## 开发环境搭建

![image-20221110194530251](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221110194530251.png)

## 基本类型

![image-20221110202928883](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221110202928883.png)

![image-20221110203203596](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221110203203596.png)

## 配置选项

![image-20221111201813362](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221111201813362.png)

![image-20221111201845473](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20221111201845473.png)

> ```
> {
>     // ts编译器的配置文件，ts编译器可根据它的信息来对代码进行编译
>     // include：指定需要被编译的ts文件
>     //     路径：/** 表示任意目录 /*表示任意文件
>     "include": [
>         "./src/**/*"
>     ],
>     "exclude": [
> 
>     ],
>     //compilerOptions编译器的选项
>     "compilerOptions": {
>         "target": "ES6",
>         //模块化 指定使用的模块化的规范  (es6,commonjs,and,system....)
>         "module": "ES6",
>         //lib 用于指定项目中要使用的库 如 (dom es6...) 
>         // "lib":[],
>          //outDir 用于指定编译后文件所在的目录
>          "outDir": "./dist",
>          //将代码合并为一个文件
>         //  "outFile": "./dist/app.js"
> 
>         //是否对js文件进行编译，默认false
>         // "allowJs": false,
> 
>         //是否检查js代码是否符合语法规范
>         // "checkJs": false
> 
>         //是否移除注释
>         "removeComments": true,
> 
>         //不生成编译后的文件
>         // "noEmit": true
> 
>         //当有错误时，不生成编译后的文件
>         "noEmitOnError": true,
> 
>         
>         //所有严格检查的总开关
>         "strict": true,
> 
>         //严格模式
>         // "alwaysStrict": true
> 
>         //不允许隐式any类型
>         "noImplicitAny": true,
> 
>         //不允许不明确的this类型
>         "noImplicitThis": true,
> 
>         //严格检查空值 如将不存在的元素复制给一个属性，这个属性其实是空值
>         "strictNullChecks": true,
>     }
> }   
> ```

## webpack

步骤：

1、初始化项目

- 进入项目根目录，执行命令

   

  ```
  npm init -y
  ```

  - 主要作用：创建package.json文件

2、下载构建工具

* `npm i -D webpack webpack-cli webpack-dev-server typescript ts-loader clean-webpack-plugin`

共安装了7个包

* webpack
  构建工具webpack
* webpack-cli
  webpack的命令行工具
* webpack-dev-server
  webpack的开发服务器，可使用浏览器打开，且会对代码进行监视。 
* typescript
  ts编译器
* ts-loader
  ts加载器，用于在webpack中编译ts文件
* html-webpack-plugin
  webpack中html插件，用来自动创建html文件
* clean-webpack-plugin
  webpack中的清除插件，每次构建都会先清除目录

3、根目录下创建webpack的配置文件webpack.config.js

- ```
  const path = require("path");
  const HtmlWebpackPlugin = require("html-webpack-plugin");
  const { CleanWebpackPlugin } = require("clean-webpack-plugin");
  
  module.exports = {
      optimization:{
          minimize: false // 关闭代码压缩，可选
      },
  
      entry: "./src/index.ts",
      
      devtool: "inline-source-map",
      
      devServer: {
          contentBase: './dist'
      },
  
      output: {
          path: path.resolve(__dirname, "dist"),
          filename: "bundle.js",
          environment: {
              arrowFunction: false // 关闭webpack的箭头函数，可选
          }
      },
  
      resolve: {
          extensions: [".ts", ".js"]
      },
      
      module: {
          rules: [
              {
                  test: /\.ts$/,
                  use: {
                     loader: "ts-loader"     
                  },
                  exclude: /node_modules/
              }
          ]
      },
  
      plugins: [
          new CleanWebpackPlugin(),
          new HtmlWebpackPlugin({
              title:'TS测试'
          }),
      ]
  
  }
  ```

4、根目录下创建tsconfig.json，配置可以根据自己需要

- ```
  {
      "compilerOptions": {
          "target": "ES2015",
          "module": "ES2015",
          "strict": true
      }
  }
  ```

5、修改package.json添加如下配置

* ```
  {
    ...略...
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack",
      "start": "webpack serve --open chrome.exe"
    },
    ...略...
  }
  ```

6、在src下创建ts文件，并在并命令行执行`npm run build`对代码进行编译，或者执行`npm start`来启动开发服务器



## Babel

经过一系列的配置，使得TS和webpack已经结合到了一起，除了webpack，开发中还经常需要结合babel来对代码进行转换以使其可以兼容到更多的浏览器，在上述步骤的基础上，通过以下步骤再将babel引入到项目中。

1、安装依赖包：

* npm i -D @babel/core @babel/preset-env babel-loader core-js
  共安装了4个包，分别是：

  @babel/core//babel的核心工具
  @babel/preset-env//babel的预定义环境
  @babel-loader//babel在webpack中的加载器
  core-js//core-js用来使老版本的浏览器支持新版ES语法

2、修改webpack.config.js配置文件

> ```
> ...略...
> module: {
>     rules: [
>         {
>             test: /\.ts$/,
>             use: [
>                 {
>                     loader: "babel-loader",
>                     options:{
>                         presets: [
>                             [
>                                 "@babel/preset-env",
>                                 {
>                                     "targets":{
>                                         "chrome": "58",
>                                         "ie": "11"
>                                     },
>                                     "corejs":"3",
>                                     "useBuiltIns": "usage"
>                                 }
>                             ]
>                         ]
>                     }
>                 },
>                 {
>                     loader: "ts-loader",
> 
>                 }
>             ],
>             exclude: /node_modules/
>         }
>     ]
> }
> ...略...
> ```

- 如此一来，使用ts编译后的文件将会再次被babel处理，使得代码可以在大部分浏览器中直接使用，可以在配置选项的targets中指定要兼容的浏览器版本。