# carrousel
carrousel

<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title>无标题文档</title>
    <style type="text/css">
        body, ul, ol, li, img {
            margin: 0;
            padding: 0;
            list-style: none;
        }

        #box {
            width: 490px;
            height: 170px;
            padding: 5px;
            position: relative;
            border: 1px solid #ccc;
            margin: 100px auto 0;
            overflow: hidden;
        }

        .ad {
            width: 490px;
            height: 170px;
            overflow: hidden;
            position: relative;
        }

        #box img {
            width: 490px;
        }

        .ad ol {
            position: absolute;
            right: 10px;
            bottom: 10px;
        }

        .ad ol li {
            width: 20px;
            height: 20px;
            line-height: 20px;
            border: 1px solid #ccc;
            text-align: center;
            background: #fff;
            float: left;
            margin-right: 10px;
            cursor: pointer;
            _display: inline;
        }

        .ad ol li.current {
            background: yellow;
        }

        .ad ul li {
            float: left;
        }

        .ad ul {
            position: absolute;
            top: 0;
            width: 2940px;
        }

        .ad ul li.current {
            display: block;
        }

        #arr {
            display: none;
        }

        #arr span {
            width: 40px;
            height: 40px;
            position: absolute;
            left: 5px;
            top: 50%;
            margin-top: -20px;
            background: #000;
            cursor: pointer;
            line-height: 40px;
            text-align: center;
            font-weight: bold;
            font-family: '黑体';
            font-size: 30px;
            color: #fff;
            opacity: 0.3;
            border: 1px solid #fff;
        }

        #arr #right {
            right: 5px;
            left: auto;
        }
    </style>
</head>
<body>
<div id="box" class="all">
    <div class="ad">
        <ul id="imgs">
            <li><img src="images/1.jpg"/></li>
            <li><img src="images/2.jpg"/></li>
            <li><img src="images/3.jpg"/></li>
            <li><img src="images/4.jpg"/></li>
            <li><img src="images/5.jpg"/></li>
        </ul>
    </div>
    <div id="arr"><span id="left"><</span><span id="right">></span></div>
</div>
</body>
</html>
<script>

    //1.鼠标移入的时候，让 箭头显示

    var box = document.getElementById('box');
    var oad = box.children[0];

    //鼠标移入事件

    // onmouseenter 鼠标进入  onmouseleave鼠标出去

    oad.onmouseenter = function () {

        var oArr = this.nextElementSibling || this.nextSibling;

        oArr.style.display = "block";


    }


    //	//2鼠标移除让箭头隐藏,从最大的盒子离开
    box.onmouseleave = function () {
        var oArr = document.getElementById('arr');
        oArr.style.display = "none";
    }


    var imgs = document.getElementById('imgs');

    //全局变量
    var tempIndex = 0;
    document.getElementById('right').onclick = function () {

        //点击的时候，调用我们的 animate的函数
        console.log(imgs);
        tempIndex++;

//        if(tempIndex>=4){
//            tempIndex=4;
//        }

//        tempIndex=tempIndex>=4?4:tempIndex

        tempIndex >= 4 ? tempIndex = 4 : tempIndex;

        animate(imgs, -490 * tempIndex)


    }


    document.getElementById('left').onclick = function () {

        //点击的时候，调用我们的 animate的函数
        console.log(imgs);
        tempIndex--;

//        if( tempIndex<=0){
//            tempIndex=0;
//        }

        tempIndex <= 0 ? tempIndex = 0 : tempIndex
        animate(imgs, -490 * tempIndex)

    }


    //匀速动画封装
    function animate(obj, target) {
        // 进来的之后，就先清空上一次余留定时器
        clearInterval(obj.timer)
        //判断一下方向。
        var step = obj.offsetLeft <= target ? 10 : -10;
        obj.timer = setInterval(function () {
            // 新的位置=当前的位置+步长；
            obj.style.left = obj.offsetLeft + step + "px";
            //在去获取当前新位置
            if (Math.abs(obj.offsetLeft - target) <= 10) {
                //没有到终点，或者超出终点，都保证只会停留在终点
                clearInterval(obj.timer);
                obj.style.left = target + "px";
            }
        }, 10)

    }


</script>
