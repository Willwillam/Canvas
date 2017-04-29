# Canvas
使用Canvas实现微信红包看照片效果

HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>微信玩转小红包</title>
<script src="http://libs.baidu.com/jquery/2.0.0/jquery.js"></script>
<link href="css/样式.css" type="text/css" rel="stylesheet">
</head>

<body>
<div id="box">
	<img src="img/1.JPG" id="blur-image">
	<canvas id="canvas">
	</canvas>
<a href="javascript:reset()" class="button" id="resetbutton">reset</a>
<a href="javascript:show()" class="button" id="showbutton">show</a>

</div>
<script src="js/脚本.js"></script>

</body>

</html>




CSS
@charset "utf-8";
/* CSS Document */
#box{
	width:640px;
	height:852px;
	margin:0 auto;
	position:relative;
	}
#blur-image{
	display:block;
	width:640px;
	height:852px;
	margin:0 auto;
	filter:blur(15px);
	-moz-fliter:blur(15px);
	-ms-fliter:blur(15px);
	-o-fliter:blur(15px);
	-webkit-fliter:blur(15px);
	left:0px;
	top:0px;
	position:absolute;
	z-index:0;
	}
#canvas{
	display:block;
	width:640px;
	height:852px;
	margin:0 auto;
	position:absolute;
	left:0px;
	top:0px;
	
	z-index:100;
	}
.button{
	 display:block;
	 position:absolute;
	 z-index:200;
	 
	 width:100px;
	 height:50px;
	 font-size:18px;
	 color:#FFFFFF;
	 text-decoration:none;
	 text-align:center;
	 line-height:50px;
	 
	 border-radius:5px;
	}
#resetbutton{
	left:100px;
	bottom:20px;
	background-color:#006;
	}	
#resetbutton:hover{
	background-color:#03F;
	}
#showbutton{
	right:100px;
	bottom:20px;
	background-color:#006;
	}
#showbutton:hover{
	background-color:#03F;
	}			
	
  
  
  JS
  // JavaScript Document
var convasWidth = 640;
var convasHeight = 852;

var canvas=document.getElementById("canvas");
var context=canvas.getContext("2d");

canvas.width=convasWidth;
canvas.height=convasHeight;
var image=new Image()
var radius=50;
var clippingRegion={x:200,y:200,r:radius};
image.src="img/1.JPG" ;
image.onload=function(e){
	initcanvas();
	}
function initcanvas(){
    clippingRegion={x:Math.random()*(convasWidth-2*radius)+
	radius,y:Math.random()*(convasHeight-2*radius)+radius,r:radius};	
	draw(image,clippingRegion);
	}
function setClippingRegion(clippingRegion){
	context.beginPath();
	context.arc(clippingRegion.x,clippingRegion.y,clippingRegion.r,0,Math.PI*2,false);
	context.clip();
	}	
function draw(image,clippingRegion){
	context.clearRect(0,0,convasWidth ,convasHeight);
	context.save();
	setClippingRegion(clippingRegion);
	context.drawImage(image,0,0);
	context.restore();
	}	
function show(){
var theAnimation =setInterval(function(){
		clippingRegion.r+=20;
		if(clippingRegion.r>1066){
			clearInterval(theAnimation);
			}
			draw(image,clippingRegion);	
		},30)
	}
function reset(){
	
	initcanvas();
	}




	
