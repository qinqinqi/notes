## 1.什么是BOM

BOM是Brower Object Model的缩写，简称浏览器对象模型



## 2.能利用BOM做什么

获得并操作浏览器属性



## 3.BOM所有对象的核心-----window

window对象是BOM的顶层（核心）对象，所有对象都是通过它延申出来的，所以也可以称为window的子对象。

### 1)window的子对象有哪些

* document对象
* frames对象
* history对象
* location对象
* navigator对象
* screen对象

### 2)window对象的方法

* 窗体控制

​       moveBy(x,y)-----------从当前位置水平移动窗体X个像素，垂直移动Y个像素；

​       moveTo(x,y)-----------移动窗体左上角到相对于屏幕左上角的(x,y)点；

​       resizeTo(w,h)----------把窗体宽度调整为W，高度调整为H；

* 窗体滚动轴

​       scrollBy(x,y)-------------如果有滚动条，将滚动条移动到相对于当前滚动条的X或Y位置

​       scrollTo(x,y)-------------如果有滚动条，将滚动条移动到相对于窗体的X或Y位置

* 窗体焦点控制

  focus()--------------------使窗体或控件获得焦点

  blur()----------------------使窗体或控件失去焦点

* 新建窗体

  open()--------------------打开或弹出一个新窗体

  close()--------------------关闭窗体

  ```
   window.open(url, name, features, replace);
   
   /*url---------要载入窗体的URL
     name--------新建窗体的名称
     features----代表窗体特性的字符串（字符串中每个个性用逗号隔开），除特殊设置一般不写
     replace-----一个布尔值，说明新载入的页面是否替换当前载入的页面，默认为false
   */
   
   /*features参数说明
   	width、height------窗体的宽高，不能小于100
   	left、top----------窗体的左坐标、上坐标，不能为负值
   	location-----------窗体是否显示地址栏，默认为no
   	resiable-----------窗体是否通过拖动边线改变大小，默认为no
   	status-------------窗体是否显示状态栏，默认为no
   	toolbar------------窗体是否显示工具栏，默认为no
   	scrollbar-----------窗体内容超出可视范围，是否允许拖动，默认为no
   */
  ```

* 对话框

  alert(str)--------------------弹出消息对话框（对话框有“确定”按钮）

  confirm(str)---------------弹出消息对话框（对话框有“确定”、“取消”按钮）

  prompt(str,defaultValue)-------弹出消息对话框（对话框中有“确定”、“取消”按钮，还有一个文本输入框）

* 状态栏

  window.defaultStatus属性---------改变浏览器状态栏的默认显示（当状态栏没有其他显示时）

  window.status属性-------------------临时改变浏览器状态栏的默认显示

* 时间函数

  setTimeOut()----------暂停指定的毫秒数后执行指定的代码

  clearTimeOut()-------取消setTimeOut函数将要执行的代码

  setInterval()-----------间隔指定的毫秒数`不停`的执行指定的代码

  clearInterval()---------取消指定的setInterval函数将要执行的代码

  setTimeOut和setInterval都有两个参数，第一个设置要执行的代码，第二个是间隔毫秒数

### 3)history对象

在浏览器历史纪录中导航

* history对象的方法

  bck()-------------加载history列表中的前一个URL

  forward()------加载history列表中的后一个URL

  go(num)-------加载history列表中的某个URL

  `注意`

  history.go(-1)------------返回+刷新

  history.back()------------返回

### 4)location对象

属性

hash-------------设置或返回从#开始的URL

search----------设置或返回从?开始的URL

host--------------设置或返回主机名和当前URL的端口号

hostname------设置或返回当前URL的主机名

port--------------设置或返回当前URL的端口号

href---------------设置或返回完整的URL

pathname------设置或返回当前URL的路径

方法

assign()----------加载新的文档，这与直接给location.herf赋值一样的效果

reload()----------重新加载文档（设置为false时，等同于普通刷新效果；设置为true时，每次都会从服务器从新下载，等同于强制刷新效果）

replace()--------用新的文档替换当前文档，不会在history中生成新的纪录，直接覆盖原来的纪录

### 5)navigator对象

appcodeName-----浏览器的代码名

appName------------浏览器的名称

appVersion----------浏览器的版本号

..........

得到浏览器的信息



## 4.常用的浏览器属性

1. clientWidth;　　内容宽度Width+左右填充padding
2. clientHeight;　　内容高度height+上下填充padding
3. clientLeft;　　左边框的宽度相当于border-left
4. clientTop;　　上边框的宽度相当于border-top
5. offsetWidth;　　clientWidth+左右边框
6. offsetHeight;　　clientHeight+上下边框
7. scrollHeight;　　真实内容宽度+上填充padding
8. scrollWidth;　　真实内容宽度+左填充padding
9. scrollLeft;　　滚动条卷去的宽度
10. scrollTop;　　滚动条卷去的高度

关于操作浏览器本身的盒子模型信息

1. clientWidth、clientHeight、 表示浏览器可视窗口的宽高
2. scrollWidth、scrollHeight、 表示浏览器真实页面的宽高