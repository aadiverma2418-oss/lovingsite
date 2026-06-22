<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For My Love ❤️</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --accent:#ff5fa2;
  --bg:#0b0614;
  --glow:0 0 20px rgba(255,95,162,.9);
}
*{box-sizing:border-box}
body{
  margin:0;
  min-height:100vh;
  background:radial-gradient(circle at top,#1a0d2e,var(--bg));
  color:#fff;
  font-family:system-ui;
  display:flex;
  justify-content:center;
  align-items:center;
  text-align:center;
}
.view{display:none;animation:fade .7s}
.view.active{display:block}
h1,h2{color:var(--accent);text-shadow:var(--glow)}
button{
  background:var(--accent);
  border:none;
  padding:12px 26px;
  border-radius:999px;
  box-shadow:var(--glow);
  cursor:pointer;
  margin:10px;
  transition:.3s;
}
button:hover{transform:scale(1.07);box-shadow:0 0 35px var(--accent)}
input{
  padding:12px;
  border-radius:12px;
  border:none;
  margin:8px;
  outline:none;
}

/* ❤️ Heart */
.heart{
  width:120px;height:120px;
  background:var(--accent);
  margin:25px auto;
  transform:rotate(-45deg);
  animation:pulse 1.5s infinite;
}
.heart:before,.heart:after{
  content:"";
  width:120px;height:120px;
  background:var(--accent);
  border-radius:50%;
  position:absolute;
}
.heart:before{top:-60px}
.heart:after{left:60px}

/* 🎮 GAME */
.board{
  display:grid;
  grid-template-columns:repeat(3,90px);
  gap:14px;
  justify-content:center;
  margin:20px auto;
}
.cell{
  width:90px;height:90px;
  background:rgba(255,255,255,.08);
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:2.4rem;
  border-radius:16px;
  cursor:pointer;
  border:3px solid var(--accent);
  box-shadow:0 0 18px rgba(255,95,162,.6);
  transition:.25s;
}
.cell:hover{
  background:rgba(255,95,162,.15);
  box-shadow:0 0 30px var(--accent);
}

/* ✨ Glow Text */
.glow{
  font-size:1.3rem;
  text-shadow:0 0 10px var(--accent),0 0 25px var(--accent);
  transition:.4s;
}
.glow:hover{
  text-shadow:0 0 30px #fff,0 0 45px var(--accent);
  transform:scale(1.04);
}

/* 😈 Not Button */
#notBtn{
  position:relative;
}
#notBtn:hover{
  position:absolute;
  left:Math.random()*60+"%";
  top:Math.random()*60+"%";
}

/* ❤️ Floating Hearts */
.float-heart{
  position:fixed;
  bottom:0;
  font-size:22px;
  animation:float 3s linear forwards;
}

@keyframes pulse{50%{transform:rotate(-45deg) scale(1.1)}}
@keyframes fade{from{opacity:0;transform:translateY(10px)}}
@keyframes float{to{transform:translateY(-120vh);opacity:0}}
</style>
</head>

<body>

<audio id="bgm" loop>
  <source src="https://assets.mixkit.co/music/preview/mixkit-romantic-love-126.mp3">
</audio>

<!-- PASSWORD -->
<section class="view active" id="pass">
  <h1>Welcome My Love ❤️</h1>
  <div class="heart"></div>
  <p>Enter Secret Password 🔐</p>
  <input id="pwd" type="password" autocomplete="off">
  <br>
  <input id="name" placeholder="Your Name 💕">
  <br>
  <button onclick="unlock()">Enter</button>
</section>

<!-- QUESTION -->
<section class="view" id="question">
  <h2>Do you love me? 😘</h2>
  <button onclick="show('game')">Yes ❤️</button>
  <button id="notBtn">Not 😜</button>
</section>

<!-- GAME -->
<section class="view" id="game">
  <h2>Tic Tac Toe 💕</h2>
  <div class="board">
    <div class="cell" onclick="move(0)"></div>
    <div class="cell" onclick="move(1)"></div>
    <div class="cell" onclick="move(2)"></div>
    <div class="cell" onclick="move(3)"></div>
    <div class="cell" onclick="move(4)"></div>
    <div class="cell" onclick="move(5)"></div>
    <div class="cell" onclick="move(6)"></div>
    <div class="cell" onclick="move(7)"></div>
    <div class="cell" onclick="move(8)"></div>
  </div>
  <p id="status"></p>
</section>

<!-- SHAYARI -->
<section class="view" id="shayari">
  <h2>For You ❤️</h2>
  <p id="shayariText" class="glow"></p>
  <button onclick="show('wish')">Next 💖</button>
</section>

<!-- WISH -->
<section class="view" id="wish">
  <h2 id="toName"></h2>
  <p id="wishText" class="glow"></p>
  <button onclick="celebrate()">Celebrate 🎉</button>
</section>

<script>
const views=document.querySelectorAll('.view');
const board=Array(9).fill("");
let over=false;
let userName="Love";

const shayariMsg=`Tum meri har dua mein ho,
Tum meri har saans mein ho,
Tum bina kahe hi samajh jao,
Itna pyar meri har baat mein ho ❤️`;

const wishMsg=`I don’t promise perfect days,
but I promise a forever heart.

Tum meri zindagi ho ❤️`;

function show(id){
  views.forEach(v=>v.classList.remove("active"));
  document.getElementById(id).classList.add("active");
  if(id==="shayari") typeText("shayariText",shayariMsg);
  if(id==="wish"){
    document.getElementById("toName").innerText=userName+" 💕";
    typeText("wishText",wishMsg);
  }
}

function unlock(){
  if(pwd.value==="2418"){
    userName=name.value||"My Love";
    document.getElementById("bgm").play();
    show("question");
  }else{
    alert("Wrong password 💔");
    pwd.value="";
  }
}

/* GAME */
function move(i){
  if(board[i]||over) return;
  board[i]="X";
  draw();
  if(win("X")) return end("You Win ❤️");
  setTimeout(ai,400);
}
function ai(){
  let e=board.map((v,i)=>v===""?i:null).filter(v=>v!==null);
  if(!e.length){end("Draw");return;}
  board[e[Math.floor(Math.random()*e.length)]]="O";
  draw();
}
function win(p){
  const w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
  return w.some(a=>a.every(i=>board[i]===p));
}
function end(msg){
  status.innerText=msg;
  over=true;
  setTimeout(()=>show("shayari"),1200);
}
function draw(){
  document.querySelectorAll(".cell").forEach((c,i)=>c.textContent=board[i]);
}

/* ✨ Typing Effect */
function typeText(id,text){
  let el=document.getElementById(id);
  el.textContent="";
  let i=0;
  let t=setInterval(()=>{
    el.textContent+=text[i];
    i++;
    if(i>=text.length) clearInterval(t);
  },40);
}

/* ❤️ Celebration */
function celebrate(){
  for(let i=0;i<35;i++){
    let h=document.createElement("div");
    h.className="float-heart";
    h.innerText="❤️";
    h.style.left=Math.random()*100+"vw";
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),3000);
  }
}
</script>

</body>
</html>
