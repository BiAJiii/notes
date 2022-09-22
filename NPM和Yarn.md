# NPM

## 安装配置

> 1、全局安装    npm install xxx -g

> 2、设置下载镜像  
>
> npm config set registry https://registry.npm.taobao.org --global 
>
> npm config set registry https://npm.taobao.org/dist --globa
>
> > 查看配置结果
> >
> > npm config get registry
> >
> > npm config get disturl



## NPM常用命令

> npm -v 查看版本信息
>
> npm install <Module Name>  使用npm命令安装模块
>
> npm install <Module Name>  -g 全局安装，可直接在命令行里使用
>
> npm list -g 查看所有全局安装的模块
>
> npm list vue 查看某个模块的版本号
>
> npm -g install npm@版本号  进行npm的版本更新
>
> npm install -save moduleName   # -save 在package文件的dependencies节点写入依赖（dependencies：运行时的依赖，发布后，即生产环境下还需要用的模块）
>
> npm install -save-dev moduleName # -save-dev 在package文件的devDependencies节点写入依赖（devDependencies：开发时的依赖，模块是开发时用的，发布时不用，这些模块在项目部署之后不再需要）

![image-20220916201739651](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916201739651.png)



# Package.json 属性说明

 ![image-20220916200449918](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916200449918.png)

> npm install 会根据别人给的扩展包，将配置好的配置文件下载下来



## Package.json配置

> npm init --yes



# 包的使用

> 在没有webpack打包前，需要通过搜索整个node_module文件目录去定位包的路径，再手动导入到html中，如<script src="xxx”>；
>
> 其实也有很多其他方便快接的方式导入
>
> 1、CommonJS
>
> 2、使用require语句导入包  =>   let pac = require("jquery")，会自动搜索到模块所在位置。
>
> 3、使用E6的import导入包  ，三种导入方式
>
> * import {结构对象的属性} from '/path'       导入接口
>
> * import不导入文件对象，即仅是使用文件模块提供的功能。使用import直接引用一个文件时，会执行一遍这个文件，而不获取任何文件对象。
>
>   * `import './lib/init.js';`
>
> * import动态导入
>
>   * ```
>     import("./m1.js").then(m=>{
>       console.log('then:',m)
>     })
>     ```





## ES6兼容性解决

![image-20220916203801104](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916203801104.png)





* 在客户端渲染，可以直接使用babel，但这样用户加载时候很慢
* 在客户端渲染，可按如下步骤

![image-20220916204111769](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916204111769.png)







# Yarn

## 基本常识

### 1、什么是包？

   package.json 用于存放download的模组。



### 2、 什么是包管理器

npm和yarn都是通过以下初始化，生成package.json

>  `npm/yarn init`

安装好的模组都会放进package.json中以便之后调用。



### 3、yarn镜像设置

> yarn config set registry `https://registry.npm.taobao.org -g`





## 常用命令

- [`yarn add`](https://classic.yarnpkg.com/en/docs/cli/add)：添加要在当前包中使用的包。
- [`yarn init`](https://classic.yarnpkg.com/en/docs/cli/init): 初始化一个包的开发。
- [`yarn install`](https://classic.yarnpkg.com/en/docs/cli/install): 安装`package.json`文件中定义的所有依赖项。
- [`yarn publish`](https://classic.yarnpkg.com/en/docs/cli/publish): 将包发布到包管理器。
- [`yarn remove`](https://classic.yarnpkg.com/en/docs/cli/remove)：从当前包中删除未使用的包。

* 默认命令：若不适用yarn开头，将默认运行yarn install开头
* yarn add ：添加依赖
* yarn audit ：对已安装的软件包执行漏洞审核
* yarn autoclean ：从程序包依赖项中清除并删除不必要的文件
* yarn bin ：显示依赖bin文件夹的位置
* yarn cache：管理用户目录中的依赖缓存
* yarn check ：验证当前项目中程序包依赖项
* yarn config ：管理依赖配置文件
* yarn create ：创建Yarn工程
* yarn dedupe：删除重复的依赖
* yarn generate-lock-entry ：生成Yarn锁文件
* yarn global ：在全局安装依赖
* yarn help ：显示Yarn的帮助信息
* yarn import ：迁移当前依赖的项目package-lock.json
* yarn info ：显示有关依赖的信息
* yarn init ：初始化工程并创建package.json文件
* yarn install ：用于安装项目的所有依赖项
* yarn licenses ：列出已安装依赖的许可证及源码url
* yarn link： 链接依赖文件夹
* yarn list ：列出已安装的依赖
* yarn login ：存储您在 registry 上的用户名和 email
* yarn logout ：清除你在 registry 上用户名和 email
* yarn outdated ：列出所有依赖项的版本信息
* yarn owner： 展示依赖作者
* yarn pack： 创建依赖项的压缩gzip
* yarn policies ：规定整个项目中执行Yarn的版本
* yarn publish ：将依赖发布到npm注册表
* yarn remove ：删除依赖
* yarn run ：运行定义的程序脚本命令
* yarn tag ：在依赖上添加，删除或列出标签
* yarn team： 管理组织中的团队，并更改团队成员身份
* yarn test ：运行程序的test命令
* yarn upgrade ：将指定依赖升级为最新版本
* yarn upgrade-interactive ：更新过期依赖的简便方法
* yarn version ：展示依赖版本信息
* yarn versions ：展示所有依赖项版本信息
* yarn why ：显示有关为什么安装依赖的信息
* yarn workspace Yarn：的工作区信息
* yarn workspaces Yarn：的所有工作区信息
  

![image-20220916205443059](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916205443059.png)

![image-20220916205512276](C:\Users\Samuel\AppData\Roaming\Typora\typora-user-images\image-20220916205512276.png)