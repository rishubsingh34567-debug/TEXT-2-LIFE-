# TEXT-2-LIFE-
Text-to-Animation Conversion Users type any text → AI converts it into human-like animation.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Rishub AI – Text to Human Animation</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600&family=Roboto&display=swap" rel="stylesheet">

<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
  background:#0b0b0f;
  color:white;
  font-family:Roboto,sans-serif;
  overflow:hidden;
}
header{
  position:fixed;
  top:0;width:100%;
  padding:15px 40px;
  background:rgba(20,20,30,.9);
  display:flex;
  justify-content:space-between;
  align-items:center;
  z-index:10;
}
header h1{font-family:Orbitron;color:#7c3aed}

.contact-btn{
  background:#7c3aed;
  color:white;
  border:none;
  padding:8px 16px;
  border-radius:8px;
  cursor:pointer;
  font-size:15px;
}
.contact-btn:hover{background:#6d28d9}

.panel{
  position:absolute;
  left:20px;top:100px;
  width:320px;
  background:#111;
  padding:20px;
  border-radius:16px;
}
.panel textarea,.panel select,.panel input{
  width:100%;
  margin-top:10px;
  padding:10px;
  border-radius:8px;
  border:none;
  font-size:15px;
}
.panel button{
  margin-top:12px;
  width:100%;
  padding:12px;
  font-size:16px;
  background:#7c3aed;
  border:none;
  border-radius:8px;
  color:white;
  cursor:pointer;
}
.panel button:hover{background:#6d28d9}

canvas{
  position:absolute;
  right:0;top:0;
}

/* CONTACT MODAL */
.contact-modal{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,0.7);
  display:none;
  align-items:center;
  justify-content:center;
  z-index:20;
}
.contact-box{
  background:#111;
  padding:25px;
  border-radius:16px;
  width:320px;
  text-align:center;
}
.contact-box h2{
  font-family:Orbitron;
  color:#7c3aed;
  margin-bottom:10px;
}
.contact-box p{margin:8px 0;font-size:15px}
.contact-box a{
  display:block;
  color:#7c3aed;
  text-decoration:none;
  margin:6px 0;
}
.contact-box button{
  margin-top:12px;
  padding:10px;
  width:100%;
  background:#7c3aed;
  border:none;
  color:white;
  border-radius:8px;
  cursor:pointer;
}
</style>
</head>

<body>

<header>
  <h1>Rishub AI Studio</h1>
  <button class="contact-btn" onclick="openContact()">Contact</button>
</header>

<div class="panel">
  <h3>Text → Human Animation</h3>

  <textarea id="text" placeholder="Example: Excited dancing person"></textarea>

  <select id="motion">
    <option value="normal">Normal</option>
    <option value="cinematic">Cinematic</option>
    <option value="fast">High Energy</option>
    <option value="calm">Calm</option>
  </select>

  <select id="avatar">
    <option value="default">Default Human</option>
    <option value="robot">Robot</option>
    <option value="shadow">Shadow Person</option>
  </select>

  <input id="bg" placeholder="Background color (red / #111)" />

  <button onclick="start()">Animate</button>
  <button onclick="speak()">Generate Voice</button>
</div>

<canvas id="c"></canvas>

<!-- CONTACT MODAL -->
<div id="contactModal" class="contact-modal">
  <div class="contact-box">
    <h2>Contact Rishub</h2>

    <p>📧 rishubsingh34567@gmail.com</p>
    <p>📱 +91 8899453199</p>

    <a href="https://www.instagram.com/iam.rishub_fx?igsh=Nm5qN3FyZzByNTh3" target="_blank">Instagram</a>
    <a href="https://github.com/rishubsingh34567-debug" target="_blank">GitHub</a>
    <a href="https://www.youtube.com/@iam.rishub_fx" target="_blank">YouTube</a>

    <button onclick="closeContact()">Close</button>
  </div>
</div>

<script>
const canvas=document.getElementById("c");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

let t=0;
let text="Hello Human";
let mode="normal";
let avatar="default";

function start(){
  text=document.getElementById("text").value||"Hello Human";
  mode=document.getElementById("motion").value;
  avatar=document.getElementById("avatar").value;
  document.body.style.background=document.getElementById("bg").value||"#0b0b0f";
}

function drawHuman(x,y,scale){
  ctx.lineWidth=4;
  ctx.strokeStyle="#7c3aed";
  if(avatar==="robot") ctx.strokeStyle="#00f0ff";
  if(avatar==="shadow") ctx.strokeStyle="#aaa";

  ctx.beginPath();
  ctx.arc(x,y-60*scale,20*scale,0,Math.PI*2);
  ctx.stroke();

  ctx.beginPath();
  ctx.moveTo(x,y-40*scale);
  ctx.lineTo(x,y+40*scale);
  ctx.stroke();

  ctx.beginPath();
  ctx.moveTo(x-30*scale,y);
  ctx.lineTo(x+30*scale,y);
  ctx.stroke();

  ctx.beginPath();
  ctx.moveTo(x,y+40*scale);
  ctx.lineTo(x-25*scale,y+80*scale);
  ctx.moveTo(x,y+40*scale);
  ctx.lineTo(x+25*scale,y+80*scale);
  ctx.stroke();
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  let amp=20,speed=0.05,scale=1;
  if(mode==="fast"){amp=40;speed=0.12}
  if(mode==="cinematic"){amp=30;speed=0.07;scale=1.1}
  if(mode==="calm"){amp=10;speed=0.03}

  let x=canvas.width/2+Math.sin(t)*amp;
  let y=canvas.height/2+Math.cos(t)*amp;

  drawHuman(x,y,scale);

  ctx.font="32px Orbitron";
  ctx.fillStyle="white";
  ctx.fillText(text,x-ctx.measureText(text).width/2,y-120+Math.sin(t)*10);

  t+=speed;
  requestAnimationFrame(animate);
}
animate();

function speak(){
  const msg=new SpeechSynthesisUtterance(text);
  msg.rate=1;
  msg.pitch=1.1;
  speechSynthesis.speak(msg);
}

function openContact(){
  document.getElementById("contactModal").style.display="flex";
}
function closeContact(){
  document.getElementById("contactModal").style.display="none";
}
</script>

</body>
</html>
