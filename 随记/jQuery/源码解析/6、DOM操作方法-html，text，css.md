# 一、html-text-css的作用

* 都可以用来读取（get）设置（set）元素


* html()   用来读取和修改元素的HTML标签  
* text()    用来读取或修改元素的纯文本内容  
* css()      设置或返回被选元素的一个或多个样式属性 



```
text(),html(),css()都是通过jQuery.access提供底层支持。
jQuery.access()是一个多功能的方法，作为set和get值来使用。
```



# 二、text代码

```

jQuery.extend({
  access: function(elems, callback, key, value) {
    
  }
})

jQuery.fn.extend({
  text: function(value) {
    jQuery.access(this, function(){, null, value})
  }
})

```

