# 一、版本号

Alpha：是内部测试版,一般不向外部发布,会有很多Bug.一般只有测试人员使用。(一般不用)
Beta：也是测试版，这个阶段的版本会一直加入新的功能。在Alpha版之后推出。
α、β、λ常用来表示软件测试过程中的三个阶段，α是第一阶段，一般只供内部测试使用；β是第二个阶段，已经消除了软件中大部分的不完善之处，但仍有可能还存在缺陷和漏洞，一般只提供给特定的用户群来测试使用；λ是第三个阶段，此时产品已经相当成熟，只需在个别地方再做进一步的优化处理即可上市发行。 

# 二、作用

html2canvas可以通过纯JS对浏览器端进行截屏，但截图的精确度还有待提高，部分css不可识别，所以在canvas中不能完美呈现原画面样式

# 三、支持的浏览器

- Firefox 3.5+
- Google Chrome
- Opera 12+
- IE9+
- Safari 6+

# 四、参数

## 1.scale：

用来调整生成图片屏幕分辨率，其实设置成1在iphone上生成的图片清晰度没啥问题，但是在有些android手机上就很模糊，所以为了兼顾这部分手机就把scale设置成了2;

## 2.useCROS

用来设置是否允许使用跨域的图片进行访问，默认是true

## 3.logging

在console.log()中输出信息，默认为false

## 4.allowTaint

是否允许污染

## 5.background

用来设置canvas的背景颜色，默认透明

## 6.letterRendering

用来设置字间距

## 7.proxy

用来设置代理地址

## 8.taintTest

是否在渲染前测试图片

## 9.timeout

图片加载延迟，默认延迟为0，单位毫秒

## 10.width、height

用来设置canvcas的宽高

# 五、canvas污染

不通过 CORS 可以在画布中使用图片，但是这会**污染**画布。一旦画布被污染，无法读取其数据。例如，不能再使用画布的 `toBlob()`, `toDataURL()` 或 `getImageData()` 方法，调用它们会抛出安全错误。这种机制可以避免未经许可拉取远程网站信息而导致的用户隐私泄露。

# 六、canvas将img转base64

    <script>
    function getBase64Image(imgurl) {
        var img = new Image();//初始化
        img.src = imgurl;
        img.setAttribute('crossOrigin', 'anonymous');
        img.onload=function(){
            var canvas = document.createElement("canvas");
            canvas.width = 300;//这个设置不能丢，否则会成为canvas默认的300*150的大小
            canvas.height = 300;//这个设置不能丢，否则会成为canvas默认的300*150的大小
            var ctx = canvas.getContext("2d");//绘图环境，如果getContext的参数是"webgl",就表示用于生成3D图像（即立体图案）.
            ctx.drawImage(img, 0, 0, 300, 300);
            var dataURL = canvas.toDataURL("image/png"); 
            console.log(dataURL)
            $("#img").attr("src",dataURL);
            html2img();
        }
    }
    </script>		


# 七、下载html2canvas.js

https://www.bootcdn.cn/html2canvas/

