<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Birthday Surprise 💖</title>
<style>
* { box-sizing: border-box; margin:0; padding:0; }
body { font-family: Arial, sans-serif; overflow-x:hidden; scroll-behavior: smooth; background:#f7c9d9; }

/* Sections */
section { min-height:100vh; display:flex; flex-direction:column; justify-content:center; align-items:center; text-align:center; color:white; padding:30px; }

/* Section Colors */
#p1 { background: radial-gradient(#ff9a9e,#fad0c4);}
#p2 { background: linear-gradient(#fbc2eb,#a6c1ee);}
#p3 { background: linear-gradient(#ffecd2,#fcb69f);}
#p4 { background: linear-gradient(#ff9a9e,#fecfef);}
#p5 { background: linear-gradient(#84fab0,#8fd3f4);}
#p6 { background: linear-gradient(#ff758c,#ff7eb3);}

/* Buttons */
.btn { padding:18px 40px; border-radius:50px; background:#ff4081; color:white; font-size:20px; cursor:pointer; border:none; margin-top:20px; box-shadow:0 10px 25px rgba(0,0,0,0.3); }

/* Hearts */
.heart { position:fixed; bottom:-20px; width:20px; height:20px; background:pink; transform:rotate(45deg); animation:float 6s linear infinite; }
.heart::before,.heart::after{ content:""; position:absolute; width:20px; height:20px; background:pink; border-radius:50%; }
.heart::before {top:-10px; left:0;} .heart::after {left:-10px; top:0;}
@keyframes float { to {transform:translateY(-120vh) rotate(45deg); opacity:0;} }

/* Slideshow */
.slideshow { width:300px; height:350px; overflow:hidden; border-radius:20px; box-shadow:0 15px 30px rgba(0,0,0,0.4); position:relative; }
.slideshow img { width:100%; height:100%; object-fit:cover; position:absolute; opacity:0; transition:opacity 1.5s ease; }

/* Candle */
.candle { width:20px; height:60px; background:white; margin-top:20px; position:relative; cursor:pointer; }
.flame { width:20px; height:20px; background:orange; border-radius:50%; position:absolute; top:-20px; animation:flicker 0.5s infinite; }
@keyframes flicker { 50% { transform: scale(1.2); } }

/* Fireworks */
.firework { position:fixed; width:5px; height:5px; border-radius:50%; background:yellow; pointer-events:none; }

/* Messages */
.popup { position:fixed; bottom:20px; background:rgba(0,0,0,0.7); color:white; padding:10px 20px; border-radius:20px; animation:fade 3s forwards; }
@keyframes fade { to {opacity:0; transform:translateY(-20px);} }

.signature { margin-top:30px; font-style:italic; }

/* Mini-game hearts */
.falling-heart { position:fixed; font-size:35px; cursor:pointer; user-select:none; }
</style>
</head>

<body>

<!-- Page 1 -->
<section id="p1">
<h1>Tap for a Surprise 🎉</h1>
<button class="btn" onclick="start()">Touch Me 💖</button>
</section>

<!-- Page 2 -->
<section id="p2">
<h1>Happy Birthday ❤️</h1>
<p>You make the world softer, warmer, and better ✨</p>
<a href="#p3" class="btn">Next →</a>
</section>

<!-- Page 3 Slideshow -->
<section id="p3">
<h1>Memories 📸</h1>
<div class="slideshow">
  <img src=d:\Album\birthday\DSC_0850.JPG>
  <img src=d:\Album\birthday\DSC_0779.JPG>
  <img src=d:\Album\birthday\DSC_0728.JPG>
</div>
<a href="#p4" class="btn">Next →</a>
</section>

<!-- Page 4 Candle -->
<section id="p4">
<h1>Make a Wish 🎂</h1>
<p>Click the candle to blow it out 🕯️</p>
<div class="candle" onclick="blow()">
  <div class="flame" id="flame"></div>
</div>
<a href="#p5" class="btn">Next →</a>
</section>

<!-- Page 5 Mini-game -->
<section id="p5">
<h1>Catch Falling Hearts 💕</h1>
<p>Click the hearts to unlock messages!</p>
<div id="messages"></div>
<a href="#p6" class="btn">Final →</a>
</section>

<!-- Page 6 Final -->
<section id="p6">
<h1>Happy Birthday Dhana 🎉</h1>
<p>You are deeply loved, endlessly cherished, and never alone. Always remember that 💖</p>
<p class="signature">— Yours, always 🌸</p>
</section>

<script>
// Globals
let started=false;

// Music
const music = new Audio("https://cdn.pixabay.com/audio/2022/03/15/audio_8b9c1f7d48.mp3");

// Start
function start(){
 if(started) return;
 started=true;
 location.href="#p2";
 music.play();
 hearts();
 glitter();
 slideshow();
 fallingHearts();
}

// Floating Hearts
function hearts(){
 setInterval(()=>{
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),6000);
 },500);
}

// Glitter
function glitter(){
 for(let i=0;i<50;i++){
  const g=document.createElement("div");
  g.style.position="fixed";
  g.style.left=Math.random()*100+"vw";
  g.style.top="-10px";
  g.style.width="5px";
  g.style.height="5px";
  g.style.background=`hsl(${Math.random()*360},100%,70%)`;
  document.body.appendChild(g);
  g.animate([{transform:"translateY(0)"},{transform:"translateY(110vh)"}],{duration:3000+Math.random()*2000});
  setTimeout(()=>g.remove(),5000);
 }
}

// Slideshow
function slideshow(){
 const slides=document.querySelectorAll(".slideshow img");
 let index=0;
 slides[index].style.opacity=1;
 setInterval(()=>{
   slides[index].style.opacity=0;
   index=(index+1)%slides.length;
   slides[index].style.opacity=1;
 },4000);
}

// Candle blow
function blow(){
 document.getElementById("flame").style.display="none";
 firework();
}

// Firework
function firework(){
 for(let i=0;i<30;i++){
  const f=document.createElement("div");
  f.className="firework";
  f.style.left=window.innerWidth/2+"px";
  f.style.top=window.innerHeight/2+"px";
  f.style.background=`hsl(${Math.random()*360},100%,70%)`;
  document.body.appendChild(f);
  const x=(Math.random()-0.5)*500;
  const y=(Math.random()-0.5)*500;
  f.animate([{transform:"translate(0,0)"},{transform:`translate(${x}px,${y}px)`}],{duration:1000});
  setTimeout(()=>f.remove(),1200);
 }
}

// Falling hearts mini-game
function fallingHearts(){
 setInterval(()=>{
  const heart=document.createElement("div");
  heart.className="falling-heart";
  heart.innerText="💖";
  heart.style.left=Math.random()*90+"vw";
  heart.style.top="-50px";
  document.body.appendChild(heart);
  heart.onclick=()=>{
    heart.remove();
    showMessage();
  };
  const fall=setInterval(()=>{
    const top=parseInt(heart.style.top);
    if(top>window.innerHeight){
      heart.remove();
      clearInterval(fall);
    } else {
      heart.style.top=top+4+"px";
    }
  },20);
 },800);
}

// Show random message
const msgs=["You’re loved 💖","Smile, birthday star ✨","You matter 😌","Best human ever 🫶"];
function showMessage(){
 const p=document.createElement("div");
 p.className="popup";
 p.innerText=msgs[Math.floor(Math.random()*msgs.length)];
 document.body.appendChild(p);
 setTimeout(()=>p.remove(),3000);
}
</script>
</body>
</html>
