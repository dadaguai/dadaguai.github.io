<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		*{
			margin: 0;
			padding: 0;
			box-sizing: border-box;
		}
	    html,body{
	        width: 100%;
	        height: 100%;
	        background-color: #000;
	    }
	</style>
</head>
<body>
	<canvas id="myCanvas"></canvas>
</body>
<script>
window.requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame || window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;
var can=document.getElementById('myCanvas');
	can.width=document.body.clientWidth;
	can.height=document.body.clientHeight;
var ctx=can.getContext("2d");
var data=[];
can.addEventListener('mousemove',moveEvent,false)


function moveEvent(e){
	data.push({
		x:e.pageX,
		y:e.pageY,
		r:Math.floor( Math.random()*20 ),
		o:1,
		mx:Math.random()>0.5?Math.floor( Math.random()*10 ):-Math.floor( Math.random()*10 ),
		my:Math.random()>0.5?Math.floor( Math.random()*10 ):-Math.floor( Math.random()*2 )
	})
	//console.log(data)
}
function render(){
	ctx.clearRect(0,0,document.body.clientWidth,document.body.clientHeight);
	for (var i = 0; i < data.length; i++) {
		ctx.beginPath();
		ctx.fillStyle="#fff";
		ctx.globalAlpha=data[i].o;
		ctx.arc(data[i].x,data[i].y,data[i].r, 0, 2 * Math.PI);
		ctx.fill();
		ctx.closePath();
		data[i].x+=data[i].mx;
		data[i].y+=data[i].my;
		data[i].o-=0.01;
		if (data[i].o<=0) {
			data.splice(i,1);
		}
	}
	requestAnimationFrame( render );
}
requestAnimationFrame( render );

</script>
</html>
