<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Luca — Experience</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root{
 --bg:#020617;--panel:#0b1220;--soft:#0f172a;--text:#e5e7eb;--accent:#f472b6;--accent2:#22d3ee;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Inter,system-ui;background:radial-gradient(circle at 30% 10%,#0b1020,var(--bg));color:var(--text);overflow-x:hidden}

/* progress bar */
#progress{position:fixed;top:0;left:0;height:3px;background:linear-gradient(90deg,var(--accent),var(--accent2));width:0%;z-index:3000}

/* sidebar */
.sidebar{position:fixed;left:0;top:0;width:240px;height:100vh;background:rgba(10,15,30,.6);backdrop-filter:blur(14px);padding:28px}
.sidebar h1{font-family:'Playfair Display';font-size:1.6rem;margin-bottom:30px}
.sidebar a{display:block;color:#cbd5e1;text-decoration:none;margin:14px 0;transition:.25s}
.sidebar a:hover{color:var(--accent);transform:translateX(6px)}

main{margin-left:240px}
.section{min-height:100vh;padding:70px 8%;display:none}
.section.active{display:block;animation:fade .6s ease}
@keyframes fade{from{opacity:0;transform:translateY(12px)}to{opacity:1}}

h2{font-family:'Playfair Display';margin-bottom:16px}
.card{background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.08);padding:28px;border-radius:18px;margin:18px 0;backdrop-filter:blur(10px)}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px}

button{background:linear-gradient(90deg,var(--accent),var(--accent2));border:none;color:white;padding:10px 18px;border-radius:999px;cursor:pointer}

/* letter style */
.letter{background:#fdfaf6;color:#222;padding:40px;border-radius:6px;font-family:'Playfair Display';line-height:1.7;box-shadow:0 20px 60px rgba(0,0,0,.4)}
.type{border-right:2px solid #222;white-space:pre-line;overflow:hidden}

/* modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,.7);display:none;align-items:center;justify-content:center}
.modalBox{background:var(--panel);padding:40px;border-radius:16px;max-width:480px;text-align:center}

/* command palette */
#cmd{position:fixed;top:20%;left:50%;transform:translateX(-50%);background:var(--panel);padding:20px;border-radius:12px;width:420px;display:none}
#cmd input{width:100%;padding:10px;background:#020617;border:1px solid #1f2937;color:white}

canvas{position:fixed;inset:0;z-index:-1}
</style>
</head>
<body>
<div id="progress"></div>
<canvas id="bg"></canvas>

<div class="sidebar">
<h1>Luca</h1>
<a onclick="go('home')">Home</a>
<a onclick="go('letter')">The Letter</a>
<a onclick="go('time')">Time</a>
<a onclick="go('moments')">Moments</a>
<a onclick="go('hidden')">Hidden</a>
</div>

<main>
<section id="home" class="section active">
<h2>Welcome</h2>
<div class="card">This is designed like a real product, but it only has one user.</div>
<div class="card">Everything here is intentional.</div>
</section>

<section id="letter" class="section">
<h2>A Letter For You</h2>
<div class="letter"><div id="typed" class="type"></div></div>
</section>

<section id="time" class="section">
<h2>Time Until Our Next Chapter</h2>
<div class="card"><div id="timer"></div></div>
</section>

<section id="moments" class="section">
<h2>Fragments</h2>
<div class="grid">
<div class="card"><button onclick="openMsg('Some meetings change nothing. Some change everything.')">Open</button></div>
<div class="card"><button onclick="openMsg('Time moves normally. Except when I am with you.')">Open</button></div>
<div class="card"><button onclick="openMsg('This is not memory. This is ongoing.')">Open</button></div>
</div>
</section>

<section id="hidden" class="section">
<h2>You Found This</h2>
<div class="card">Not everything is meant to be obvious.</div>
</section>
</main>

<div class="modal" id="modal"><div class="modalBox" id="modalText"></div></div>

<div id="cmd"><input placeholder="Type: home / letter / time ..." onkeydown="cmdNav(event)"></div>

<script>
/* navigation */
function go(id){document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');}

/* typing letter */
const text=`I don't know if websites are supposed to feel like this.\n\nBut this one exists because of you.\nNot to impress. Not to show.\nJust to hold something real in a digital space.`;
let i=0;function type(){if(i<text.length){typed.innerHTML+=text.charAt(i);i++;setTimeout(type,28);}}type();

/* countdown */
const target=new Date('2026-07-04');
setInterval(()=>{
let d=target-new Date();
let days=Math.floor(d/86400000);
let h=Math.floor(d/3600000)%24;
let m=Math.floor(d/60000)%60;
let s=Math.floor(d/1000)%60;
timer.innerHTML=`${days}d ${h}h ${m}m ${s}s`;
},1000);

/* modal */
function openMsg(t){modal.style.display='flex';modalText.innerText=t}
modal.onclick=()=>modal.style.display='none';

/* command palette */
document.addEventListener('keydown',e=>{if(e.ctrlKey&&e.key==='k'){e.preventDefault();cmd.style.display='block';cmd.querySelector('input').focus();}});
function cmdNav(e){if(e.key==='Enter'){go(e.target.value.toLowerCase());cmd.style.display='none';}}

/* scroll progress */
window.onscroll=()=>{let h=document.documentElement.scrollHeight-window.innerHeight;progress.style.width=(window.scrollY/h)*100+'%'};

/* animated background */
const c=document.getElementById('bg');const x=c.getContext('2d');c.width=innerWidth;c.height=innerHeight;
let p=Array.from({length:120},()=>({x:Math.random()*c.width,y:Math.random()*c.height,r:Math.random()*2,v:Math.random()*0.4}));
(function a(){x.clearRect(0,0,c.width,c.height);x.fillStyle='white';p.forEach(o=>{x.beginPath();x.arc(o.x,o.y,o.r,0,6.28);x.fill();o.y+=o.v;if(o.y>c.height)o.y=0});requestAnimationFrame(a);})();
</script>
</body>
</html>
