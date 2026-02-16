<!DOCTYPE html>
<html lang="hu">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Neked 💗</title>
<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg1:#fff0f5;
  --bg2:#ffe4ec;
  --accent:#ff6b9a;
  --text:#4a2c35;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:'Inter',sans-serif;
  color:var(--text);
  background:linear-gradient(135deg,var(--bg1),var(--bg2));
  overflow-x:hidden;
}
nav{
  position:fixed;
  top:0;left:0;right:0;
  background:rgba(255,255,255,.7);
  backdrop-filter:blur(10px);
  padding:10px;
  display:flex;
  justify-content:center;
  gap:15px;
  z-index:10;
}
nav button{
  border:none;
  background:none;
  font-size:15px;
  color:var(--text);
  cursor:pointer;
  padding:6px 10px;
  border-radius:8px;
}
nav button:hover{background:#fff}
section{
  min-height:100vh;
  padding:100px 20px 60px;
  display:none;
  justify-content:center;
}
section.active{display:flex}
.container{
  max-width:620px; /* könnyű olvashatóság */
  width:100%;
}
h1{
  font-family:'Great Vibes',cursive;
  font-size:52px;
  text-align:center;
  margin-bottom:10px;
}
.short{
  text-align:center;
  font-size:18px;
  margin:14px 0;
  line-height:1.7;
}
.card{
  background:white;
  padding:18px;
  border-radius:18px;
  margin:12px 0;
  box-shadow:0 10px 25px rgba(0,0,0,.08);
  cursor:pointer;
  transition:.3s;
}
.card:hover{transform:scale(1.03)}
.reveal{display:none;margin-top:8px;color:#7a4b57}
.button{
  display:block;
  margin:20px auto;
  padding:12px 20px;
  border:none;
  border-radius:999px;
  background:var(--accent);
  color:white;
  font-size:15px;
  cursor:pointer;
}
.counter{
  text-align:center;
  font-size:20px;
  margin-top:20px;
}
.meter{
  height:10px;
  background:#ffd3e0;
  border-radius:10px;
  overflow:hidden;
  margin:20px 0;
}
.meter span{
  display:block;
  height:100%;
  width:0%;
  background:var(--accent);
  transition:1s;
}
.quote{
  text-align:center;
  font-size:17px;
  margin:25px 0;
  min-height:40px;
}
.fade{animation:fade .6s}
@keyframes fade{from{opacity:0;transform:translateY(8px)}to{opacity:1}}
</style>
</head>
<body>

<nav>
<button onclick="show('home')">Kezdőlap</button>
<button onclick="show('letter')">Levél</button>
<button onclick="show('time')">Mióta együtt</button>
<button onclick="show('why')">Miért szeretlek</button>
</nav>

<section id="home" class="active">
<div class="container">
<h1>Szia 💗</h1>
<p class="short">Ezt az oldalt nem csak csináltam.</p>
<p class="short">Hanem időt tettem bele.</p>
<p class="short">Mert te fontos vagy nekem.</p>

<div class="meter"><span id="loveMeter"></span></div>
<p class="short">Ez minden nappal nő 🙂</p>

<div class="card" onclick="toggle(this)">
Első gondolat reggel...
<div class="reveal">legtöbbször te vagy.</div>
</div>

<div class="card" onclick="toggle(this)">
Miért jó veled lenni?
<div class="reveal">Mert nyugodt vagyok melletted.</div>
</div>

<div class="card" onclick="toggle(this)">
Tudod mi a kedvenc részem?
<div class="reveal">Az, hogy együtt csinálunk akár semmit is.</div>
</div>

</div>
</section>

<section id="letter">
<div class="container">
<h1>Egy kis levél</h1>
<p class="short fade">Nem akarok nagy szavakat.</p>
<p class="short fade">Csak azt, hogy tudd...</p>
<p class="short fade">nagyon örülök, hogy vagy nekem.</p>
<p class="short fade">És minden nap, amióta együtt vagyunk, számít.</p>
<p class="short fade">Nem tökéletes.</p>
<p class="short fade">De igazi.</p>
</div>
</section>

<section id="time">
<div class="container">
<h1>Mióta együtt</h1>
<div class="counter" id="together"></div>
<p class="short">És ez csak megy tovább…</p>
</div>
</section>

<section id="why">
<div class="container">
<h1>Random ok 😄</h1>
<div class="quote" id="quote"></div>
<button class="button" onclick="newQuote()">Új ok</button>
</div>
</section>

<script>
function show(id){
 document.querySelectorAll('section').forEach(s=>s.classList.remove('active'));
 document.getElementById(id).classList.add('active');
}

function toggle(el){
 const r=el.querySelector('.reveal');
 r.style.display=r.style.display==='block'?'none':'block';
}

const start=new Date('2025-07-04T00:00:00');
function updateTime(){
 const now=new Date();
 const diff=now-start;
 const d=Math.floor(diff/86400000);
 const h=Math.floor(diff/3600000)%24;
 const m=Math.floor(diff/60000)%60;
 const s=Math.floor(diff/1000)%60;
 document.getElementById('together').innerText=
 `${d} nap ${h} óra ${m} perc ${s} mp`;
}
setInterval(updateTime,1000);
updateTime();

const quotes=[
"Mert jó veled beszélgetni.",
"Mert megnevettetsz.",
"Mert hiányzol, ha nem vagy ott.",
"Mert melletted könnyebb minden.",
"Mert te te vagy."
];
function newQuote(){
 document.getElementById('quote').innerText=
 quotes[Math.floor(Math.random()*quotes.length)];
}
newQuote();

// kis 'dopamin' animáció
setTimeout(()=>{
 document.getElementById('loveMeter').style.width='78%';
},500);
</script>

</body>
</html>
