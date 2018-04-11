# f2e-rem-rotate
rem布局 横竖屏旋转

## meta ##
    <meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0,  user-scalable=0" name="viewport"/>
# html #
    <div class="main">
        <div class="screen">
            <div class="wrap scale">
            测试    
            </div>
        </div>
    </div>

## css ##
	* {
            margin: 0;
            padding: 0;
        }
        html,body{
            width: 100%;
            height: 100%;
            overflow: hidden;
        }
        .main{
            width: 6.4rem;
            height: 100%;
            margin: 0 auto;
        }
        .screen{
            width: 100vh;
            height: 100vw;
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
            background: #ccc;
            position: absolute;
            left: 0;
            right: 0;
            bottom:0;
            top:0;
            margin: auto;
        }

## js ##
```
 // rem布局 放入head标签中
(function (psdWidth) {
    var resizeEvent = 'orientationchange' in window ? 'orientationchange' : 'resize';
    function rem() {
	var wWidth = window.innerWidth;
	var wHeight = window.innerHeight;
	var w;
	if (wWidth > wHeight) {
	    w = wHeight;
	} else {
	    w = wWidth;
	}
	var fontSize = w > 1000 ? 100 : 100 * w / psdWidth;
	document.documentElement.style.fontSize = fontSize + 'px';
    }
    rem();
    window.addEventListener(resizeEvent, function () {
	clearTimeout(timer);
	var timer = setTimeout(rem, 100);
    }, false);
})(640);  //传入设计稿宽度


//旋转屏幕
(function(){
    fitScreen();
    window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", fitScreen, false);
    function fitScreen() {
	var ww = $(window).width();
	var wh = $(window).height();
	if (window.orientation !== undefined) {
	    if (window.orientation === 90 || window.orientation === -90) {
		hor();// 横屏 
	    } else if (window.orientation === 180 || window.orientation === 0) {
		ver();
	    }
	} else {  //方便pc调试
	    if (ww > wh) {
		hor();  // 横屏
	    } else {
		ver();  // 竖屏
	    }

	}
    }
    var screenDom = $('.screen');
    // 横屏
    function hor() {
	setTimeout(function () {
	    var ww = $(window).width();
	    var wh = $(window).height();
	    screenDom.css({
		'width': ww + 'px',
		'height': wh + 'px',
		'transform': 'translate3d(-50%,-50%,0)',
		'-webkit-transform': 'translate3d(-50%,-50%,0)'
	    });
	}, 300);
    }
    // 竖屏
    function ver() {
	setTimeout(function () {
	    var ww = $(window).width();
	    var wh = $(window).height();
	    screenDom.css({
		'width': wh + 'px',
		'height': ww + 'px',
		'transform': 'translate3d(-50%,-50%,0) rotate(90deg)',
		'-webkit-transform': 'translate3d(-50%,-50%,0) rotate(90deg)'
	    });
	}, 300);
    }
})();


//缩放
(function (scaleHeight) {
    var wHeight = window.innerHeight;
    var scaleHeight = scaleHeight ? scaleHeight : 1030;
    var scale = function () {
	if (wHeight * 0.75 > window.innerHeight) {
	    return
	} //屏蔽软键盘弹起时触发resize事件（只考虑竖屏）
	var wWidth = window.innerWidth;
	var wHeight = window.innerHeight;
	var h = 640 / wWidth * wHeight;
	if (wWidth > wHeight) { //横屏判断
	    h = 640 / wHeight * wWidth;
	}
	if (h <= scaleHeight) {
	    $('.scale').css({
		'-webkit-transform': 'scale(' + h / scaleHeight + ')'
	    });
	}
    }
    scale();
})(1030); //传入内容安全区域高度（设计稿宽度换算成640）

```

## 注意 ##


1. 上面代码为常规专题（页面有主体内容1030*640）时
2. 视频及cavans时可能不需要主体内容wrap,只需要旋转screen就可以

	


## demo ##
[点击查看](http://go.163.com/web/f2e_common/common/f2e-rem/orient.html)
# 实际项目 #
[点击查看](http://test.go.163.com/go/2018/0101/haihang/index.html)
