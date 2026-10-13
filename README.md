# My-game
M.html

<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>LOS SANTOS - الکی گیم</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#090b12;color:white;font-family:Arial,sans-serif;overflow:hidden}
button{font-family:inherit;cursor:pointer}
#loading{
position:fixed;inset:0;z-index:10;overflow:hidden;
background:linear-gradient(160deg,#4d8fba,#e0a16e 55%,#25272c);
display:flex;align-items:center;justify-content:center;
}
#skyline{position:absolute;bottom:0;width:100%;height:65%;
background:linear-gradient(transparent,#17202b)}
.building{position:absolute;bottom:0;background:#222b36;border:2px solid #35414c}
.b1{left:3%;width:15%;height:48%}
.b2{left:20%;width:12%;height:72%}
.b3{left:35%;width:18%;height:40%}
.b4{right:20%;width:15%;height:66%}
.b5{right:3%;width:14%;height:48%}
#sun{position:absolute;top:9%;left:13%;width:100px;height:100px;
background:#ffda9b;border-radius:50%;box-shadow:0 0 80px #ffd49b}
.loadContent{position:relative;z-index:2;width:min(90%,650px);text-align:center;
padding:24px;background:#11151ac9;border:1px solid #ffffff33;border-radius:12px}
.logo{font-size:clamp(38px,9vw,75px);font-weight:1000;letter-spacing:2px;
text-shadow:4px 4px #222;color:#fff}
.logo span{color:#80e86c}
.subtitle{color:#ddd;font-size:13px;letter-spacing:2px}
#slide{font-size:48px;margin:12px}
#update{min-height:45px;color:#ddd;font-size:14px;line-height:1.8}
.bar{height:12px;background:#444;border:1px solid #aaa;margin:20px 0 10px;overflow:hidden}
#progress{width:0;height:100%;background:#82e65d;transition:width .15s}
#percent{font-size:13px;color:#b9fca5}
#enter{display:none;background:#7ee65a;color:#101010;font-weight:bold;
border:0;border-radius:6px;padding:13px 30px;margin-top:15px}
#game{display:none;height:100dvh;background:linear-gradient(#68b7df 0 45%,#648d43 45% 100%);position:relative}
.top{display:flex;justify-content:space-between;gap:6px;padding:12px;font-weight:bold}
.stat{background:#10151dcc;border-radius:9px;padding:10px;font-size:14px}
#field{position:absolute;inset:65px 0 100px;overflow:hidden}
#road{position:absolute;bottom:0;left:0;width:100%;height:28%;
background:#45484c;border-top:5px solid #bdb9a8}
#road:after{content:"";position:absolute;left:0;right:0;top:50%;
border-top:5px dashed #f7e8a3}
#player{position:absolute;bottom:8%;left:50%;transform:translateX(-50%);
font-size:54px;z-index:2;filter:drop-shadow(2px 4px 2px #333)}
.coin{position:absolute;font-size:34px;cursor:pointer;user-select:none;
filter:drop-shadow(0 2px 4px #333);animation:bob .7s infinite alternate}
@keyframes bob{to{transform:translateY(-8px) rotate(10deg)}}
#hint{position:absolute;bottom:76px;width:100%;text-align:center;font-size:13px;color:#fff;text-shadow:1px 2px #222}
.controls{position:absolute;bottom:10px;width:100%;display:flex;justify-content:space-around;align-items:center}
.ctrl{width:65px;height:55px;background:#111c;color:white;border:1px solid #ffffff77;border-radius:15px;font-size:25px}
#overlay{display:none;position:absolute;inset:0;background:#000c;z-index:5;
align-items:center;justify-content:center;text-align:center;padding:20px}
.panel{background:#151922;border:1px solid #ffffff44;border-radius:15px;padding:28px;width:min(90%,400px)}
.panel h2{font-size:30px}
.panel button{padding:13px 25px;margin:6px;border:0;border-radius:7px;background:#83e65d;font-weight:bold}
#notice{color:#d8f9c9;font-size:13px}
</style>
</head>
<body>

<section id="loading">
<div id="sun"></div>
<div id="skyline">
<div class="building b1"></div><div class="building b2"></div>
<div class="building b3"></div><div class="building b4"></div>
<div class="building b5"></div>
</div>
<div class="loadContent">
<div class="logo">LOS <span>SANTOS</span></div>
<div class="subtitle">THE MOST USELESS GAME EVER</div>
<div id="slide">🚘 🌴 💸</div>
<h3>به شهر لوس الکی خوش آمدی!</h3>
<p id="update">در حال آماده‌سازی شهر...</p>
<div class="bar"><div id="progress"></div></div>
<div id="percent">0%</div>
<button id="enter">ورود به بازی 🚀</button>
</div>
</section>

<main id="game">
<div class="top">
<div class="stat">💵 پول: <span id="money">0</span></div>
<div class="stat">🏆 رکورد: <span id="best">0</span></div>
<div class="stat">⏱️ <span id="time">45</span></div>
</div>
<div id="field">
<div id="road"></div>
<div id="player">🏃</div>
</div>
<div id="hint">💸 پول‌ها رو لمس کن و جمع کن! با دکمه‌ها حرکت کن.</div>
<div class="controls">
<button class="ctrl" id="left">⬅️</button>
<button class="ctrl" id="jump">⬆️</button>
<button class="ctrl" id="right">➡️</button>
</div>
<div id="overlay">
<div class="panel">
<h2 id="result">پایان بازی!</h2>
<p id="resultText">نتیجه</p>
<p id="notice">زندگی بی‌معنی است، ولی پول جمع کن 😂</p>
<button id="again">دوباره بازی کن</button>
<button id="menu">منوی اصلی</button>
</div>
</div>
</main>

<script>
const $=id=>document.getElementById(id);
const messages=[
"در حال ساختن برج‌های الکی...",
"در حال آوردن ماشین‌های خیالی...",
"در حال شمارش پول‌های مردم...",
"در حال فراری دادن پلیس‌ها...",
"تقریباً آماده‌ایم!"
];
let pct=0,slide=0;
const loader=setInterval(()=>{
 pct=Math.min(100,pct+Math.random()*4+1);
 $("progress").style.width=pct+"%";
 $("percent").textContent=Math.floor(pct)+"%";
 if(Math.floor(pct)%20<4)$("update").textContent=messages[Math.min(4,Math.floor(pct/20))];
 if(pct>=100){
  clearInterval(loader);
  $("update").textContent="شهر آماده است! بزن بریم 😎";
  $("enter").style.display="inline-block";
 }
},120);
setInterval(()=>{
 slide++;
 $("slide").textContent=["🚘 🌴 💸","🚁 🌇 💰","🏍️ 🏙️ 💵","🚓 💸 🏃"][slide%4];
},1800);

let x=50,money=0,time=45,active=false,coins=[],spawnTimer=null,clock=null;
let best=Number(localStorage.getItem("sillyBest")||0);
$("best").textContent=best;
function position(){
 $("player").style.left=x+"%";
}
function move(dir){if(!active)return;x=Math.max(7,Math.min(93,x+dir*7));position()}
$("left").addEventListener("pointerdown",e=>{e.preventDefault();move(-1)});
$("right").addEventListener("pointerdown",e=>{e.preventDefault();move(1)});
$("jump").addEventListener("pointerdown",e=>{
 e.preventDefault();if(!active)return;
 $("player").style.bottom="25%";
 setTimeout(()=>$("player").style.bottom="8%",350);
});
document.addEventListener("keydown",e=>{
 if(e.key==="ArrowLeft"||e.key==="a")move(-1);
 if(e.key==="ArrowRight"||e.key==="d")move(1);
 if(e.key==="ArrowUp"||e.key===" ") $("jump").click();
});
function spawn(){
 if(!active)return;
 const c=document.createElement("div");
 c.className="coin";
 c.textContent=Math.random()<.2?"💎":"💵";
 c.style.left=(5+Math.random()*85)+"%";
 c.style.top="0px";
 $("field").appendChild(c);
 coins.push({el:c,y:0,x:parseFloat(c.style.left),value:c.textContent==="💎"?5:1});
}
function finish(){
 active=false;clearInterval(clock);clearInterval(spawnTimer);
 coins.forEach(c=>c.el.remove());coins=[];
 $("overlay").style.display="flex";
 $("result").textContent=money>=20?"سلطان لوس سانتوس! 👑":"پولدار نشدی داداش 😂";
 $("resultText").textContent="پول جمع‌شده: "+money+" | رکورد: "+best;
}
function start(){
 $("loading").style.display="none";
 $("game").style.display="block";
 $("overlay").style.display="none";
 $("field").querySelectorAll(".coin").forEach(c=>c.remove());
 coins=[];x=50;money=0;time=45;active=true;
 $("money").textContent=money;$("time").textContent=time;position();
 clearInterval(clock);clearInterval(spawnTimer);
 spawnTimer=setInterval(spawn,700);
 clock=setInterval(()=>{
  if(!active)return;
  time--;$("time").textContent=time;
  if(time<=0)finish();
 },1000);
}
function frame(){
 if(active){
  for(let i=coins.length-1;i>=0;i--){
   const c=coins[i];c.y+=2.5;c.el.style.top=c.y+"px";
   if(c.y>$("field").clientHeight){c.el.remove();coins.splice(i,1);continue}
   const playerY=$("field").clientHeight*.78;
   if(c.y>playerY-45&&c.y<playerY+50&&Math.abs(c.x-x)<10){
    money+=c.value;$("money").textContent=money;
    c.el.remove();coins.splice(i,1);
    if(money>best){best=money;$("best").textContent=best;localStorage.setItem("sillyBest",best)}
   }
  }
 }
 requestAnimationFrame(frame);
}
$("enter").onclick=start;
$("again").onclick=start;
$("menu").onclick=()=>{
 $("overlay").style.display="none";$("game").style.display="none";
 $("loading").style.display="flex";
};
frame();
</script>
</body>
</html>
