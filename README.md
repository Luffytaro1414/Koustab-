<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine Story</title>

<style>
body{
  margin:0;
  height:100vh;
  background:linear-gradient(135deg,#ff5f9e,#ff9a9e);
  font-family: Arial, sans-serif;
  color:white;
  overflow:hidden;
  text-align:center;
}
.page{
  display:none;
  height:100vh;
  justify-content:center;
  align-items:center;
  flex-direction:column;
}
.page.active{display:flex;}
.card{
  background:rgba(255,255,255,0.22);
  padding:25px;
  border-radius:20px;
  max-width:90%;
  backdrop-filter:blur(12px);
  position:relative;
}
button{
  padding:12px 24px;
  border:none;
  border-radius:25px;
  margin:8px;
  font-size:17px;
  cursor:pointer;
}
.no{
  background:#444;
  color:#fff;
  position:relative;
}
.yes{
  background:#ff2e7e;
  color:white;
}
.msg{
  margin-top:10px;
  font-size:16px;
  opacity:0.9;
}
.promise{
  background:rgba(255,255,255,0.25);
  padding:12px;
  border-radius:15px;
  margin:8px 0;
  transition:0.3s;
}
.promise:hover{
  background:rgba(255,255,255,0.4);
  transform:scale(1.03);
}
.fall{
  position:fixed;
  top:-30px;
  font-size:26px;
  animation:fall 6s linear forwards;
}
.sparkle{
  position:absolute;
  font-size:20px;
  animation:spark 1s forwards;
}
@keyframes fall{
  to{transform:translateY(110vh);opacity:0;}
}
@keyframes spark{
  to{transform:translateY(-40px);opacity:0;}
}
.big{font-size:80px;}
.poem{font-size:15px;line-height:1.6;}
</style>
</head>

<body>

<!-- PAGE 1 -->
<div class="page active" id="p1">
  <div class="card">
    <h2>Will you be my valentine my lady? ❤️</h2>
    <button class="yes" onclick="go('p2','❤️',this)">YES</button>
    <button class="no" onclick="moveNo(this,'🥺 Think once more…')">NO</button>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 2 -->
<div class="page" id="p2">
  <div class="card">
    <h3>🌹 Rose Day</h3>
    <p>Will you accept this rose my lady?</p>
    <button class="yes" onclick="go('p3','🌹',this)">YES</button>
    <button class="no" onclick="deny(this,'💔 Rose is waiting…')">NO</button>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 3 -->
<div class="page" id="p3">
  <div class="card">
    <h3>💍 Propose Day</h3>
    <p>Will you be Koushiki and samanya's mother? 🤧</p>
    <button class="yes" onclick="go('p4','💍',this)">YES</button>
    <button class="no" onclick="deny(this,'😶 That was rude…')">NO</button>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 4 -->
<div class="page" id="p4">
  <div class="card">
    <h2>This teddy needs your love 🤧</h2>
    <button class="yes" onclick="go('p5','🧸',this)">Give love 🧸</button>
    <button class="no" onclick="deny(this,'😢 Teddy sad…')">NO</button>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 5 PROMISE DAY -->
<div class="page" id="p5">
  <div class="card">
    <h2>🤞 Promise Day</h2>

    <div class="promise">🫶 I'll be your biggest supporter</div>
    <div class="promise">💯 I'll never let you regret choosing me</div>
    <div class="promise">😊 I'll always make you happy</div>

    <button class="yes" onclick="go('p6','🤞',this)">I Accept</button>
    <button class="no" onclick="deny(this,'🙂 Promises still stand.')">NO</button>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 6 -->
<div class="page" id="p6">
  <div class="card">
    <h2>Hug and kiss day 😚🫂</h2>
    <p>Sending kissy and warm hug for my lady 😗</p>
    <button class="yes" onclick="hugYes(this)">Receive ❤️</button>
    <button class="no" onclick="deny(this,'😌 Hug reserved.')">NO</button>
    <div id="hug"></div>
    <div class="msg"></div>
  </div>
</div>

<!-- PAGE 7 FINAL -->
<div class="page" id="p7">
  <div class="card">
    <h2>I love you My lady 🥹❤️</h2>
    <div class="poem">
      Tum hakikat ho ya koyi haseen khwaab ho<br>
      Mere sune se dil ka tumhi jawab ho<br>
      Jindegi khubsurat hain sirf tumhari wajah se<br>
      Mere jeene ki wajah aur mera pyara sa gulab ho ❤️✨
    </div>
  </div>
</div>

<script>
let fallInterval;

function sparkle(btn){
  let s=document.createElement("div");
  s.className="sparkle";
  s.innerText="✨";
  s.style.left="50%";
  s.style.top="0";
  btn.appendChild(s);
  setTimeout(()=>s.remove(),1000);
}

function go(id,emoji,btn){
  sparkle(btn);
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  rain([emoji,"❤️"]);
}

function deny(btn,text){
  btn.parentElement.querySelector('.msg').innerText=text;
}

function moveNo(btn,text){
  btn.style.left = Math.random()*120 - 60 + "px";
  btn.style.top = Math.random()*80 - 40 + "px";
  btn.parentElement.querySelector('.msg').innerText=text;
}

function hugYes(btn){
  sparkle(btn);
  document.getElementById("hug").innerHTML="<div class='big'>🫂❤️</div>";
  setTimeout(()=>go('p7','💖',btn),1200);
}

function rain(emojis){
  clearInterval(fallInterval);
  fallInterval=setInterval(()=>{
    let e=document.createElement("div");
    e.className="fall";
    e.innerText=emojis[Math.floor(Math.random()*emojis.length)];
    e.style.left=Math.random()*100+"vw";
    document.body.appendChild(e);
    setTimeout(()=>e.remove(),6000);
  },500);
}
</script>

</body>
</html># Koustab-
