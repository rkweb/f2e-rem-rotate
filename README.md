# f2e-rem-rotate
rem布局 横竖屏旋转

## meta ##
    <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0,  user-scalable=0" name="viewport"/>
# html #
    <!--旋转的盒子-->
	<div class="screen">
		
		<!--主体内容居中显示-->
		<div class="wrap"></div>
	
	</div>
## css ##
	.screen{
	    width: 100%;
	    height: 100%;
	    position: absolute;
	    left: 50%;
	    top: 50%;
	    overflow: hidden;
	    transform:translate3d(-50%,-50%,0) rotate(90deg);
	    -webkit-transform: translate3d(-50%,-50%,0) rotate(90deg);
	    margin: auto;
	}
	.wrap{
	    width: 10.3rem;
	    height: 6.4rem;
	    position: absolute;
	    left: 50%;
	    margin-left: -5.15rem;
	    top: 50%;
	    margin-top: -3.2rem;
	    -webkit-transform-origin: center center;
	    background: green;
	    opacity: 0.5; 
	}
## js ##
```javascript  
var screen = $(".screen")  //旋转的盒子  

//主体内容的初始宽高
var wrapW = $('.wrap').width();
var wrapH = $('.wrap').height();  

//调用
fitScreen();
window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize",fitScreen, false);
function fitScreen(){
    var  ww = $(window).width();
    var wh = $(window).height();
    if(netease.ua.weixin || window.orientation){
        if(window.orientation === 90 || window.orientation === -90){
            // 横屏 浏览器的宽度大于高度
            hor();
        }
        if(window.orientation === 180 || window.orientation === 0){
            // 竖屏 浏览器的宽度小于高度
            ver();
        }
    }else{
        if(ww > wh){
        	 // 横屏
            hor();  
        }else{
           // 竖屏
            ver();
        }
    }
}

// 横屏函数
function hor(){
    setTimeout(function(){
        sv = 'w';
        var ww = $(window).width();
        var wh = $(window).height();
        screen.css({
            'width':ww + 'px',
            'height':wh + 'px',
            'transform':'translate3d(-50%,-50%,0)',
            '-webkit-transform':'translate3d(-50%,-50%,0)'
        });
		
        var scale = wh / wrapW < ww / wrapH ? wh / wrapW : ww / wrapH;
        $('.wrap').css({
        	'transform': 'scale('+scale+')'
        });
    },300);
}

// 竖屏函数
function ver(){
    setTimeout(function(){
    	sv = 'h';
       
        var ww = $(window).width();
        var wh = $(window).height();
        screen.css({
            'width':wh + 'px',
            'height':ww + 'px',
            'transform':'translate3d(-50%,-50%,0) rotate(90deg)',
            '-webkit-transform':'translate3d(-50%,-50%,0) rotate(90deg)'
        });

        var scale = ww / wrapW < wh / wrapH ? ww / wrapW : wh / wrapH;
        $('.wrap').css({
        	'transform': 'scale('+scale+')'
        });
    },300);
}
```

## 注意 ##


1. 上面代码为常规专题（页面有主体内容1030*640）时
2. 视频及cavans时可能不需要主体内容wrap,只需要旋转screen就可以

	


## demo ##
[点击查看](http://go.163.com/web/f2e_common/common/f2e-rem/orient.html)
# 实际项目 #
[点击查看](http://test.go.163.com/go/2018/0101/haihang/index.html)
