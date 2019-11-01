# Js函数

函数就是封装起来可以被重复调用的代码块

## 1.好处

*程序更加简洁

*维护更加方便

*逻辑更加清晰

## 2.函数的声明

###  *使用function关键字

关键字:被js赋予了特殊功能的单词）

同一块中，function声明的函数会被优先解析

> function 函数名(参数){				//参数可有可无	函数名的命名规则和变量名是一样的，函数名不能和变量名重复
>
> ​	函数(主)体
>
> }

### *匿名函数

> var	fn=function(){}		//声明变量直接赋值给函数	
>
> setInterval(function(){},1000);
>
> div.onclick=function(){}

### *实例化构造函数

> var fn =new Function(){}

## 3.函数的调用

### *函数名() 	变量名()

### *在事件的后面进行调用

> 		var ele=document.querySelector(".demo");
> 		ele.onclick=function(){
> 			alert(1);
> 		}

### *自调用

自己调用自己

> 	(function(){
> 	   	 alert("函数自调用")
> 		})();　

var	fn=function(){}		//声明变量直接赋值给函数

## 4.函数的参数

>  让函数的调用更加灵活

### *参数	分为实参	和形参

* 实参：在调用函数的时候传递的真正的值
* 形参：在声明函数的时候定义的变量

### *参数的个数

可以是多个  参数之间用,隔开

### *参数的数据类型

任意的数据类型

> 多个表格

	<script>
		function fn(row,lie,color){
			document.write("<table border='1'align='center'>");
			for(var i=0;i<row;i++){
				if(i%2==0){
					document.write(`<tr bgcolor=${color}>`);	//引入颜色
				}
				
				for(var j=0;j<lie;j++){
					document.write(`<td>第${i+1}行 第${j+1}列</td>`);
				}
				document.write("</tr>");
			}
			document.write("</table>");
		}
		fn(5,5,"red");
		fn(6,6,"pink");
		fn(7,7,"blue");
		fn(8,8,"yellow");
	</script>


### *参数的默认值(初始化)

第一种初始化：

> 			if(row==undefined){
> 				row=10;
> 			}
> 			if(lie==undefined){
> 				lie=10;
> 			}
> 			if(color==undefined){
> 				color="red";
> 			}

第二种初始化：

> 			row=row||10;
> 			lie=lie||10;
> 			color=color||"red";

### *实参的个数超出形参的个数

arguments对象

每声明一个函数	函数的内容都会自动生成一个arguments对象	arguments对象会保存所有传递的实参

		function fun1(a,b){
			// 遍历
			for(var i=0;i<arguments.length;i++){
				console.log(arguments[i]);
			}
	
		}
		fun1(44,58,55,85,1)
## 5.函数的返回值

定义在函数内部的一个语法结构	返回的值就是函数调用表达式的结果

return  返回值;

返回值只能有一个

return语句之后代码会被自动忽略掉

return	可有可无	可以返回任意我们需要的值

## 6.函数的重载

即模拟函数重载		根据参数的个数和类型的不同执行不同的函数体

	<script>
		function fun3(){
			var sum=0;
			if(arguments.length==1){
				for(var i=0;i<=arguments[0];i++){
					sum+=i;
				}
			}
			else if(arguments.length>1){
				for(var i=0;i<arguments.length;i++){
					sum+=arguments[i];
				}
			}
			return sum;
		}
		console.log(fun3(10));
		console.log(fun3(10,10));
	</script>
## 7.环境

### *Js代码的执行分为两种环境执行

* 全局环境		整个script块
* 函数环境

### *任何一条语句在执行前都要先解析当前所处的环境

### *全局变量

如果在全局环境中声明一个变量，在整个全局环境中都可以访问到这个变量，也就称为当前的变量拥有全局的作用域	这个变量被称作全局变量

### *局部变量

如果在函数环境中声明一个变量，在这个当前的函数环境中都可以访问到这个变量，也就当前的作用域只在函数当中，这个变量被称作局部变量

### *产生作用域的实际的原因

在某个函数运行结束之后	函数内部声明的变量都被销毁掉了

保证全局变量不受污染	方便进行变量命名

函数的作用域和变量的作用域拥有完全相同的表现特征

## 8.作用域链

当我们访问某个变量的时候会从当前所在变量的环境中进行解析，如果在当前环境中找不到，则到当前环境的外部环境中寻找，一直找到全局环境为止

## 9.块级作用域

作用：ES6新增的let、const作用之后就被销毁了

if(){}		for(){}	while(){}	do() while{}