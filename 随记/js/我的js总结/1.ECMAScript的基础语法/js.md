网页的三层结构：

结构层	HTML	超文本标记语言

表现层	CSS

行为层	JavaScript   脚本语言

# 一、JavaScript的背景知识

## 1.JavaScript是什么

 *一门语言

*一门计算机语言

*一门计算机脚本语言（在其他环境中运行)

*一门可以运行在浏览器V8引擎中的脚本语言



## 2.用来做什么

*完成一些表单的验证

*制作一些网页效果（轮播图、选项卡等）

*对于网页的内容进行读写

*进行数据的操作(获取、传递)

*开发网页游戏

*开发网页应用

*进行后台开发（Node.js）

#### js的作用：

制作页面效果      处理数据

## 3.JavaScript的发展历史

*1995年	网景公司	布兰登艾奇 将liveScript变成JavaScript

*1995年	IE	Jscript

*1996年	网景公司等开发者将JavaScript提交到ECMA（指定计算机行业的标准）

*1997年	ECMAScript1.0

*1998年	ECMAScript2.0

*1999年	ECMAScript3.0

*2005年	ECMAScript4.0（未正式发布）微小改动ECMAScript3.1

*2010年	ECMAScript5.0	

*2015年	ECMAScript6.0	2015

*......	ECMAScript	2017

## 4.JavaScript的组成

*ECMAScript	核心语法（变量、数据类型、流程控制、函数、数组、对象）

*BOM	Browser	Model	浏览器对象模型（如何用JS控制浏览器）

*DOM	Document	Obbject	 Model	文档对象模型（如何用JS控制文档）

## 5.JavaScript的语法特点

*基于对象和事件驱动的解释型松散型语言

## 6.Javascript的引用方式 

### *a链接或者重定向的位置进行调用

	<a href="javascript:alert(1)">链接</a>
	<form action="javascript:alert(2)">
		<input type="submit">
	</form>
### *在事件的后面进行调用

	<div onclick="alert(3)"></div>
### *嵌入方式	执行一次

	<script>
		alert(4);
	</script>
### *引入方式

	<script src="js1.js"></script>
* 注意

  ​	用于引入的script标签不能再插入其他内容

  ​	采用不同的方式引入的js代码最终还是在一起执行的	所以互相之间还是有联系的



## 7.JavaScript的变量

### *存储数据的容器

### *变量的赋值

​	声明的同时进行赋值	var 变量名=值;

	<script>
		var a=1;
		alert(a);
	</script>
​	先声明再赋值		var 变量名； 变量名=值；

	<script>
		var a;
		a=1;
		alert(a);
	</script>
​	一次性声明多个变量，然后赋值	var	变量名1，变量名2，变量名3；	变量名1=值；

```
<script>
    var name,age,sex;
    name="张三";
    alert(name);
</script>
```

​	一次性声明多个变量的同时进行赋值	var	变量名1=值，var	变量名2=值，var	变量名3=值，......;

```
<script>
    var name="zhangsan",age=17,sex="男";
    // alert(name);
    // alert(age);
    // alert(sex);
    alert(name+age+sex);
</script>
```

### *声明变量	var（关键字）

​	var+空格+变量名

​	*ES6	新增的变量声明方式：let(关键字)	

	<script>
		let b=2;
		alert(b);
	</script>
​	*ES6	新增的常量的声明方式:const	const 常量名=值；

	<script>
		const c=3;
		alert(c);
	</script>
### *声明变量产生的覆盖问题

变量值可以重新赋值，常量不可以

var可以重新声明	let和const不可以

不使用任何关键字声明	直接给变量赋值不会报错

### *变量命名的规范

1.变量命名严格区分大小写

2.开始必须是字母、下划线、$,	

   后续可以是字母、数字、下划线 、$

3.不能使用关键字和保留字作为变量名

4.JavaScript的命名习惯	长单词使用驼峰命名法（第一个单词首字母小写，后续首字母大写）	getNameBylist	Date()	Object()

5.变量的命名必须有实际意义

## 8.JavaScript的数据类型

*数值	

> Number			10		100000000	10.001		-10		1e+2（科学计数法）	十六进制0x 	八进制0o/0	二进制0b

*字符串类型		

> String 	" " 	' '	ES6	新增的``反隐号（模板字符串）		引号嵌套（单引号和双引号只能互相嵌套）

*布尔值

> Boolean	 	true和false

*undefined

> 只有一个值	undefined，是一个特殊的值	在某些情况下		变量没有被赋值但被声明了
>
> 形参没有对应的实参
>
> 函数没有返回值
>
> 访问一个没有定义的下标

*空值

> null		占位符	一般用于解除对象的引用

*Symbol(ES6新增)	var sy1=Symbol();

*对象

> Object	函数	数组

## 9.数据类型的划分

*初始类型	数值	字符串	布尔值	undefined	null		Symbol

*引用类型	对象

​	*代码在运行的时候数据都是保存在计算机内存中

​	*内存当中是分为	堆栈	堆区

​	堆栈、堆区的区别

​		第一，栈区保存长度固定的值	所占空间比较少	读取速度快

​			堆区保存的是长度可变的值	所占空间比较大	访问速度相对慢一些

​		第二，js在运行的时候	初始类型都是在栈区内保存的

​			 引用类型都是在堆区中保存的	只在栈区中保存一个引用地址

## 10.判断数据类型（typeof）

