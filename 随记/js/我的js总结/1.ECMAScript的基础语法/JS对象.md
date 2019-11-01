# 一、JS对象

是属性的无序集合体

## 1.对象

是object	 	是东西

是任何的客观事物以及抽象的规则、计划、事件等

一切皆对象

## 2.属性

### 1）属性

描述对象当前状态的一些信息（数值、字符串、布尔值）

写法：对象名.属性

### 2）方法

描述对象的行为、动作、功能（函数）

写法：对象名.方法名()

## 3.类

> 具有相同或者相似属性的对象的抽象描述叫做类
>
> 类的具体化或者实例化就是对象	

在JS中通过构造函数来实现类	构造函数：function、Array		实例化函数得到类new function()	new Array()

## 4.语法

* #### 创建一个对象

  1.json方式

  var obj={name1:"value1",name2:"value2"}

  2.先写一个构造函数（类）	再去实例化

  function Human(){};

  var obj=new Human();

  3.直接实例化顶层构造函数	object()

  var obj=new object();

* 对象属性的添加

  可以在任意的时刻进行添加

* 对象属性的访问

  * 对象.属性
  * 对象[变量]
  * 对象.方法()
    * 对象[变量]	();

* 对象属性的遍历

  for(var i in person1){

  ​	console.log(i);

  ​	console.log(person1[i])

  }

* 对象属性的删除

  delete 对象.属性;


# 二、JS对象的分类

## 1.原生对象

在JS定义的语法内部自带的一些对象/构造函数

Array()	String() 	Boolean() 	Function()	Object()	Error()	Date()[从0  开始]	RegExp()		Math(数学对象) 	JSON

得到一个原生对象		new 构造函数()

> Math()对象的语法
>
> * 绝对值:Math.abs(-100)
>
> * 取整：Math.round(4.4)     四舍五入
>
>   ​	   Math.floor(4.999)    向下取整	小的
>
>   ​           Math.ceil(4.0001)    向上取整	大的
>
> * 最大值： Math.max(14,5,6,2,3,5)
>
> * 最小值：Math.min(4,-9,5,8,5)
>
> * 随机数：Math.random()              不需要传递参数   0-1的随机数
>
> * 求平方根：Math.sqrt(2)
>
> * 求开几次方：Math.pow(2,10)或者Math.pow(2**10)【ES6】
>
> * 求正弦值:Math.sin()
>
> * 求余弦值：

## 2.宿主对象

*BOM 浏览器对象模型		Window（全局对象）		history 		 location		 screen	navigagator浏览器

*DOM	文档对象类型		document	element		attribute 	event	

​	*获取这些对象有特定的方式

HTML对象	div、a、p...每一个标签

# 三、DOM

document	object	model文档对象模型

提供了用JS操作页面当中标签、属 性、样式、 内容的能力

## 1.操作页面

#### *document对象

> queySelector()
>
> querySelectorAll()

#### *获取元素对象/标签对象的方法

> document.querySelect()
>
> document.querySelectAll()

	<script>
	var divobj=document.querySelector(".demo");
	divobj.onclick=function(){
		divobj.id="box"
		divobj.style.width="100px";
		divobj.style.height="100px";
		// divobj.style.border-radius="50%";
		divobj.style.background="blue";
	}
	</script>
#### *元素对象的属性

* innerHTML	获取或者设置		标签的内容
* className     获取或者设置        标签的类名
* id                    获取或者设置          标签的id
* style                 获取标签的行内样式集合
  * div.style.width      或者设置某一个行内样式
* classList             获取标签的类名集合对象
  * add()添加某个类名
  * remove()移除某个类名



一个简单的小程序

CSS

	<style>
		.btn{
			width: 150px;
			height:80px;
			font-size:38px;
			background:green;
			position:absolute;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
			margin:auto;
			line-height:80px;
			text-align:center;
			color:#fff;
			border-radius:40px;
			cursor:pointer;
			user-select:none;
		}
	</style>
HTML

	<body>
		<div class="btn">开始</div>
	</body>
JS

	<script>
	var divobj=document.querySelector(".btn");
	n=0;
	divobj.onclick=function(){
		n++;
		if(n%2==0){
			divobj.style.background="green";
			divobj.style.color="#fff";
			divobj.innerHTML="开始";
		}
		else{
			divobj.style.background="red";
			divobj.style.color="#000";
			divobj.innerHTML="暂停";
		}
	}
	</script>

#### *元素对象的事件

* onclick鼠标单击事件
* onmouseenter鼠标进入事件
* onmouseleave鼠标离开事件


* transitionend过渡结束事件

#### *元素对象的方法

* addEventListener(事件类型，事件处理程序（程序）)
* querySelector()
* querySelectorAll()



# 四、继承&原型

## 1.继承

在一个类中通过某种方式获得另一个类中所有的属性和方法	这种方式叫做继承

存在继承关系的类 当我们访问某个类实例化对象的属性的时候，会先从当前对象身上找， 如果找不到就会找类，如果当前类没有就会去找当前类的父类

## 2.原型

将某个对象的构造函数（子类）的prototype属性设置为另一个构造函数（父类）实例化的对象，这个对象就称作某个对象的原型。这 也是实现继承的一种方式

## 3.-_proto__

每一个对象自带的一个访问器属性，这个属性对象身上本身是没有的，是浏览器实现的一个功能  通过__proto___可以访问当前对象的原型

		function Person(){
			this.head=1;
			this.legs=2;
			this.arms=2;
		}
		var person=new Person();
		console.log(person);
	
		function Student(id,className){
			this.studentId=id;
			this.className=className;
		}
	
		function Teacher(id,position){
			this.teacherId=id;
			this.position=position;
		}
	
		//Student Teacher的原型
		Student.prototype=person;
		Teacher.prototype=person;
	
		var stu=new Student(1,"WUIW1711");
		console.log(stu);
		var tea=new Teacher(2,"导师");
		console.log(tea);
## 4.Array方法

百度Array  MDN

ES3：	ie6  ie7  ie8都支持

push() 方法将一个或多个元素添加到数组的末尾，并返回新数组的长度。	末尾

pop()方法从数组中**删除**最后一个**元素**，并**返回**该元素的**值**。此方法**更改**数组的**长度**。	末尾

**unshift()** 方法将一个或多个元素添加到数组的开头，并返回新数组的长度。	开头

**shift()** 方法从数组中**删除**第一个元素，并返回该元素的值。此方法更改数组的长度。	开头

**splice()**方法通过删除现有元素和/或添加新元素来更改一个数组的内容。	任意位置

`**slice()**` 方法返回一个从开始到结束（**\*不包括结束***）选择的数组的一部分**浅拷贝**到一个新数组对象。原始数组不会被修改。

E56新增的十个方法



# 五、this

在**调用函数**的时候通过call或者apply传递的参数		谁调用就指谁

* 调用当前方法的对象


* 调用事件的时候  this指的是添加事件的对象
  * callapply	传递的参数
* 如果在构造函数中  this指的就是实例化的对象

# 六、ES6  class定义类