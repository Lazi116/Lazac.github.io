<!DOCTYPE html>
<html lang="hu">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Neked ❤️</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;700&family=Montserrat:wght@300;400;500&family=Great+Vibes&display=swap" rel="stylesheet">
<style>
:root{
 --bg1:#1f1020;
 --bg2:#3a1c3f;
 --accent:#ff6fa5;
 --accent2:#ffd1dc;
 --text:#fff5f7;
}
*{margin:0;padding:0;box-sizing:border-box}
body{
 font-family:Montserrat, sans-serif;
 color:var(--text);
 background:linear-gradient(135deg,var(--bg1),var(--bg2));
 overflow-x:hidden;
}

h1,h2{font-family:'Playfair Display',serif}
.script{font-family:'Great Vibes',cursive}

nav{
 position:fixed;top:0;width:100%;
 background:rgba(0,0,0,.25);
 backdrop-filter:blur(10px);
 display:flex;justify-content:center;gap:30px;
 padding:18px;z-index:1000;
}
nav a{color:#fff;text-decoration:none;cursor:pointer;transition:.3s}
nav a:hover{color:var(--accent)}

.section{
 min-height:100vh;
 padding:120px 10% 60px;
 display:none;
 animation:fade .7s ease;
}
.section.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(20px)}to{opacity:1}}

.card{
 background:rgba(255,255,255,.08);
 border-radius:20px;
 padding:30px;
 margin:20px 0;
 backdrop-filter:blur(12px);
 box-shadow:0 10px 40px rgba(0,0,0,.3);
}

button{
 background:linear-gradient(90deg,var(--accent),#ff9ec4);
 border:none;color:white;padding:10px 20px;
 border-radius:30px;cursor:pointer;
}

.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px}

/* lebegő szívecskék */
canvas{position:fixed;top:0;left:0;z-index:-1}

/* modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,.6);display:none;align-items:center;justify-content:center}
.modalBox{background:#2a132d;padding:40px;border-radius:16px;max-width:420px;text-align:center}

.count{font-size:1.4rem;margin-top:10px}

input,textarea{
 width:100%;padding:10px;margin-top:10px;border-radius:10px;border:none;
}
</style>
</head>
<body>
<canvas id="hearts"></canvas>

<nav>
<a onclick="go('home')">Kezdőlap</a>
<a onclick="go('letter')">Levél</a>
<a onclick="go('memories')">Emlékek</a>
<a onclick="go('countdown')">Visszaszámláló</a>
<a onclick="go('why')">Miért szeretlek</a>
<a onclick="go('secret')">Titok</a>
</nav>

<section id="home" class="section active">
<h1 class="script" style="font-size:3rem">Ez az oldal érted készült</h1>
<div class="card">Nem azért, hogy "szép" legyen. Hanem hogy megmutassa, mennyire fontos vagy nekem.</div>
<div class="card">Minden kis részlet azért van itt, mert te vagy az életem része.</div>
</section>

<section id="letter" class="section">
<h2>Amit talán szóban nehéz elmondani</h2>
<div class="card" id="typed"></div>
</section>

<section id="memories" class="section">
<h2>Kis pillanatok</h2>
<div class="grid">
<div class="card"><button onclick="msg('Veled a legegyszerűbb dolgok is különlegesek.')">Megnyit</button></div>
<div class="card"><button onclick="msg('Amikor együtt vagyunk, minden kicsit könnyebb.')">Megnyit</button></div>
<div class="card"><button onclick="msg('Nem kell nagy dolgoknak történniük, hogy boldog legyek.')">Megnyit</button></div>
</div>
</section>

<section id="countdown" class="section">
<h2>Következő évfordulónkig</h2>
<div class="card"><div id="timer" class="count"></div></div>
</section>

<section id="why" class="section">
<h2>Miért szeretlek?</h2>
<div class="card">
<button onclick="generateReason()">Mutass egy okot</button>
<p id="reason" style="margin-top:15px"></p>
</div>
</section>

<section id="secret" class="section">
<h2>Ha idáig eljutottál…</h2>
<div class="card">Ez az oldal csak egy dologra akart emlékeztetni: fontos vagy nekem. Nagyon.</div>
</section>

<div class="modal" id="modal"><div class="modalBox" id="modalText"></div></div>

<script>
function go(id){document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');window.scrollTo(0,0)}

/* gépelős levél (Valentin-napi hangulat, nem szó szerint) */
const text=`Nem tudom, hogy lehet-e egy érzést igazán leírni.

De azt tudom, hogy mióta ismerlek, minden nap egy kicsit más lett.
Nem tökéletes — csak jobb. És nekem ez számít.

Nem nagy szavak miatt vagy fontos.
Hanem a mosolyod, a jelenléted, a közös pillanatok miatt.

Ez az oldal is csak egy apró próbálkozás arra,
hogy megmutassam: szeretlek.`;
let i=0;
function type(){if(i<text.length){document.getElementById('typed').innerHTML+=text.charAt(i);i++;setTimeout(type,25)}}
type();

/* visszaszámláló */
const target=new Date('2026-07-04T00:00:00');
setInterval(()=>{
let d=target-new Date();
let nap=Math.floor(d/86400000);
let ora=Math.floor(d/3600000)%24;
let perc=Math.floor(d/60000)%60;
let mp=Math.floor(d/1000)%60;
timer.innerHTML=`${nap} nap ${ora} óra ${perc} perc ${mp} mp`;
},1000);

/* random okok */
const reasons=[
"Mert veled önmagam lehetek.",
"Mert megnevettetsz.",
"Mert jó melletted lenni.",
"Mert számítasz nekem.",
"Mert együtt minden egyszerűbb."
];
function generateReason(){
reason.innerText=reasons[Math.floor(Math.random()*reasons.length)];
}

/* modal */
function msg(t){modal.style.display='flex';modalText.innerText=t}
modal.onclick=()=>modal.style.display='none';

/* lebegő szívek háttér */
const c=document.getElementById('hearts');
const x=c.getContext('2d');
c.width=innerWidth;c.height=innerHeight;
let h=[];
for(let i=0;i<60;i++)h.push({x:Math.random()*c.width,y:Math.random()*c.height,s:Math.random()*2+1,v:Math.random()*0.5});
(function draw(){
x.clearRect(0,0,c.width,c.height);
x.fillStyle='rgba(255,182,193,.7)';
h.forEach(o=>{x.beginPath();x.arc(o.x,o.y,o.s,0,6.28);x.fill();o.y-=o.v;if(o.y<0)o.y=c.height});
requestAnimationFrame(draw);
})();
</script>
</body>
</html>
