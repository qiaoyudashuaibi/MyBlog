---
title: （三）使用Vue CLI（v4.0.5）创建一个项目
date: 2019-11-15 13:46:09
tags: VUE
---
什么是Vue CLI？
Vue CLI是一个基于Vue.js进行快速开发的完整系统。

可以做什么？
1.搭建交互式的项目脚手架。
2.快速开始零配置原型开发。
3.可作为一个运行时的依赖。该依赖：
·可升级。
·基于webpack，带有合理的默认配置。
·可通过项目内的配置文件进行配置。
·可通过插件进行扩展。
4.集成官方插件。
5.有图形化创建和管理Vue.js项目的用户界面。

如何安装？
如果电脑已经安装了旧版本CLI（1.x或2.x）的话，使用命令
```
npm uninstall vue-cli -g
```
或者
```
yarn global remove vue-cli
```
卸载。

Vue CLI需要Node.js 8.9 或更高的版本。

使用如下命令安装CLI
```
npm install -g @vue/cli
```
或
```
yarn global add @vue/cli
```

如果想对单个vue文件进行快速原型开发的话，安装一个额外的全局扩展
```
npm install -g @vue/cli-service-global
```

用这个命令查看安装的版本
```
vue --version
```

如果想进行快速原型开发的话，只需要一个vue文件，使用CLI在该文件的目录下执行
```
vue serve
```
这样可以在零配置的情况下为该文件开启一个服务器。


如何创建一个项目？
使用如下代码创建一个项目。
```
vue create hello-world
```

之后，你会被提示选取一个preset（预设），会出现两个选项。
1.default（babel，eslint）
2.manually select feature
第一项的意思是可以选择默认的Babel（一个JavaScript编译器）和eslint（可组装的JavaScript和JSX检查工具）
第二项的意思是手动来选择特性。

选择默认适合快速的创建一个新项目，而手动选择更适合面向生产的项目。

手动选择的选择包括以下几类：
1.Babel：JS编译器，可以将ES6代码转变为ES5代码，从而在现有环境运行。
2.TypeScript：TypeScript，简称TS，意思是JavaScript的超集，可以编译为纯JavaScript。
3.Progressive Web App （PWA） Support：渐进式Web应用程序。
4.Router：vue路由。
5.Vuex：vue的状态管理模式。
6.CSS Pre-processors：Css的预处理器。
7.Linter / Formatter：代码风格检查和格式化。
8.Unit Testing：单元测试。
9.E2E Testing：E2E测试。

这里我们简单的只选择Babel，回车确定。
这是系统提示
Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? (Use arrow keys)
意思是我们要把Babel，PostCSS和ESLint的配置文件放在哪，有两个选项。
1.In dedicated config files  
2.In package.json  
第一个意思是每个配置文件都是专用的单独存放，第二个意思是将配置文件存放在package.json中。

选择对应的选项后系统提示
 Save this as a preset for future projects? (y/N)
意思是是否将此保存为项目的预设。选择之后CLI开始运行，一个项目就创建好了。

使用cd命令进入该项目的文件夹，使用
```
npm run serve
```

开启服务，我们就可以在浏览器访问该项目。

项目中各种文件夹的作用：
build：配置文件
config：核心配置文件
node_modules：模块
router：路由
componentS：组件
assets：静态资源
static：全局静态文件