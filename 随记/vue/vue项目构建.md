# 1.vue-cli是什么

vue-cli 是vue.[js](http://lib.csdn.net/base/javascript)的脚手架，用于自动生成vue.js+webpack的项目模板，分为vue init webpack-simple 项目名 和vue init webpack 项目名 两种。

# 2.vue的作用

可以直接生成一个vue项目的架构

# 3.搭建vue-cli

## ①安装Node.js

​	在安装vue的环境之前，安装NodeJS环境是必须的。可以使用node -v指令检查，需要保证安装了4.0版本以上的nodeJS环境。傻瓜式安装，直接下一步下一步

## ②安装vue-cli

​	使用指令:npm install -g vue-cli

## ③初始化项目

​	使用指令vue init webpack news(项目名称)

*  `注意`	
  * Project name :项目名称 ，如果不需要更改直接回车就可以了。注意：这里不能使用大写。
  * Project description:项目描述，默认为A Vue.js project,直接回车，不用编写。
  * Author：作者，如果你有配置git，他会读取.ssh文件中的user。
  * Install vue-router? 是否安装vue的路由插件，Y代表安装，N无需安装，下面的命令也是一样的。
  * Use ESLint to lint your code? 是否用ESLint来限制你的代码错误和风格,**填上N**
  * setup unit tests with Karma + Mocha? 是否需要安装单元测试工具Karma+Mocha。
  * Setup e2e tests with Nightwatch?是否安装e2e来进行用户行为模拟测试。
  * Should we run npm install for you after the project has been created?(recommended)npm询问你使用npm安装还是yarn安装包依赖，我这里选择

  ​                 是npm，yarn更快更好，使用yarn之前确保你的电脑已经安装yarn

## ④安装依赖npm包

​	首先进入文件夹：cd news，然后执行指令：npm install

## ⑤运行vue环境

​	指令：npm run dev

​	打开网址：https://localhost:8080

# 4.vue-cli的项目结构

## ①build文件夹

​	此目录包含开发服务器和生产webpack构建的实际配置。通常，不需要更改这些文件，除非要自定义Webpack加载器，在这种情况下，应该看

​	build/webpack.base.conf.js。

## ②config/index.js

​	它是主要的配置文件，暴露了构建设置的一些最常见的配置选项（查看config/index.js:配置的详细理解的文档）。需要修改的地方：开发期间的API代理，

​	要配置代理规则，编辑`dev.proxyTable`

## ③src文件夹

​	这是大部分应用程序代码所在的位置，里边有JS文件，有css文件，有vue文件，后期主要操作这个目录。

* assets-----------------------资源目录，专门用于存放图片、css、定义js
* components--------------专门用于存放vue组件
* router------------------------vue的路由文件存放在这里
* App.vue---------------------与main.js同时存在，是第一个入口组件，相当于所有组件的根组件，相当于以前基础页面里边的`<div id="app"></div>`
* main.js----------------------最重要的文件夹，项目的起始文件，也是webpack的入口文件，整个程序从这个地方开始

## ④static文件夹

​	不想使用Webpack进行处理的静态资产的一个逃生舱口。它们将直接复制到生成webpack建立的资产的同一个目录中。只适合放一些自定义js文件。

## ⑤test/unit

​	包含单元测试相关文件。

## ⑥test/e2e

​	包含e2e测试相关文件。

## ⑦index.html

​	这是我们的单页面应用程序的模板 `index.html`。在开发和构建期间，Webpack将生成资产，并将生成的资产的URL自动注入到此模板中以呈现最终

​	的HTML。

## ⑧package.json

​	包含所有构建依赖项和构建命令的NPM软件包元文件，也可以在这里查看使用npm安装的插件。



# 5.一些代码描述

## ①、webpack.base.conf.js

路径：build

```javascript

module.exports = {
  ....
  
  resolve: {
  	//设置拓展名，如果配置了这个，name在import导入的时候，就不用再写后缀名了
  	//使用scss的时候，还可以加上.css 和 .scss
    extensions: ['.js','.vue','.json'],
    
    //别名配置
    alias: {
    	//需要完整的含编译器的vue版本时才写vue$,但是我们实际引用vue的时候都是 import Vue from 'vue' 并没有走这个别名
      'vue$': 'vue/dist/vue.esm.js',
      //这里的@ 指的是路径 ../src ，在webpack.base.conf.js里就被封装了![5e2de4a9d520a5afdf5dae0ec3174d6](C:\Users\Administrator\Desktop\notes\随记\vue\images\5e2de4a9d520a5afdf5dae0ec3174d6.png)
      '@': resolve('src'),
    }
  }
  ...
}

```

![5e2de4a9d520a5afdf5dae0ec3174d6](C:\Users\Administrator\Desktop\notes\随记\vue\images\5e2de4a9d520a5afdf5dae0ec3174d6.png)



## ②、main.js

路径： src

```javascript
//main.js
import Vue from 'vue'
import App from './App'
import router from './router'
/**
*其实就是：import router from './router/index.js'
*在使用webpack项目中，如果导入的是index.js，则可以省略
*这里是相当于导入了一个路由
*/

//在生产环境里把注释全部去掉
Vue.config.productionTip = false

//是否启动代码质量检查，不要删除
/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```







vue-cli最全的解析：https://blog.csdn.net/xiaoyangerbani/article/details/80735310