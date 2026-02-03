<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Birthday Surprise 💖</title>

<style>
* { box-sizing:border-box; margin:0; padding:0; }

html { scroll-behavior:smooth; }

body {
  font-family: Arial, sans-serif;
  overflow-x:hidden;
  background:#f7c9d9;
}

/* Sections */
section {
  min-height:100vh;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  text-align:center;
  color:white;
  padding:30px;
  opacity:0;
  transform:translateY(40px);
  transition:all 0.8s ease;
}

section.active {
  opacity:1;
  transform:translateY(0);
}

/* Backgrounds */
#p1 { background:radial-gradient(#ff9a9e,#fad0c4); }
#p2 { background:linear-gradient(#fbc2eb,#a6c1ee); }
#p3 { background:linear-gradient(#ffecd2,#fcb69f); }
#p4 { background:linear-gradient(#ff9a9e,#fecfef); }
#p5 { background:linear-gradient(#84fab0,#8fd3f4); }
#p6 { background:linear-gradient(#ff758c,#ff7eb3); }

/* Button */
.btn {
  padding:18px 40px;
  border-radius:50px;
  background:#ff4081;
  color:white;
  font-size:20px;
  cursor:pointer;
  border:none;
  margin-top:20px;
  box-shadow:0 10px 25px rgba(0,0,0,0.3);
}

/* Candle */
.candle {
  width:20px;
  height:60px;
  background:white;
  margin-top:20px;
  position:relative;
  cursor:pointer;
}

.flame {
  width:20px;
  height:20px;
  background:orange;
  border-radius:50%;
  position:absolute;
  top:-20px;
  animation:flicker 0.5s infinite;
}

@keyframes flicker {
  50% { transform:scale(1.2); }
}

/* Floating hearts */
.heart {
  position:fixed;
  bottom:-20px;
  width:20px;
  height:20px;
  background:pink;
  transform:rotate(45deg);
  animation:float 6s linear infinite;
}

.heart::before,.heart::after{
  content:"";
  position:absolute;
  width:20px;
  height:20px;
  background:pink;
  border-radius:50%;
}

.heart::before { top:-10px; }
.heart::after { left:-10px; }

@keyframes float {
  to { transform:translateY(-120vh) rotate(45deg); opacity:0; }
}

/* Falling hearts */
.falling-heart {
  position:fixed;
  font-size:35px;
  cursor:pointer;
  user-select:none;
}

/* Popup */
.popup {
  position:fixed;
  bottom:20px;
  background:rgba(0,0,0,0.7);
  color:white;
  padding:10px 20px;
  border-radius:20px;
  animation:fade 3s forwards;
}

@keyframes fade {
  to { opacity:0; transform:translateY(-20px); }
}

.signature { margin-top:30px; font-style:italic; }
</style>
</head>

<body>

<section id="p1" class="active">
  <h1>Tap for a Surprise 🎉</h1>
  <button class="btn" onclick="start()">Touch Me 💖</button>
</section>

<section id="p2">
  <h1>Happy Birthday ❤️</h1>
  <p>You make the world softer, warmer, and better ✨</p>
  <button class="btn" onclick="goTo('p3')">Next →</button>
</section>

<section id="p3">
  <h1>Memories 💫</h1>
  <p>Every moment with you is special,<br>even without pictures 💖</p>
  <button class="btn" onclick="goTo('p4')">Next →</button>
</section>

<section id="p4">
  <h1>Make a Wish 🎂</h1>
  <p>Click the candle 🕯️</p>
  <div class="candle" onclick="blow()">
    <div class="flame" id="flame"></div>
  </div>
  <button class="btn" onclick="goTo('p5')">Next →</button>
</section>

<section id="p5">
  <h1>Catch Falling Hearts 💕</h1>
  <p>Tap the hearts for surprises</p>
  <button class="btn" onclick="goTo('p6')">Final →</button>
</section>

<section id="p6">
  <h1>Happy Birthday Dhana 🎉</h1>
  <p>You are deeply loved 💖</p>
  <p class="signature">— Yours, always 🌸</p>
</section>

<script>
let started=false;
const music=new Audio("https://cdn.pixabay.com/audio/2022/03/15/audio_8b9c1f7d48.mp3");

function goTo(id){
  document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
  const target=document.getElementById(id);
  target.classList.add("active");
  target.scrollIntoView({behavior:"smooth"});
}

function start(){
 if(started) return;
 started=true;
 music.play();
 goTo("p2");
 hearts();
 fallingHearts();
}

function hearts(){
 setInterval(()=>{
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),6000);
 },900);
}

function blow(){
 document.getElementById("flame").style.display="none";
 popup("Wish granted ✨");
}

let heartCount=0;
function fallingHearts(){
 setInterval(()=>{
  if(heartCount>10) return;
  heartCount++;

  const h=document.createElement("div");
  h.className="falling-heart";
  h.innerText="💖";
  h.style.left=Math.random()*90+"vw";
  document.body.appendChild(h);

  let y=-40;
  const fall=setInterval(()=>{
    y+=3;
    h.style.transform=`translateY(${y}px)`;
    if(y>innerHeight){
      h.remove();
      heartCount--;
      clearInterval(fall);
    }
  },16);

  h.onclick=()=>{
    popup("You are loved 💕");
    h.remove();
    heartCount--;
    clearInterval(fall);
  };
 },1200);
}

function popup(text){
 const p=document.createElement("div");
 p.className="popup";
 p.innerText=text;
 document.body.appendChild(p);
 setTimeout(()=>p.remove(),3000);
}
</script>

</body>
</html>
