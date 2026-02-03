<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Birthday Surprise 💖</title>

<style>
* { box-sizing:border-box; margin:0; padding:0; }

html {
  scroll-behavior: smooth;
}

body {
  font-family: Arial, sans-serif;
  overflow-x:hidden;
  background:#f7c9d9;
  scroll-snap-type: y mandatory;
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
  scroll-snap-align:start;
  opacity:0;
  transform:translateY(40px);
  transition:all 0.8s ease;
}

section:target,
section:first-of-type {
  opacity:1;
  transform:translateY(0);
}

/* Section Colors */
#p1 { background:radial-gradient(#ff9a9e,#fad0c4); }
#p2 { background:linear-gradient(#fbc2eb,#a6c1ee); }
#p3 { background:linear-gradient(#ffecd2,#fcb69f); }
#p4 { background:linear-gradient(#ff9a9e,#fecfef); }
#p5 { background:linear-gradient(#84fab0,#8fd3f4); }
#p6 { background:linear-gradient(#ff758c,#ff7eb3); }

/* Buttons */
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

.heart::before { top:-10px; left:0; }
.heart::after { left:-10px; top:0; }

@keyframes float {
  to { transform:translateY(-120vh) rotate(45deg); opacity:0; }
}

/* Slideshow */
.slideshow {
  width:300px;
  height:350px;
  overflow:hidden;
  border-radius:20px;
  box-shadow:0 15px 30px rgba(0,0,0,0.4);
  position:relative;
}

.slideshow img {
  width:100%;
  height:100%;
  object-fit:cover;
  position:absolute;
  opacity:0;
  transition:opacity 1.5s ease;
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

/* Falling hearts */
.falling-heart {
  position:fixed;
  font-size:35px;
  cursor:pointer;
  user-select:none;
  will-change:transform;
}

.signature {
  margin-top:30px;
  font-style:italic;
}
</style>
</head>

<body>

<section id="p1">
<h1>Tap for a Surprise 🎉</h1>
<button class="btn" onclick="start()">Touch Me 💖</button>
</section>

<section id="p2">
<h1>Happy Birthday ❤️</h1>
<p>You make the world softer, warmer, and better ✨</p>
<a href="#p3" class="btn">Next →</a>
</section>

<section id="p3">
<h1>Memories 📸</h1>
<div class="slideshow">
  <img src="images/img1.jpg">
  <img src="images/img2.jpg">
  <img src="images/img3.jpg">
</div>
<a href="#p4" class="btn">Next →</a>
</section>

<section id="p4">
<h1>Make a Wish 🎂</h1>
<p>Click the candle 🕯️</p>
<div class="candle" onclick="blow()">
  <div class="flame" id="flame"></div>
</div>
<a href="#p5" class="btn">Next →</a>
</section>

<section id="p5">
<h1>Catch Falling Hearts 💕</h1>
<a href="#p6" class="btn">Final →</a>
</section>

<section id="p6">
<h1>Happy Birthday Dhana 🎉</h1>
<p>You are deeply loved 💖</p>
<p class="signature">— Yours, always 🌸</p>
</section>

<script>
let started=false;
const music=new Audio("https://cdn.pixabay.com/audio/2022/03/15/audio_8b9c1f7d48.mp3");

function start(){
 if(started) return;
 started=true;
 location.href="#p2";
 music.play();
 setTimeout(hearts,500);
 setTimeout(slideshow,800);
 setTimeout(fallingHearts,1200);
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

function slideshow(){
 const slides=document.querySelectorAll(".slideshow img");
 let i=0;
 slides[i].style.opacity=1;
 setInterval(()=>{
  slides[i].style.opacity=0;
  i=(i+1)%slides.length;
  slides[i].style.opacity=1;
 },3500);
}

function blow(){
 document.getElementById("flame").style.display="none";
 popup("Wish granted ✨");
}

let heartCount=0;
const MAX=12;

function fallingHearts(){
 setInterval(()=>{
  if(heartCount>=MAX) return;
  heartCount++;

  const h=document.createElement("div");
  h.className="falling-heart";
  h.innerText="💖";
  h.style.left=Math.random()*90+"vw";
  document.body.appendChild(h);

  let y=-50;
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
