# 一、el和data的使用

el：声明vue实例对象操作的元素

data：是函数，要返回一个对象



# 二、methods方法

①、方法中的this自动绑定到Vue实例中；

②、不应该使用箭头函数来定义method函数

③、写法

```
greet: function(){
  return ...;
},

greet(形参){
  return ...;
}
```

④、任何事件都会触发所有的回调，包括刷新



# 三、指令

v开头的就是指令

## v-bind属性绑定

缩写： :



## v-on:事件绑定

缩写：@

### 修饰符：

* .stop      阻止事件冒泡
* .prevent   阻止默认事件
* .once    只触发一次回调（事件）
* .self   只有绑定元素触发时才触发回调
* .enter或.13     键盘按下回车触发回调
* .alt.enter    键盘按下alt+回车触发回调

### 键盘事件

* keyup
* keydown



### v-model:双向数据绑定

 只能在input、select、textarea、components上实现，使用ref也可以实现数据的双向绑定

* .lazy   懒
* .number  
* .trim

## ref的使用

通过ref可以获得元素的值





# watch的使用

持续监听属性的状态，一般不建议使用，比较耗费性能



# computed的使用

数据常常发生变化可以使用computed



# 动态绑定css

1、属性绑定

2、计算属性绑定



# v-if和v-show

v-if：根据表达式的值的真假条件渲染元素，在切换时元素及它的数据绑定/组件被销毁并重建

v-show：根据表达式的真假值，切换元素的display属性

# v-for



# fetch和axios

一般常用axios



# 搭建项目

* npm i vue-cli -g
* vue create 项目名



# 项目目录



# 组件嵌套

**①、注册全局组件**

​	在main.js中引入、注册，任何地方都可以使用

**②、注册局部组件**

​	在组件中引入、注册，仅当前组件可用



# 多组件嵌套



# 组件传值

属性传值

传值-----只影响自身的值

传引用（对象   数组）



子传父   $emit

父传子  prop

子传子



生命周期钩子函数