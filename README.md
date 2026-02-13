<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Forever Us ❤️</title>

<style>
body{
margin:0;
overflow:hidden;
font-family:Arial, sans-serif;
background:url("bg.jpg") no-repeat center center fixed;
background-size:cover;
color:white;
}

/* Dark overlay */
body::before{
content:"";
position:fixed;
width:100%;
height:100%;
background:rgba(0,0,0,0.6);
z-index:0;
}

/* Lip intro */
#lip{
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
font-size:80px;
cursor:pointer;
animation:pulse 1.5s infinite;
z-index:5;
}
@keyframes pulse{
0%{transform:translate(-50%,-50%) scale(1);}
50%{transform:translate(-50%,-50%) scale(1.2);}
100%{transform:translate(-50%,-50%) scale(1);}
}

/* Photos */
.photo{
position:absolute;
width:120px;
border:4px solid white;
border-radius:10px;
box-shadow:0 0 20px white;
transform-origin:top center;
animation:swing 3s infinite ease-in-out;
z-index:2;
}
@keyframes swing{
0%{transform:rotate(-5deg);}
50%{transform:rotate(5deg);}
100%{transform:rotate(-5deg);}
}

/* Proposal */
#proposal{
display:none;
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
background:white;
color:black;
padding:30px;
border-radius:15px;
text-align:center;
z-index:10;
}

button{
padding:10px 25px;
margin:10px;
font-size:18px;
border:none;
border-radius:8px;
cursor:pointer;
}

#yesBtn{background:red;color:white;transition:0.4s;}
#noBtn{background:gray;color:white;position:relative;}

/* Map Scene */
#mapScene{
display:none;
position:absolute;
width:100%;
height:100%;
top:0;
left:0;
background:black;
z-index:20;
}

#mapImage{
position:absolute;
width:100%;
height:100%;
object-fit:cover;
}

#routeSVG{
position:absolute;
width:100%;
height:100%;
top:0;
left:0;
}

#travelHeart{
position:absolute;
font-size:28px;
}

#finalText{
position:absolute;
width:100%;
top:45%;
text-align:center;
font-size:38px;
display:none;
color:white;
}
</style>
</head>

<body>

<audio id="music">
<source src="Khat.mp3" type="audio/mpeg">
</audio>

<div id="lip">💋</div>

<!-- Photos -->
<img src="kush1.jpeg" class="photo" style="top:10%; left:10%;">
<img src="kush2.jpeg" class="photo" style="top:10%; right:10%;">
<img src="kush3.jpeg" class="photo" style="bottom:15%; left:15%;">
<img src="kush4.jpeg" class="photo" style="bottom:15%; right:15%;">
<img src="kush5.jpeg" class="photo" style="top:40%; left:45%; width:150px;">

<!-- Proposal -->
<div id="proposal">
<h2>Will You Be Mine Forever? ❤️</h2>
<button id="yesBtn">YES 💖</button>
<button id="noBtn">NO 😅</button>
</div>

<!-- Map Scene -->
<div id="mapScene">

<img src="map.jpg" id="mapImage">

<svg id="routeSVG">
<path id="routePath"
d="M 150 600 
C 400 200, 700 700, 
900 300 
S 1400 200, 
1700 500"
stroke="red"
stroke-width="5"
fill="transparent"
stroke-dasharray="4000"
stroke-dashoffset="4000"/>
</svg>

<div id="travelHeart">❤️</div>
<div id="finalText">Udham Singh Nagar ❤️ Hastinapur<br>Finally Together Forever</div>

</div>

<script>
let noCount=0;

/* First Click */
document.body.addEventListener("click",function(){
document.getElementById("music").play();
document.getElementById("lip").style.display="none";
setTimeout(()=>{
document.getElementById("proposal").style.display="block";
},2500);
},{once:true});

/* NO logic */
document.getElementById("noBtn").onclick=function(){
noCount++;
if(noCount<4){
this.style.position="absolute";
this.style.top=Math.random()*70+"%";
this.style.left=Math.random()*70+"%";
}else{
this.style.display="none";
document.getElementById("yesBtn").style.transform="scale(1.8)";
}
};

/* YES logic */
document.getElementById("yesBtn").onclick=function(){
document.getElementById("proposal").style.display="none";
startMap();
};

function startMap(){
document.getElementById("mapScene").style.display="block";

let path=document.getElementById("routePath");
let length=path.getTotalLength();

path.style.strokeDasharray=length;
path.style.strokeDashoffset=length;

/* Draw route for 2 minutes */
setTimeout(()=>{
path.style.transition="stroke-dashoffset 120s linear";
path.style.strokeDashoffset="0";
},1000);

let heart=document.getElementById("travelHeart");
let progress=0;

/* Move heart for full 3 minutes */
let move=setInterval(()=>{
progress+=0.00055;
let point=path.getPointAtLength(progress*length);
heart.style.left=point.x+"px";
heart.style.top=point.y+"px";

if(progress>=1){
clearInterval(move);
setTimeout(()=>{
document.getElementById("finalText").style.display="block";
},2000);
}
},20);
}
</script>

</body>
</html>
