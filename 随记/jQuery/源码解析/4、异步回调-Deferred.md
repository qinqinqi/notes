# 一、Promise规范

## 1.Promise作为一个模型，提供了一个在软件工程中描述延时（或将来）概念的解决方案

* Promise表示一个异步操作的最终结果。
* 与Promise最主要的交互方法是，通过将函数传入它的then方法，从而获得Promise最终的值或Promise最终拒绝（reject）的原因。
* 一个Promise必须处于以下状态其中之一：pending，fulfilled或rejected。
* 一个Promise必须提供一个then方法来获取其值或原因。



而Derferred是这种规范的具体实现。![Promise规范](C:\Users\Administrator\Desktop\notes\随记\jQuery\源码解析\images\Promise规范.png)





# 二、Deferred API

## 1.jQuery.Deferred()

一个构造函数，返回一个链式实用对象方法来注册多个回调，回调队列，调用回调队列，并转达任何同步或异步函数的成功或失败状态。



## 2.deferred.done()

当Deferred（延迟）对象解决时，调用添加处理程序。



## 3.deferred.fail()

当Deferred（延迟）对象拒绝时，调用添加处理程序。



## 4.deferred.progress()

当Deferred（延迟）对象生成进度通知时，调用（已）添加的处理程序。



## 5.jQuery.when()

提供一种方法来执行一个或多个对象的回调函数，Deferred（延迟）对象通常表示异步事件。



## 6.   .promise

返回一个Promise对象用来观察当某种类型的所有行动绑定到集合，排队与否还是已经完成。

