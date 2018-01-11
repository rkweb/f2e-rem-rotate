# f2e-rem-rotate
rem布局 横竖屏旋转

## meta ##
    <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0,  user-scalable=0" name="viewport"/>
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
    if(netease.ua.weixin){
        if(window.orientation === 90 || window.orientation === -90){
            // 横屏 浏览器的宽度大于高度
            h();
        }
        if(window.orientation === 180 || window.orientation === 0){
            // 竖屏 浏览器的宽度小于高度
            v1();
        }
    }else{
        if(ww > wh){
        	 // 横屏
            h();  
        }else{
           // 竖屏
            v1();
        }
    }
}
// 横屏
function h(){
    setTimeout(function(){
        sv = 'w';
        var ww = $(window).width();
        var wh = $(window).height();

        screen.css({
            'left':"50%",
            'top':'50%',
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
// 竖屏
function v1(){
    setTimeout(function(){
    	sv = 'h';
       
        var ww = $(window).width();
        var wh = $(window).height();
        screen.css({
            'left':"50%",
            'top':'50%',
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


1. 背景图要加`background-size:cover`属性
2. 雪碧图`background-size: 整个雪碧图的宽，整个雪碧图的高`，用`background-position`定位每个小图
3. img要写width和height
4. 100px = 1rem 可以直接换算
5. js代码最好放在head里面
6. chrome模拟手机时，用原始尺寸，不要用原来自己设置的尺寸
7. 当页面中有canvas时，canvas按照设计图尺寸写，最后把canvas整体缩一下
	
```javascript
//当canvas不是全屏
$('canvas').css({
	'width': $(window).width(), 
	'height': canva原始的高度*$(window).width()/640
})
//当canvas是全屏
$('canvas').css({
	'width': $(window).width(), 
	'height': $(window).height()
})
```


## demo ##
[点击查看](http://test.go.163.com/go/2017/1009/rem/)
