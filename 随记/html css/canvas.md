canvas标签及对应属性、API详解、结合实际案例讲解：

https://blog.csdn.net/baidu_31683691/article/details/51669355



canvas的使用：

1.获得canvas对象

var canvas=document.getElementById('canvas');



2.绘制画布

var ctx=canvas.getContext('2d');    //3d可以使用  var ctx=canvas.getContext('webgl')





canvas的基本使用

1.坐标





toDataURL()会直接生成base64格式的图片