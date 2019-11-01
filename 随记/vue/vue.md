# vue的优点

性能：好

指令与组件划分：更明确

框架设计：简单

渲染能力：使用 Vue 语法开发的组件不仅仅可以运行在浏览器端，还能被用于开发 iOS 和 Android 上的原生应用（三端的通用组件）



# vue的缺点

成熟度、社区活跃度都不是很好

影响力相比于angular和react还差的很远（人才需求相对较少）

不兼容IE8



# vue全家桶

* vue-cli:脚手架，构建工具  一般全局安装
* vue-router：路由
* vue-resource:设置代理，config/index.js下面的proxyTable
* vuex:状态管理




# 什么是npm

npm是Node.js的包管理工具,许多开发者都把自己开发的包发布到npm官网上，这样我们可以直接用npm下载相应的包



# vue.js的环境搭建

vscode打开控制台：ctrl+shift+y,选择终端就可以进入控制台

http://www.cnblogs.com/hi-shepherd/p/6662348.html



# 将vue项目打包发布

* 指令：npm run build
* 将生成的dist文件上传到服务器，访问文件夹中的html文件就可以了
* 可能存在的问题：
  * 所有的`js，css，img`等路径是指向根目录的
  * 修改`config/index.js`里的`assetsPublicPath`的字段，初始项目是`/`是指向项目根目录的也是为什么会出现错误，这时改为`./`指向当前目录



# 本地安装和全局安装的区别

http://www.cnblogs.com/PeunZhang/p/5629329.html

|  区别  |             本地              |                    全局                    |
| :--: | :-------------------------: | :--------------------------------------: |
| 安装方式 |                             |               加-g或-global                |
| 安装位置 | 安装在这个大文件夹下的node_modules文件夹下 | 安装在Node安装目录下的node_modules文件夹中，可通过npm root -g查看全局安装目录 |
| 调用方式 |      通过require()的方式引入       |            在命令行中直接运行该组件包支持的命令            |



# vue.js的引入

1)一般在head标签中引入----------------------------------可以防止抖屏

​	html是由上而下运行的,当vue.js写在页面底部时,你使用vue定义的data数据将在html已经渲染好后才加载,这样就会造成一个页面抖动的效果

2)一般引入在线的vue.js------------------------------------加载速度比本地的要快

​	`<!-- 开发环境版本，包含了有帮助的命令行警告 --><script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>`

​	`<!-- 生产环境版本，优化了尺寸和速度 --><script src="https://cdn.jsdelivr.net/npm/vue"></script>`