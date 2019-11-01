# 一、gulp网站

中文：[https://www.gulpjs.com.cn/](https://www.gulpjs.com.cn/)

英文：[https://gulpjs.com/](https://gulpjs.com/)



# 二、gulp的特点

任务化、基于流（I/O）、异步多任务（也可以同步）

# 三、常用的API

## *gulp.src()

读取目标源文件的路径，将数据存到gulp内存中

## *gulp.dest()

输出文件

## *gulp.task()

注册任务

## *gulp.watch()

监视文件

# 四、常用的插件

*gulp-concat：合并文件（js/css）

*gulp-uglify：压缩js文件

*gulp-rename：文件重命名

*gulp-less：编译less

*gulp-clean-css：压缩css

*gulp-htmlmin：压缩html

*gulp-fez-tinypic：压缩图片（不能压缩gif，jpg会失真，必须拥有一个TinyAPIKey）

*gulp-livereload：实时自动编译刷新（半自动）

*gulp-connect：热加载（全自动）

*open：自动打开指定的链接
*gulp-load-plugins：实现插件懒加载(不需要将所有的插件一一require进来)

# 五、安装gulp
必须全局安装过gulp才能局部安装

*全局安装

```
npm install gulp -g
```

*局部安装

```
npm install gulp --save-dev
```

*指定版本

```
npm i -g gulp@3.9.1
npm install --save-dev gulp@3.9.1
```



# 六、创建一个简单的gulp项目

```
|-dist

	|-src

		|-js

		|-css

		|-less

|-index.html

|-gulpfile.js----gulp配置文件

|-package.json

	{

		"name":"文件名",

		"version":"1.0.0"

	}
```



# 七、gulpfile.js配置

## *压缩js文件

```
// 引入压缩js所用到的插件
var concat=require('gulp-concat');
var uglify=require('gulp-uglify');
var rename=require('gulp-rename');
gulp.task('js',function(){
    return gulp.src('src/js/*.js')   //找到数据源文件，将数据读取到gulp的内存中，如果js文件夹的兄弟文件夹也有js文件，则路径用src/**/*.js */
            .pipe(concat('build.js')) //临时合并文件
            .pipe(gulp.dest('dist/js'))  //临时输出文件到本地
            .pipe(uglify())              //压缩文件
            .pipe(rename({suffix:".min"}))  //重命名
            .pipe(gulp.dest('dist/js'))   //压缩后再输出到本地
})
```

## *less转换

```
gulp.task('less',function(){
    return gulp.src('src/less/*.less')
            .pipe(less())
            .pipe(gulp.dest('src/css'))
})
```

## *注册压缩css任务

```
//添加依赖任务，防止less没执行完css任务已经执行完的情况
gulp.task('css',['less'],function(){
    return gulp.src('src/css/*.css')      //读取css文件到gulp内存
            .pipe(concat('index.css'))    //合并css文件
            .pipe(cssClean({compatibility:"ie8"}))             //压缩css文件
            .pipe(rename({suffix:'.min'}))             //重命名
            .pipe(gulp.dest('dist/css/'))  //压缩后再输出到本地
})
```

## *注册压缩html任务

`一般清除空格就好了`

```
gulp.task('html',function(){
    var options = {
        collapseWhitespace:true,//清除空格
        // collapseBooleanAttributes:true,//省略布尔属性的值
        // removeComments:true,//清除注释
        // removeEmptyAttributes:true,//清除空属性
        // removeScriptTypeAttributes:true,//清除所有script标签中的type="text/javascript"属性
        // removeStyleLinkTypeAttributes:true,//清除link的type属性
        // minifyJS:true,//压缩html中的js代码
        // minifyCSS:true //压缩html中的css代码  
    };
    return gulp.src('index.html')
            .pipe(htmlMIn(options))
            .pipe(gulp.dest('dist'))
})
```

##*压缩png图片
```
var tinify = require('gulp-fez-tinypic');
 
gulp.task('tinypic', function() {
    gulp.src('images/*.png')
        .pipe(tinify('NTAyBf36QFEq2SnvtOIBL0hloVuo1EPr'))   //必须拥有一个TinyAPIKey
        .pipe(gulp.dest('dist/images'));
});
```

## *实时刷新

`注意`每个任务都需要铺相应的管道，.pipe(livereload()) 和 .pipe(connect.reload())

半自动

```
gulp.task('watch',['default'],function(){
    //开启监听
    livereload.listen();
    //确认监听的目标以及绑定的相应的任务
    gulp.watch('src/js/*.js',['js']);
    gulp.watch(['src/less/*.less','src/css/*.css'],['css']);
})
```

全自动

```
gulp.task('server',['default'],function(){
    connect.server({
        root: 'dist/',
        livereload: true,//实时刷新
        port: 8000
    });
    open('http://localhost:8000/');
    //确认监听的目标以及绑定的相应的任务
    gulp.watch('src/js/*.js',['js']);
    gulp.watch(['src/less/*.less','src/css/*.css'],['css']);
})

```

##*插件懒加载
```
var $=require('gulp-load-plugins')();
gulp.task('html',function(){
	return gulp.src('index.html')
			.pipe($.htmlmin({collapseWhitespace:true}))
			.pipe($.dest('dist'))
});
//使用gulp-load-plugins时，gulp-htmlmin使用$.htmlmin(),gulp-clean-css使用$.CleanCss,单词顺序也不能更换
```



## *注册默认任务

```
gulp.task('default',['任务名1','任务名2','任务名3']);
```







