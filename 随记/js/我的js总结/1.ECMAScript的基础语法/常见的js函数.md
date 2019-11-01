

# 一、常见的JS函数



## 1.递归函数

### *条件

1）在函数的内部自己调用自己

		function fu1(){
			alert(2);
			fu1();
		}
		fu1();
​	2）在函数的内部自己调用自己	有设置不再继续递归的出口

		function fn(n){
			if(n==1){
				return 1;
			}
			else{
				return n*fn(n-1);
			}
		}
		fn(5);
		fn(1);
		console.log(fn(5));
		console.log(fn(1));
### *特点

参数一定是发生改变的

## 2.回调函数

把一个函数作为另一个函数的参数使用，这个函数就被称为回调函数

## 3.闭包***

原因

		function fu3(){
			console.log(num);
			var num=10;
			num++;
			console.log(num);
		}
		fu3();//函数执行之后变量数据就被销毁
		fu3();//从新执行
为了函数执行之后变量数据不被销毁	有了闭包，即在函数运行结束之后不被销毁掉的一种手段

实现方式：在函数的内部定义另外一个函数并将它返回，因此在这个函数中可以访问函数内部定义的变量

		function fu3(){
			var num=10;
			function inner(){
				num++;
				console.log(num);
			}
			return inner;
		}
		var val=fu3();
		val();
		val();
		val();
## 4.内置顶层函数

在js内部定义好的拥有全局作用域的一些函数

### *eval()	

对参数引号内部的代码按照js的语法进行解析

### *Number()

将其他的数据类型转换为数值类型	只识别纯数字、16进制数、空字符串

		console.log(Number("123"));//123
		console.log(Number("a"));//NAN
		console.log(Number("123a"));//NAN
		console.log(Number(""));//0
		console.log(Number("-123"));//-123
		console.log(Number("0x11"));//16进制数识别
		console.log(Number("000111000"));//111000
		console.log(Number("123.000"));//123
		console.log(Number(true));//1
		console.log(Number(false));//0
		console.log(Number(undefined));//NAN
		console.log(Number(null));//0
### *parseInt()

将字符串类型转换成数值类型(整数)

* 从左往右依次识别，如果是数字显示数字直到出现非数字停止（16进制数也可转换），如果是非数字直接显示“NAN”，忽略小数点以后的数

   console.log(parseInt("123"));//123
   	console.log(parseInt("a"));//NAN
   	console.log(parseInt("123a"));//123
   	console.log(parseInt("vfdv123"));//NAN
   	console.log(parseInt(""));//NAN
   	console.log(parseInt("-123"));//-123
   	console.log(parseInt("0x11"));//17
   	console.log(parseInt("000123000"));//123000
   	console.log(parseInt("123.45"));//123
   	console.log(parseInt(true));//NAN
   	console.log(parseInt(false));//NAN
   	console.log(parseInt(undefined));//NAN
   	console.log(parseInt(null));//NAN
   * 第二个参数进制转换

  parseInt("数字"，几进制)

### *parseFloat()

将字符串类型转换成数值类型（整数或小数）

### *string()

转换成字符串类型	对象换转换成object

### *boolean()

将其他数据类型转换成布尔值

### *isNAN()

判断当前的值进行Number转换之后是不是NAN

## 5.数据类型转换

### *强制数据类型转换

Number()	parseInt()	parseFloat()	Striing()	Boolean()

### *隐式的数据类型转换

* “5”-“3”						在-两边	如果不是数值	自动调用Number()函数进行计算
  * “hellow"+123		        在+两边	如果一个是字符串 另一个不是	对于不是字符串类型的	自动调用String()
    * 10>"5"                                        在〉两边如果一边是数值另一边不是	对于不是数值的类型	自动调用Number()函数进行转换
  * 表达式1？表达式2：表达式3表达式1如果不是布尔值会自动调用Boolean()转换成布尔值
  * if(表达式){}                                表达式1如果不是布尔值会自动调用Boolean()转换成布尔值

## 6.箭头函数

*语法

一般用于回调函数

*

> 1.箭头函数没有arguments对象
>
> 2.箭头函数不会影响当前this 的指向

箭头函数不会影响当前this 的指向