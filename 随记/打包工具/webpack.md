淘宝镜像安装

```
npm install cnpm -g --registry=https://r.npm.taobao.org
```

文件目录结构

```
webpack_demo
	bulid   ----存放生产环境下的打包文件
	dist    ----存放开发环境下的打包文件
	src     ----存放源文件
	  index.js  ---入口文件
	package.json
	webpack.config.js  ----webpack配置文件
```

初始化项目

```
cpm init -y
```

安装webpack

```
cnpm i --save-dev webpack webpack-cli     //webpack4以上的版本已经将其脚手架分离出来，所以需要另外安装；不推荐进行全局安装
```



使用npx进行打包

````
npx webpack  //默认打包的是开发环境下的，可在配置文件中加mode: "development"

npx webpack --mode development/production   //指定打包的模式

npx打包的文件不够灵活，可更改配置文件自定义打包
````



npm安装参数

--save (可简写为-S)
--save-dev (可简写为-D)

**1、cnpm i m**

* 将m模块安装到node_modules中
* 不会修改package.json
* 运行cnpm i 命令时不会安装m模块

**2、cnpm i m --save**

* 将m模块安装到node_modules中
* 会在package.json的dependencies属性下添加m模块
* 运行cnpm i命令时自动安装到node_modules中

**3、cnpm i m --save-dev**

- 将m模块安装到node_modules中

- 会在package.json的DevDependencies属性下添加m模块

- 运行cnpm i命令时自动安装到node_module

  ​

  ​

  ​

  ### 使用hash和chunkhash的区别

  只用hash完全能够满足需要，hash是工程级别的，如果项目里但凡有一个文件有改动，打包后的hash码就会更新，所有文件的hash码都会更新，而且都是一样的hash码，所以问题来了，如果我们的项目很大，我们只是修改了一个bug或是一个页面，却需要用户重新更新所有文件，用户体验大大降低了。

  这时候chunkhash出现了，他是文件级别的，一般我们在output的chunkFilename中使用它，在outpput的filename中使用hash，在css分离的时候使用contenthash，当然事无绝对，我们应该见机行事，如果担心写错了，可以全部用hash代替，就是牺牲一些用户体验罢了，牺牲多少呢？项目越大，牺牲越大