```
<script>
	var num=10;//number
	var str="122";//string
	var boo=true;//boolean
	var foo;//undefine
	var bar=null;//object
	var obj={};
	alert(typeof obj);
</script>
```
## 11.JavaScript运算符

### *算数运算符

 +，	-	，*，	/，	++，	--,	%

> 	<script>
> 		var num1=10
> 		var num2=20
> 		console.log(num1+num2)
> 		console.log(num1-num2)
> 		console.log(num1*num2)
> 		console.log(num1/num2)
> 		console.log(5+5)
> 		console.log(10%3)
> 		num1++;
> 		console.log(num1)
> 		++num1;
> 		console.log(num1)
> 		var result=num1++;
> 		console.log(result)
> 		var result=++num1;
> 		console.log(result)
> 	</script>

> +还可以用来连接字符串	只要+左右的值只要有一个是字符串 	最终结果就是拼接之后的字符串
>
> 	<script>
> 		var str1="vfv"
> 		var str2="mi"
> 		var str3=str1+str2
> 		console.log(str3)
> 	</script>

> 如果字符串中全部都是数值也可以除了+之外的算数运算
>
> 	<script>
> 		var str4="2"
> 		var str5="5"
> 		console.log(str4*str5)
> 	</script>

> 在算数运算中如果得不到最终的结果，会得到一个NaN（Not a Number）
>
> 	<script>
> 		console.log("aaa"-5)
> 	</script>

### *关系运算符（比较运算符）

<	>	>=	<=	==	===		!=	!==		运算结果是布尔值

> 	<script>
> 		var num1=5
> 		var num2=10
> 		var result=num1<num2
> 		console.log(result)
> 	</script>

> 其他类型的比较
>
> *字符串和字符串比较	是从第一位开始	依次比较字母所对应的ASSII码值得大小
>
> 		// var foo=5
> 		// var bar="10"
> 		// console.log(foo<bar)
> 		// console.log(foo>bar)
> 		// var foo=10
> 		// var bar="10"
> 		// console.log(foo==bar)
> 		// console.log(foo===bar)
> 		var str1="adc"
> 		var str2="abc"
> 		console.log(str1>str2)
> 	</script>
> *数值和由数值组成的字符串是可以比较的
>
> ​	==只比较数值大小是否相等
>
> ​	===不仅要比较数值大小是否相等，还要比较数据类型是否相同	
>
> 	<script>
> 		var foo=10
> 		var bar="10"
> 		console.log(foo==bar)
> 		console.log(foo===bar)
> 	</script>

### *赋值运算符

> =	+=	-=	*=	/=	%=
>
> 	<script>
> 		var num1=10
> 		// num1=num1+5
> 		num1+=5
> 		console.log(num1)
> 	</script>

### *逻辑运算符

与运算&&	或运算||	非运算！

> *对于布尔值进行运算
>
> 1.与运算	同真为真
>
> 2.或运算	有真为真
>
> 3.非运算	假值变为真值	真值变成假值
>
> 	<script>
> 		var boo1=true
> 		var boo2=false
> 		console.log(boo1&&boo2)
> 		console.log(boo1||boo2)
> 		console.log(!boo1)
> 		console.log(!boo2)
> 	</script>

>  *对于其他类型的值进行运算		 假值（0 NAV “ ” undefined false null）	真值（1 true）

* 与运算

  |  值1  |  值2  |  结果  |
  | :--: | :--: | :--: |
  |  真   |  真   |  真2  |
  |  真   |  假   |  假   |
  |  假   |  假   |  假2  |

* 或运算

  |  值1  |  值2  |  结果  |
  | :--: | :--: | :--: |
  |  真   |  真   |  真1  |
  |  真   |  假   |  真   |
  |  假   |  假   |  假2  |

### *一元运算符

typeof	+（正号）	-（负号）	new		delete

	<script>
		var foo=1
		console.log(typeof foo)
		console.log(-foo)
		console.log(-(-foo))
	</script>
### *三元运算符（三元表达式）

表达式？当表达式为真的时候的值：当表达式为假的时候的值（表达式1？表达式2：表达式3）

* ？前边的关系运算表达式可以替换为任意的一个表达式

* 表达式：本身就是一个值或者可以用来求值的代码

   <script>
   		var grade=65
   		var result=grade>=60?"及格":"不及格"
   		console.log(result)
   	</script>



### *扩展运算符

...

```
let arr=[1,2,3,4,5];
 console.log(...arr); // 结果是1 2 3 4 5
 console.log(Math.max(...arr));//最大值
 console.log([0,1,2,3,...arr]);//拼接数组
 // 剩余运算符  ...
 let [a,b,...c]=arr;//结果是 1 2 [3,4,5]
```

### *特殊运算符

()（提升算术优先级、调用函数）	



## 12.解构赋值

### *es6新增

*可以是数组，可以是对象，可以是函数



数组

```
// 结果是1 2 3
let arr=[1,2,3];
let [a,b,c]=arr;
// 结果是1 2
let arr=[1,2,3];
let [a,b,]=arr;
// 结果是1 2 undefined
let arr=[1,2];
let [a,b,c]=arr;
//交换变量值
var a=1;
var b=2;
[a,b]=[b,a];
```



对象

```
//取别名
let obj={name:"zhangsan"};
let {name:n}=obj;
console.log(n);

//字符串对象的长度
let str="asdfghjk";
// let length=str.length;
let {length}=str;
console.log(length);
```

函数



## 






