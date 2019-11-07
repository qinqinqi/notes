# 一、callbacks

* `概念：`  通过事件函数了解Callbacks
  * 事件通常与函数配合使用，这样可以通过发生的事件来驱动函数的执行。
  * 原则：一个事件对应一个事件函数，在一个事件对应对各事件函数的情况下，后者会覆盖前者。通过添加数组的方法，实现一对多。
  * Callbacks则是把这些处理成一个可控的容器。


* `作用：`  $.callbacks用于管理函数队列
* `使用：`  通过add添加处理函数到队列当中，通过使用fire去执行这些处理函数。
* `提示：` $.callbacks是在jQuery内部使用，如为.ajax，\$.Deferred等组件提供基础功能的函数。它也可以用在类似功能的一些组件中，如自己开发的插件。



# 二、API实例

````javascript

//调用$.Callbacks，获取到一个Callbacks实例
var cb = $.Callbacks();

//add向内部队列添加函数
cb.add(function () {
  console.log("add one")
});

//fire依次执行队列中的函数
cb.fire();  //会输出add one

````



# 三、Callbacks的字符串参数

$.Callbacks("once unique stopOnFalse memory ");

## 1.once

* 函数队列只执行一次    fire()
* 不添加这个参数函数队列调用多少次就执行多少次，添加了以后只执行一次

```
//不添加once参数                         //添加once参数
var cb = $.Callbacks();                 var cb = $.Callbacks('once');
cb.add(function () {                    cb.add(function () {
  console.log("add one");                   console.log("add one");
});                                     });
cb.fire();  //输出add one                cb.fire();  //输出一次add one
cb.fire();  //输出add one                cb.fire();  
```



## 2.unique

* 往内部队列添加的函数保持唯一，不能重复添加   add()
* 不添加这个参数内部队列可以添加多个函数，添加了以后不管添加多少个函数只执行第一个函数

```
//不添加unique参数                              //添加unique参数
var cb = $.Callbacks();                        var cb = $.Callbacks('unique');
function ceshi(){                              function ceshi(){
    console.log("这是测试");                      console.log("这是测试");
}                                              }
cb.add(ceshi,ceshi);//这是测试  这是测试        cb.add(ceshi,ceshi);//这是测试 cb.fire();                                     cb.fire();
```



## 3.stopOnFalse

* 内部队列里的函数是依次执行的，当某个函数的返回值是false时，停止继续执行剩下的函数。
* 不添加这个参数，即使函数内部返回false也不会停止执行下一个函数；但是添加了这个参数，函数内部返回false时会停止执行。



## 4.memory

* 当函数队列fire一次过后，内部会记录当前fire的参数。当下次调用add的时候，会把记录的参数传递给新添加的函数并立即执行这个新添加的函数。不需要再次fire。



# 四、源码解析

## 1.对options的处理

* ①无参数默认处理

* ②参数是string形式使用typeof进行判断即可，非此类参数则需要进行处理

  * ```
    typeof options === "string"
    ```

* ③参数是多个的时候，需要对参数进行切割，并依次传入。具体可查看createOptions(options)

````javascript
jQuery.Callback = function (options) {
  option = typeof options === "string" ? (optionsCache[options] || createOptions(options)) : {};
}
````



## 2.optionsCache

缓存对象

## 3.createOption(options)

用来对多个参数进行分割

```javascript
function createOptions(options) {//定义一个处理多个参数的方法
    var object = optionsCache[options] = {};//在缓存内进行记录一次 对象形式
    options.split(/\s+/).forEach(function(value) {//value是切割参数数组的每一项
        object[value] = true;//扩展对应的value属性
    });
    return object;//返回出去 支持多种参数传递并存储在cache缓存中
}
```



## 4.处理完options后定义了了一堆变量和方法

```javascript
var // Last fire value (for non-forgettable lists)
        memory,
        // Flag to know if list was already fired
        fired,
        // Flag to know if list is currently firing
        firing,
        // First callback to fire (used internally by add and fireWith)
        firingStart,
        // End of the loop when firing
        firingLength,
        // Index of currently firing callback (modified by remove if needed)
        firingIndex,
        // Actual callback list
        list = [],
        // Stack of fire calls for repeatable lists
        stack = !options.once && [],
        // Fire callbacks
        fire = function( data ) {
            ..................
        },
        self = {
            add: function() {
                ..............
            },
            remove: function() {
                ................
            },
            has: function( fn ) {
                ..................
            },
            empty: function() {
                ..................
            },
            disable: function() {
                ..................
            },
            disabled: function() {
                ................
            },
            lock: function() {
                ..............
            },
            locked: function() {
                ..............
            },
            fireWith: function( context, args ) {
                ...................
            },
            fire: function() {
                ................
            },
            fired: function() {
                ................
            }
        };
```

最后Callbacks返回了self对象，所以在self上面定义的仅供Callbacks使用。在他的内部方法中有两个比较重要的，一个是list，所有add添加的函数都存储在list上，另一个是fire方法，他实现了触发list中的函数的具体逻辑。

`self方法`

* add：添加函数
* remove：删除函数
* has：检测list中是否有相同的函数
* empty：清空list
* disable：禁止所有操作list = stack = memory = undefined
* disabled：list是否可用
* lock：锁
* locked：锁是否可用
* fireWith：为触发list函数做预处理，最终调用list方法
* fire：调用fireWith方法
* fired：fire方法是否运行过



## 5.练习

```javascript
//once
var cb = $.Callbacks('once');
cb.add(function(){
    alert('a');
});
cb.add(function(){
    alert('b');
});
cb.fire();//弹出a,b
cb.fire();//不执行


//memory
var cb = $.Callbacks('memory');
cb.add(function(){
    alert('a');
});
cb.add(function(){
    alert('b');
});
cb.fire();//弹出a,b

cb.add(function(){ //弹出c
    alert('c');
});



//once memory
var cb = $.Callbacks('once memory');
cb.add(function(){
    alert('a');
});
cb.add(function(){
    alert('b');
});
cb.fire();//弹出a,b

cb.add(function(){ //弹出c
    alert('c');
});
cb.fire(); //不执行


//add方法多个参数逗号隔开
var cb = $.Callbacks();
cb.add(function(){
    alert('a');
},function(){
    alert('b');
});

cb.fire(); //弹出a,b


//stopOnFalse
var cb = $.Callbacks('stopOnFalse');
cb.add(function(){
    alert('a');
    return false;
},function(){
    alert('b');
});

cb.fire();//弹出a


//lock()
var cb = $.Callbacks('memory');
cb.add(function(){
    alert('a');
});

cb.fire();//弹出a
cb.lock();//锁住fire()

cb.add(function(){ //弹出b
    alert('b');
});
cb.fire();//不执行


//remove()
var cb = $.Callbacks();
var fn1 = function(){
    alert('a');
};
var fn2 = function(){
    alert('b');
};
cb.add(fn1);
cb.add(fn2);
cb.fire(); //弹出a,b

cb.remove(fn1,fn2);
cb.fire();//不执行
```



# 五、扩展知识

* forEach
* 三元表达式
* 逻辑与  var   result = ex1 && ex2;
* 逻辑或  var   result = ex1 || ex2;
* Array.prototype.slice.call(arguments)            可以将类数组转换成真正的数组
* toString.call(fn) ==="[object Function]"         toString.call()进行数据类型的检索
* options.split(/\s+/).forEach









