# 1.判断鼠标移入方向

<script>

​        $("li").on("mouseenter mouseleave",function(e) {

​           var w = this.offsetWidth;

​           var h = this.offsetHeight;

​           var toTop = this.getBoundingClientRect().top + document.body.scrollTop;  //兼容滚动条

​           var x = (e.pageX - this.getBoundingClientRect().left - (w / 2)) * (w > h ? (h / w) : 1);   //获取当前鼠标的x轴位置

​           var y = (e.pageY - toTop - h/2) * (h > w ? (w / h) : 1);

​          //上面对长方形也做了兼容，也就是按照最小的那个边的一半作为半径了

​          //例如有一个宽6，高是2的矩形 右上角的坐标就是{x:3,y:1}，经过上面的计算后{x:2/6 * 3,y:1}=》{x:1,y:1}   算出来也就是45°的样子

​          //如果是正方形，可以去掉后面的系数（w>h && h>w）

​           var direction = Math.round((((Math.atan2(y, x) * 180 / Math.PI) + 180) / 90) + 3) % 4; //direction的值为“0,1,2,3”分别对应着“上，右，下，左”

​           var eventType = e.type;

​           var res = Math.atan2(y, x) / (Math.PI / 180) + 180 ;  

​           // console.log(((Math.atan2(y, x) * 180 / Math.PI) + 180));

​           // console.log(Math.round((Math.atan2(y, x) / (Math.PI / 180) + 180) / 90 + 3) % 4);

​           var dirName = new Array('上方','右侧','下方','左侧');

​           if(eventType == 'mouseenter'){

​              console.log(dirName[direction]+'进入');

​                

​            }else{

​                console.log(dirName[direction]+'离开');

​            }

​        });

​    </script>

# 2.响应式固定定位

	<script>
	  function fixeds(){
	    $(".fixed").each(function(){
	        var windowwidth = document.documentElement.clientWidth;
	        var fixedwidth = $(this).width();
	        var kszone = ( windowwidth - 1000 ) / 2 -10;
	        if ( kszone >= fixedwidth ){
	            $(this).css("right",kszone - fixedwidth );	
	        }else{
	            $(this).css("right","10px");	
	        }
	            $(this).fadeIn();
	    })
	  }
	  
	  fixeds();
	  $(window).resize(function(){fixeds();})
	</script>


