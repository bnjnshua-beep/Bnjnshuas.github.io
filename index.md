<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Balentayms</title>

<style>
body {
    margin: 0;
    font-family: 'Sylfaen', cursive;
    background: radial-gradient(circle at top, #ff5f6d, #00008B);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow: hidden;
}

.card {
    background: white;
    width: 94%;
    max-width: 360px;
    padding: 18px;
    border-radius: 25px;
    box-shadow: 0 20px 40px rgba(0,0,0,.35);
    text-align: center;
    position: relative;
}

img {
    width: 100%;
    border-radius: 15px;
}

h1 {
    color: #98002e;
    font-size: 2.0rem;
    margin: 10px 0;
}

.dialogue {
    min-height: 45px;
    font-size: .95rem;
    color: #444;
}

.timer {
    font-size: .85rem;
    color: #ff2f6e;
    margin-top: 4px;
}

.buttons {
    height: 170px;
    margin-top: 15px;
    position: relative;
}

button {
    padding: 12px 22px;
    border-radius: 30px;
    border: none;
    font-size: 1rem;
    cursor: pointer;
    position: absolute;
}

#yes {
    background: #ff2f6e;
    color: white;
    left: 50%;
    bottom: 0;
    transform: translateX(-50%);
    z-index: 10;
}

#no {
    background: #ddd;
    left: 50%;
    top: 0;
    transform: translateX(-50%);
}

.love {
    display: none;
    font-size: 2.0rem;
    color: #98002e;
    font-weight: bold;
}

.credit {
    position: fixed;
    bottom: -100%;
    width: 100%;
    text-align: center;
    font-size: 1rem;
    animation: credits 12s linear forwards;
    background: rgba(0,0,0,0.85);
    color: white;
    padding-top: 50px;
}

@keyframes credits {
    to { bottom: 100%; }
}

.heart {
    position: fixed;
    bottom: -30px;
    font-size: 24px;
    animation: rise 4s linear forwards;
    pointer-events: none;
}

@keyframes rise {
    100% { transform: translateY(-120vh); opacity: 0; }
}

.popup {
    position: fixed;
    top: 35%;
    left: 50%;
    transform: translateX(-50%);
    background: white;
    padding: 15px;
    border-radius: 15px;
    box-shadow: 0 10px 25px rgba(0,0,0,.3);
    z-index: 999;
}

.shake {
    animation: shake 0.3s;
}

@keyframes shake {
    0% { transform: translate(2px, 2px); }
    50% { transform: translate(-2px, -2px); }
    100% { transform: translate(0, 0); }
}
</style>
</head>

<body>

<div class="card" id="card">
    <!-- CHANGE IMAGE HERE -->
    <img src="4M7IWwP.png">

    <h1>Date tayo? o Magdadate tayo?💖</h1>

    <div class="dialogue" id="dialogue">
        Choose wisely
    </div>

    <div class="timer" id="timer">Forced YES in: 12</div>

    <div class="buttons">
        <button id="no">NO 😈</button>
        <button id="yes">YES 💘</button>
    </div>

    <div class="love" id="love">
        💞 Yey!!! Okay! 💞<br>
        Wala ka din naman choice 🥰
    </div>
</div>

<audio id="panic" src="https://www.myinstants.com/media/sounds/windows-error.mp3"></audio>
<audio id="win" src="https://www.myinstants.com/media/sounds/anime-wow-sound-effect.mp3"></audio>

<script>
const noBtn = document.getElementById("no");
const yesBtn = document.getElementById("yes");
const dialogue = document.getElementById("dialogue");
const timerEl = document.getElementById("timer");
const love = document.getElementById("love");
const card = document.getElementById("card");
const panic = document.getElementById("panic");
const win = document.getElementById("win");

let hits = 0;
let timeLeft = 12;

const lines = [
    "Uy wait lang 😅",
    "Sayang effort ko 🥲",
    "May plano na ako😭",
    "JOK😤",
    "Magwalk In na lang tayo.",
    "Sa Orange Bucket",
    "Okay, Tara! HAHAHAHA."
];

function moveNo() {
    hits++;
    panic.play();
    navigator.vibrate?.(150);
    card.classList.add("shake");
    setTimeout(()=>card.classList.remove("shake"),300);

    const maxX = card.clientWidth - noBtn.offsetWidth;
    const maxY = card.clientHeight - noBtn.offsetHeight - 120;

    noBtn.style.left = Math.random()*maxX + "px";
    noBtn.style.top = Math.random()*maxY + "px";
    noBtn.style.transform = `scale(${Math.max(0.35, 1 - hits*0.1)})`;

    dialogue.textContent = lines[Math.min(hits-1, lines.length-1)];
    fakePopup();
}

function fakePopup() {
    const p = document.createElement("div");
    p.className = "popup";
    p.textContent = "⚠️ System Error: NO not supported.";
    document.body.appendChild(p);
    setTimeout(()=>p.remove(),800);
}

noBtn.addEventListener("mouseover", moveNo);
noBtn.addEventListener("touchstart", moveNo);

const countdown = setInterval(()=>{
    timeLeft--;
    timerEl.textContent = "Forced YES in: " + timeLeft;
    if(timeLeft<=0) yesBtn.click();
},1000);

yesBtn.onclick = ()=>{
    clearInterval(countdown);
    noBtn.style.display="none";
    yesBtn.style.display="none";
    timerEl.style.display="none";
    dialogue.style.display="none";
    love.style.display="block";
    win.play();
    hearts();
    credits();
};

function hearts(){
    setInterval(()=>{
        const h=document.createElement("div");
        h.className="heart";
        h.textContent=["💖","👉👌","👅","🍆","🍑","🤫","💗","💘"][Math.floor(Math.random()*8)];
        h.style.left=Math.random()*100+"vw";
        h.style.fontSize=Math.random()*20+20+"px";
        document.body.appendChild(h);
        setTimeout(()=>h.remove(),4000);
    },200);
}

function credits(){
    const c=document.createElement("div");
    c.className="credit";
    c.innerHTML=`
    <h2>🎬 CREDITS 🎬</h2>
    <p>Director: Josh</p>
    <p>Lead Actor: Josh</p>
    <p>Lead Actress: JC 😘</p>
    <p>Budget: Emotional Damage</p>
    <p>Special Thanks: Destiny</p>
    <br><p>Post-credits scene loading…</p>`;
    document.body.appendChild(c);
}
</script>

</body>
</html>
