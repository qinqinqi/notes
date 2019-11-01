参考网址：json菜鸟教程



# 一、语法



{ "name":"runoob", "alexa":10000, "site":null }

1.在{}中书写

2.key 和 value 中使用冒号:分割。

3.每个 key/value 对使用逗号,分割。



# 二、访问对象值



## 1.使用点号.

var myObj, x;
myObj = { "name":"runoob", "alexa":10000, "site":null };
x = myObj.name;



## 2.使用中括号[]

var myObj, x;
myObj = { "name":"runoob", "alexa":10000, "site":null };
x = myObj["name"];



# 三、for-in循环对象



1.循环对象的属性

var myObj, x;
myObj = { "name":"runoob", "alexa":10000, "site":null };
x = myObj["name"];



2.访问属性的值，用[]

var myObj = { "name":"runoob", "alexa":10000, "site":null };
for (x in myObj) {
​    document.getElementById("demo").innerHTML += myObj[x] + "<br>";
}



# 四、嵌套 JSON 对象

myObj = {
​    "name":"runoob",
​    "alexa":10000,
​    "sites": {
​        "site1":"www.runoob.com",
​        "site2":"m.runoob.com",
​        "site3":"c.runoob.com"
​    }
}



`注意`你可以使用点号.或者中括号[]来访问嵌套的 JSON 对象

x = myObj.sites.site1;
// 或者
x = myObj.sites["site1"];



# 五、修改值

1.使用点号.进行修改

myObj.sites.site1 = "www.google.com";

2.使用中括号[]进行修改

myObj.sites["site1"] = "www.google.com";



# 六、删除对象属性（delete）

使用delete关键字

delete myObj.sites.site1;或者delete myObj.sites["site1"]



