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
body.dark{
  --bg1:#1f1020;
  --bg2:#3a1c3f;
  --accent:#ff6fa5;
  --text:#fff5f7;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:'Inter',sans-serif;
  color:var(--text);
  background:linear-gradient(135deg,var(--bg1),var(--bg2));
  overflow-x:hidden;
  transition:background 0.5s,color 0.5s;
}
nav{
  position:fixed;top:0;left:0;right:0;
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
  max-width:620px;
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
#darkModeToggle{
  position:fixed;
  bottom:20px;
  right:20px;
  background:var(--accent);
  border:none;
  border-radius:50%;
  width:50px;
  height:50px;
  font-size:24px;
  color:white;
  cursor:pointer;
  box-shadow:0 4px 12px rgba(0,0,0,.3);
}
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
<p class="short">Ez az oldal rólad szól.</p>
<p class="short">Minden apró részletet azért tettem ide, mert szeretlek.</p>
<div class="meter"><span id="loveMeter"></span></div>
<p class="short">Ez a szeretet napról napra nő 🙂</p>
<div class="card" onclick="toggle(this)">Első gondolat reggel...<div class="reveal">legtöbbször te vagy.</div></div>
<div class="card" onclick="toggle(this)">Miért jó veled lenni?<div class="reveal">Mert nyugodt vagyok melletted.</div></div>
<div class="card" onclick="toggle(this)">Kedvenc pillanat?<div class="reveal">Kedvenc??? Veled??? Az összes egyértelmű.</div></div>
</div>
</section>

<section id="letter">
<div class="container">
<h1>Egy kis levél</h1>
<p class="short fade">Veled minden perc ertelmet nyer,</p>
<p class="short fade">Minden pillanat veled otthon.</p>
<p class="short fade">Szeretlek, nem tudnék nélküled élni.</p>
<p class="short fade">Minden nap, amióta együtt vagyunk, egyre jobban</p>
<p class="short fade">Ez a kapcsolat nem tökéletes, de igazi.</p>
</div>
</section>

<section id="time">
<div class="container">
<h1>Mióta együtt</h1>
<div class="counter" id="together"></div>
<p class="short">És ez csak megy tovább és tovább amíg élek sőt még utána is…</p>
</div>
</section>

<section id="why">
<div class="cont8ainer">
<h1>Miért is szeretlek?(itt van pár ok te kuki)</h1>
<div class="quote" id="quote"></div>
<button class="button" onclick="newQuote()">Új ok</button>
</div>
</section>

<button id="darkModeToggle" onclick="toggleDark()">🌓</button>

<script>
function show(id){document.querySelectorAll('section').forEach(s=>s.classList.remove('active'));document.getElementById(id).classList.add('active');}
function toggle(el){const r=el.querySelector('.reveal');r.style.display=r.style.display==='block'?'none':'block';}
const start=new Date('2025-07-04T00:00:00');
function updateTime(){const now=new Date();const diff=now-start;const d=Math.floor(diff/86400000);const h=Math.floor(diff/3600000)%24;const m=Math.floor(diff/60000)%60;const s=Math.floor(diff/1000)%60;document.getElementById('together').innerText=`${d} nap ${h} óra ${m} perc ${s} mp`;}
setInterval(updateTime,1000);updateTime();

// Miért szeretlek - sok ok
const quotes=[
"Mert boldogabb vagyok veled.","Mert megnevettetsz.","Mert hiányzol, ha nem vagy ott.","Mert melletted minden könnyebb.","Mert te te vagy.","Mert mindig figyelsz rám.","Mert veled minden egyszerűbb.","Mert a mosolyod szebb barki mosolyanal.","Mert inspirálsz.","Mert a hangod megnyugtat.","Mert szeretem, ahogy gondolkodsz.","Mert minden nap jobbá teszed az életem.","Mert tudod, mikor kell hallgatni.","Mert szeretsz apró dolgokat csinálni.","Mert nevetésed fülemnek a leszebb zene","Mert veled minden pillanat különleges." ];
function newQuote(){document.getElementById('quote').innerText=quotes[Math.floor(Math.random()*quotes.length)];}
newQuote();

// dopaminos csík
setTimeout(()=>{document.getElementById('loveMeter').style.width='78%';},500);

// sötét/világos mód
function toggleDark(){document.body.classList.toggle('dark');}
</script>

</body>
</html>
