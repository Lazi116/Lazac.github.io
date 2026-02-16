<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Luca — Digital Universe</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">
<style>
:root{
 --bg1:#020617;
 --bg2:#0f172a;
 --accent:#f472b6;
 --accent2:#22d3ee;
 --glass:rgba(255,255,255,0.06);
 --text:#e2e8f0;
}
*{margin:0;padding:0;box-sizing:border-box}
body{
 font-family:'Montserrat',sans-serif;
 color:var(--text);
 background:radial-gradient(circle at 30% 20%,#111827,var(--bg1));
 overflow-x:hidden;
}

/* Sidebar */
.sidebar{
 position:fixed;
 left:0;top:0;
 height:100vh;width:220px;
 background:rgba(0,0,0,0.4);
 backdrop-filter:blur(12px);
 padding:30px 20px;
 z-index:1000;
}
.sidebar h2{font-family:'Playfair Display';margin-bottom:30px}
.sidebar a{
 display:block;
 margin:15px 0;
 color:#cbd5e1;
 text-decoration:none;
 transition:.3s;
}
.sidebar a:hover{color:var(--accent);transform:translateX(8px)}

main{margin-left:220px}

.section{
 min-height:100vh;
 padding:80px 8%;
 position:relative;
 display:none;
}
.section.active{display:block;animation:fade .9s ease}

@keyframes fade{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}

h1{font-family:'Playfair Display';font-size:3rem;margin-bottom:20px}

.card{
 background:var(--glass);
 border:1px solid rgba(255,255,255,0.1);
 border-radius:24px;
 padding:35px;
 margin:20px 0;
 backdrop-filter:blur(16px);
 transition:.4s;
}
.card:hover{transform:translateY(-8px) scale(1.01)}

.grid{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
 gap:20px;
}

button{
 background:linear-gradient(90deg,var(--accent),var(--accent2));
 border:none;padding:12px 22px;border-radius:40px;
 color:white;cursor:pointer;font-weight:600;
}

.countdown{font-size:1.4rem;margin-top:10px}

/* floating particles */
canvas{position:fixed;top:0;left:0;z-index:-1}

/* modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,.7);display:none;align-items:center;justify-content:center;z-index:2000}
.modal-box{background:#020617;padding:50px;border-radius:20px;max-width:500px;text-align:center}

/* music toggle */
.music{
 position:fixed;bottom:25px;right:25px;
 background:#111827;border-radius:50%;
 width:60px;height:60px;
 display:flex;align-items:center;justify-content:center;
 cursor:pointer;font-size:20px;
}
</style>
</head>
<body>

<canvas id="bg"></canvas>

<div class="sidebar">
 <h2>Luca</h2>
 <a onclick="go('home')">Home</a>
 <a onclick="go('story')">Story</a>
 <a onclick="go('timeline')">Timeline</a>
 <a onclick="go('countdown')">Countdown</a>
 <a onclick="go('memories')">Memories</a>
 <a onclick="go('secret')">Secret</a>
</div>

<main>
<section id="home" class="section active">
<h1>This is not a website.</h1>
<div class="card">This is a digital space built for one person only.</div>
<div class="card">Every animation, every pixel, every line exists because you exist.</div>
</section>

<section id="story" class="section">
<h1>Why You Matter</h1>
<div class="grid">
<div class="card">You changed ordinary days into meaningful ones.</div>
<div class="card">You made time feel faster and moments feel deeper.</div>
<div class="card">This page is just a reflection of that impact.</div>
</div>
</section>

<section id="timeline" class="section">
<h1>Our Timeline</h1>
<div class="card">The day everything started.</div>
<div class="card">The first time I realized you were different.</div>
<div class="card">All the small moments that became important.</div>
<div class="card">Right now — still writing this story.</div>
</section>

<section id="countdown" class="section">
<h1>Next Anniversary In</h1>
<div id="timer" class="countdown"></div>
</section>

<section id="memories" class="section">
<h1>Interactive Messages</h1>
<div class="grid">
<div class="card"><button onclick="msg('You are the calm in my chaos.')">Open</button></div>
<div class="card"><button onclick="msg('Some people exist. You feel like destiny.')">Open</button></div>
<div class="card"><button onclick="msg('If time had a favorite moment, it would be us.')">Open</button></div>
<div class="card"><button onclick="msg('This is only version 1 of something infinite.')">Open</button></div>
</div>
</section>

<section id="secret" class="section">
<h1>You weren’t supposed to find this.</h1>
<div class="card"><button onclick="msg('But I knew you would.')">Reveal</button></div>
</section>
</main>

<div class="modal" id="modal" onclick="closeMsg()">
<div class="modal-box" id="modalText"></div>
</div>

<div class="music" onclick="toggleMusic()">♫</div>
<audio id="audio" loop>
<source src="https://cdn.pixabay.com/audio/2022/03/15/audio_115b9bceef.mp3" type="audio/mpeg">
</audio>

<script>
function go(id){
 document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
 window.scrollTo(0,0);
}

function msg(t){
 modal.style.display='flex';
 modalText.innerText=t;
}
function closeMsg(){modal.style.display='none'}

/* countdown */
const target=new Date('2026-07-04T00:00:00');
setInterval(()=>{
 const now=new Date();
 const d=target-now;
 const days=Math.floor(d/1000/60/60/24);
 const h=Math.floor(d/1000/60/60)%24;
 const m=Math.floor(d/1000/60)%60;
 const s=Math.floor(d/1000)%60;
 timer.innerHTML=`${days}d ${h}h ${m}m ${s}s`;
},1000);

/* music */
let playing=false;
function toggleMusic(){
 if(!playing){audio.play()}else{audio.pause()}
 playing=!playing;
}

/* animated particles */
const c=document.getElementById('bg');
const x=c.getContext('2d');
c.width=innerWidth;c.height=innerHeight;
let p=[];
for(let i=0;i<160;i++){
 p.push({x:Math.random()*c.width,y:Math.random()*c.height,r:Math.random()*2,v:Math.random()*0.6});
}
function anim(){
 x.clearRect(0,0,c.width,c.height);
 x.fillStyle='white';
 p.forEach(o=>{
  x.beginPath();
  x.arc(o.x,o.y,o.r,0,Math.PI*2);
  x.fill();
  o.y+=o.v;
  if(o.y>c.height)o.y=0;
 });
 requestAnimationFrame(anim);
}
anim();

onresize=()=>{c.width=innerWidth;c.height=innerHeight}
</script>
</body>
</html>
