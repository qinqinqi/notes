# 一、jquery无new构建实例

jq的核心就是从HTML文档中匹配元素并对其进行操作

## 1.实例化jquery对象

```javascript

//无new构造
$(".test").text("这是一段测试文本！");

使用new构建
var test = new $(".test");
test.text("这是一段测试文本！");
```



jquery实现无new构建的方式

```javascript
(function(window, undefi![5c2104a8ad7db039e85472f81a698fd](C:\Users\Administrator\Desktop\notes\随记\jQuery\源码解析\images\5c2104a8ad7db039e85472f81a698fd.png)ed) {
  var
  // ...
  jQuery = function(selector, context) {
    // The jQuery object is actually just the init constructor 'enhanced'
    return new jQuery.fn.init(selector, context, rootjQuery);
  },
  
  jQuery.fn = jQuery.prototype = {
    init: function(selector, context, rootjQuery) {
      // ...
    }
  }
  jQuery.fn.init.prototype = jQuery.fn;
})(window);
```



## 2.无new构建实例详解

### 1）函数表达式和函数声明

​	在ECMAScript中，创建函数最常用的两个方法就是函数表达式和函数声明。在ECMA规范中只明确了一点：函数声明必须带有标识符（函数名称），而函数表达式可以省略。

```javascript
//定义了一个匿名自执行函数
(function(window, undefined) {
  /...
})(window)
```

可以将上边的代码结构分为两部分：(function(window, undefined){}) 和 (window)。第一部分是表达式，而这个表达式本身是一个匿名函数，所以在这个匿名函数后边加(window)就表示执行这个匿名函数并传入参数window。



### 2）原型

​	在js中，原型也是一个对象，通过原型可以实现对象的属性继承，js的对象中都包含一个“[[Prototype]]”内部属性，这个属性对应的即是该对象的原型。

**比较“prototype”和"_proto_"**

* 对于所有的对象，都有“\_proto_”属性，这个属性对应该对象的原型。
* 对于函数对象，除了“\_proto_”属性，还有prototype属性，当一个函数被用作构造函数来创建实例时，该函数的prototype属性值将被作为原型赋值给所有对象实例（也就是设置实例的“\_proto_”属性）

```javascript
function Person(name, age){
  this.name = name;
  this.age = age;
}
Person.prototype.getInfo = function(){
  console.log(this.name + " is " + this.age + " years old");
};
//调用
var will = new Person("Will", 28);
will.getInfo();//"Will is 28 years old"
```



### 3）闭包

闭包就是内部函数被其外部函数之外的变量引用。

jquery.fn的init函数就被jQuery的构造函数调用了，这里就形成了一个闭包。

```
jQuery = function(selector, context){
  return new jQuery.fn.init(selector, context, rootjQuery);
}
```



### 4.总结

* 使用$("XXX")这种实例化方式，其内部调用的是return new jQuery.fn.init(selector, contaxt, rootjQuery)，也就是构造实例交给了jQuery.fn.init()方法来完成。
* 将jQuery.fn.init的prototype属性设置成jQuery.fn，那么使用new jQuery.fn.init()生成的原型对象就是jQuery.fn，所以挂载到jQuery.fn上面的函数就相当于挂载到jQuery.fn.init()生成的jQuery对象上，所有使用new jQuery.fn.init()生成的对象也能够访问到jQuery.fn上的所有原型方法。
* 实例化方法存在的一个关系链是：
  * jQuery.fn.init.prototypr = jQuery.fn = jQuery.prototype;
  * new jQuery.fn.init()相当于new jQuery();
  * jQuery()返回的是new jQuery.fn.init()，而var obj = new jQuery()



# 二、共享原型对象

jQuery.fn.init.prototype = jQuery.fn;



![5c2104a8ad7db039e85472f81a698fd](C:\Users\Administrator\Desktop\notes\随记\jQuery\源码解析\images\5c2104a8ad7db039e85472f81a698fd.png)



# 三、extend功能函数



使用分为两种，一种是在外部使用，一种是在源码内部使用。不管哪种方式，传过去的第一个对象必须是一个object。



**1.外部使用：**

```javascript
<script>

	//任意对象扩展 参数必须是两个及以上
	var obj = $.extend({},{name:"xiaoming"});
	
	//jquery本身扩展
	$.extend({
      work: function(){}
	});
	
	//实例对象扩展
	$.fn.extand({
      sex:"男"
	});
	$().sex;
</script>
```



**2.内部使用**



# 四、扩展知识

* 对象   百度搜索“js string”
  * 内置对象   JavaScript语言提供的  
  * 宿主对象   宿主环境提供
  * 自定义对象   new + 构造函数()创造的



* 浅拷贝和深拷贝
  - 核心：引用类型和非引用类型的拷贝结构是不同的
  - 区别：
    - 浅拷贝只是拷贝基本类型的数据，如果父对象的属性等于数组或另一个对象，那么实际上，子对象获得的只是一个内存地址，因此存在父对象被篡改的可能，浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一款内存。
    - 深拷贝就是能够实现真正意义上的数组和对象的拷贝。递归调用“浅拷贝”。（深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共存内存，修改新对象不会改到原对象）