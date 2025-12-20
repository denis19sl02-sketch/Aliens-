<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Aliens: Space Defense</title>
    <style>
        body { margin: 0; background: #000; overflow: hidden; font-family: 'Arial Black', sans-serif; user-select: none; touch-action: none; color: white; }
        canvas { display: block; position: absolute; top: 0; left: 0; z-index: 1; }
        .screen { position: absolute; top: 0; left: 0; width: 100%; height: 100%; display: flex; flex-direction: column; align-items: center; justify-content: center; z-index: 100; background: rgba(0,0,0,0.4); }
        #ui { position: absolute; top: 15px; width: 100%; display: flex; justify-content: space-around; font-size: 18px; z-index: 10; pointer-events: none; display: none; }
        h1 { font-size: 60px; text-shadow: 0 0 30px #0f0; margin-bottom: 20px; text-align: center; color: #0f0; letter-spacing: 5px; }
        button { padding: 15px 40px; font-size: 22px; border-radius: 50px; cursor: pointer; font-weight: bold; border: 4px solid #fff; transition: 0.2s; background: #222; color: #fff; margin: 8px; z-index: 110; }
        #playBtn { background: #00ff00; color: #000; font-size: 35px; padding: 20px 70px; border-color: #000; }
        .lvl-card { background: rgba(34, 34, 34, 0.8); border: 2px solid #555; padding: 12px; margin: 5px; width: 75%; border-radius: 15px; text-align: center; cursor: pointer; transition: 0.2s; }
        .lvl-card.active { border-color: #0f0; box-shadow: 0 0 15px #0f0; background: rgba(0, 50, 0, 0.8); }
        #joyContainer { position: absolute; bottom: 40px; left: 40px; width: 120px; height: 120px; background: rgba(255,255,255,0.1); border: 2px solid #fff; border-radius: 50%; z-index: 50; display: none; }
        #joyStick { position: absolute; top: 35px; left: 35px; width: 50px; height: 50px; background: #fff; border-radius: 50%; }
        #fireButton { position: absolute; bottom: 40px; right: 40px; width: 110px; height: 110px; background: #ff0000; border: 5px solid #fff; border-radius: 50%; display: none; align-items: center; justify-content: center; font-weight: bold; z-index: 50; }
    </style>
</head>
<body onclick="initAudio()">

<div id="ui">
    <div>❤️ HP: <span id="hp">45</span></div>
    <div style="color: #0ff;">⏱️ ARRIVAL: <span id="timer">00:50</span></div>
    <div>🛸 SCORE: <span id="score">0</span></div>
</div>

<div id="mainMenu" class="screen">
    <h1>ALIENS</h1>
    <button id="playBtn">PLAY</button>
    <button id="levelsBtn" style="background: #0088ff;">LEVELS</button>
    <p id="currentLvlInfo" style="color: #0f0; margin-top: 15px; font-size: 14px;">Selected: Level 0 (50 Sec)</p>
</div>

<div id="levelsMenu" class="screen" style="display: none;">
    <h1 style="font-size: 40px;">SELECT MISSION</h1>
    <div class="lvl-card" id="lc0" onclick="selectLevel(0)"><h3>LEVEL 0</h3><p>Time: 50 Sec | Tutorial</p></div>
    <div class="lvl-card" id="lc1" onclick="selectLevel(1)"><h3>LEVEL 1</h3><p>Time: 3 Min | Easy</p></div>
    <div class="lvl-card" id="lc2" onclick="selectLevel(2)"><h3>LEVEL 2</h3><p>Time: 6 Min | Medium</p></div>
    <div class="lvl-card" id="lc3" onclick="selectLevel(3)"><h3>LEVEL 3</h3><p>Time: 10 Min | Hard</p></div>
    <button onclick="backToMain()">BACK</button>
</div>

<div id="gameOver" class="screen" style="display: none; background: rgba(100,0,0,0.8);">
    <h1 style="color: #fff; text-shadow: none;">ROCKET DESTROYED!</h1>
    <button onclick="resetToMenu()">GO TO MAIN PAGE</button>
</div>

<div id="victoryScreen" class="screen" style="display: none; background: rgba(0,100,0,0.8);">
    <h1 style="color: #fff; text-shadow: none;">MISSION SUCCESS!</h1>
    <button onclick="resetToMenu()">GO TO MAIN PAGE</button>
</div>

<div id="joyContainer"><div id="joyStick"></div></div>
<div id="fireButton">FIRE</div>
<canvas id="gameCanvas"></canvas>

<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let audioCtx = null;
function initAudio() { if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)(); if (audioCtx.state === 'suspended') audioCtx.resume(); }

function playSnd(freq, type, duration, vol, rampFreq) {
    if (!audioCtx) return;
    const osc = audioCtx.createOscillator(); const gain = audioCtx.createGain();
    osc.type = type; osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
    if (rampFreq) osc.frequency.exponentialRampToValueAtTime(rampFreq, audioCtx.currentTime + duration);
    gain.gain.setValueAtTime(vol, audioCtx.currentTime); gain.gain.linearRampToValueAtTime(0, audioCtx.currentTime + duration);
    osc.connect(gain); gain.connect(audioCtx.destination); osc.start(); osc.stop(audioCtx.currentTime + duration);
}

// --- СОСТОЯНИЕ ИГРЫ ---
let gameState = "MAIN_MENU"; 
let defaultTime = 50; 
let timeLeft = 50;
let spawnRate = 0.03;
let stationY = canvas.height - 110;
let planetY = canvas.height - 80;
let goalPlanet = { y: -700, radius: 400, active: false };
let player = { x: canvas.width / 2, y: canvas.height - 150, hp: 45, score: 0 };
let moveX = 0, isHoldingFire = false, fireCooldown = 0;
let enemies = [], bullets = [], enemyBullets = [], stars = [];

for(let i=0; i<100; i++) stars.push({x: Math.random()*canvas.width, y: Math.random()*canvas.height, s: Math.random()*3+1});

function selectLevel(num) {
    playSnd(440, 'sine', 0.1, 0.1, 880);
    if(num === 0) { defaultTime = 50; spawnRate = 0.025; }
    if(num === 1) { defaultTime = 180; spawnRate = 0.035; }
    if(num === 2) { defaultTime = 360; spawnRate = 0.05; }
    if(num === 3) { defaultTime = 600; spawnRate = 0.07; }
    timeLeft = defaultTime;
    document.getElementById("currentLvlInfo").innerText = `Selected: Level ${num} (${num === 0 ? '50 Sec' : (defaultTime/60) + ' Min'})`;
    document.querySelectorAll('.lvl-card').forEach(c => c.classList.remove('active'));
    document.getElementById('lc'+num).classList.add('active');
}

function resetToMenu() {
    gameState = "MAIN_MENU";
    player.hp = 45; player.score = 0;
    player.x = canvas.width / 2;
    timeLeft = defaultTime;
    enemies = []; bullets = []; enemyBullets = [];
    goalPlanet.active = false; goalPlanet.y = -700;
    stationY = canvas.height - 110; planetY = canvas.height - 80;
    
    document.getElementById("hp").innerText = player.hp;
    document.getElementById("score").innerText = player.score;
    document.getElementById("gameOver").style.display = "none";
    document.getElementById("victoryScreen").style.display = "none";
    document.getElementById("ui").style.display = "none";
    document.getElementById("joyContainer").style.display = "none";
    document.getElementById("fireButton").style.display = "none";
    document.getElementById("mainMenu").style.display = "flex";
    playSnd(200, 'sine', 0.2, 0.1, 50);
}

function backToMain() { 
    playSnd(200, 'sine', 0.1, 0.1, 50);
    document.getElementById("levelsMenu").style.display = "none"; 
    document.getElementById("mainMenu").style.display = "flex"; 
}

document.getElementById("levelsBtn").onclick = () => { 
    playSnd(600, 'sine', 0.1, 0.1, 300);
    document.getElementById("mainMenu").style.display = "none"; 
    document.getElementById("levelsMenu").style.display = "flex"; 
};

document.getElementById("playBtn").onclick = () => {
    initAudio();
    document.getElementById("mainMenu").style.display = "none";
    document.getElementById("ui").style.display = "flex";
    document.getElementById("joyContainer").style.display = "block";
    document.getElementById("fireButton").style.display = "flex";
    
    let m = Math.floor(timeLeft/60); let s = timeLeft%60;
    document.getElementById("timer").innerText = `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    
    gameState = "LAUNCHING";
    playSnd(50, 'sawtooth', 2.0, 0.4, 400);
};

// Управление
const fireBtn = document.getElementById("fireButton");
fireBtn.addEventListener("touchstart", (e) => { e.preventDefault(); isHoldingFire = true; });
window.addEventListener("touchend", () => { isHoldingFire = false; });

window.addEventListener("touchmove", (e) => {
    if (gameState !== "GAME") return;
    for (let t of e.touches) {
        if (t.clientX < 250) {
            let rect = document.getElementById("joyContainer").getBoundingClientRect();
            moveX = Math.min(Math.max((t.clientX - (rect.left + 60))/50, -1), 1);
            document.getElementById("joyStick").style.transform = `translateX(${moveX*40}px)`;
        }
    }
}, {passive: false});

setInterval(() => {
    if (gameState === "GAME" && timeLeft > 0) {
        timeLeft--;
        let m = Math.floor(timeLeft/60); let s = timeLeft%60;
        document.getElementById("timer").innerText = `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
        if (timeLeft === 0) goalPlanet.active = true;
    }
}, 1000);

function update() {
    stars.forEach(s => {
        let speed = (gameState === "GAME" || gameState === "LAUNCHING") ? s.s * 3 : s.s;
        s.y += speed;
        if(s.y > canvas.height) { s.y = -10; s.x = Math.random()*canvas.width; }
    });

    if (gameState === "LAUNCHING") {
        stationY += 15; planetY += 15;
        if (stationY > canvas.height + 250) gameState = "GAME";
    }

    if (gameState === "GAME") {
        player.x += moveX * 12;
        player.x = Math.max(40, Math.min(canvas.width-40, player.x));
        if (isHoldingFire && --fireCooldown <= 0) {
            playSnd(1500, 'square', 0.06, 0.03, 400);
            for(let i = 0; i < 12; i++) {
                let a = (i / 12) * Math.PI * 2;
                bullets.push({ x: player.x, y: player.y, vx: Math.cos(a) * 16, vy: Math.sin(a) * 16 });
            }
            fireCooldown = 8;
        }
        if (goalPlanet.active) {
            goalPlanet.y += 2.5;
            if (player.y - goalPlanet.y < goalPlanet.radius) {
                gameState = "VICTORY";
                playSnd(300, 'sine', 2.5, 0.5, 1200);
                document.getElementById("victoryScreen").style.display = "flex";
            }
        }
    }

    if (player.hp <= 0 && gameState === "GAME") {
        gameState = "DEAD";
        playSnd(60, 'sawtooth', 1.5, 0.7, 10);
        document.getElementById("gameOver").style.display = "flex";
    }

    bullets.forEach((b, i) => { b.x += b.vx; b.y += b.vy; if(b.y < -100 || b.y > canvas.height+100) bullets.splice(i,1); });
    enemyBullets.forEach((eb, i) => {
        eb.x += eb.vx; eb.y += eb.vy;
        if (Math.hypot(eb.x-player.x, eb.y-player.y) < 28 && gameState === "GAME") {
            player.hp -= 2; enemyBullets.splice(i,1);
            document.getElementById("hp").innerText = Math.max(0, player.hp);
            playSnd(120, 'triangle', 0.15, 0.3, 40);
        }
    });

    if (gameState === "GAME" && Math.random() < spawnRate && !goalPlanet.active) {
        let newX = Math.random() * (canvas.width - 100) + 50;
        let isSafe = true;
        enemies.forEach(en => { if(Math.abs(en.x - newX) < 120) isSafe = false; });
        if(isSafe) enemies.push({x: newX, y: -60, hp: 12, shoot: 0});
    }

    enemies.forEach((en, i) => {
        en.y += 3.5; en.shoot++;
        if (en.shoot > 70 && en.y < player.y - 100) {
            [-3, 0, 3].forEach(vx => enemyBullets.push({x: en.x, y: en.y, vx: vx, vy: 7}));
            en.shoot = 0;
        }
        bullets.forEach((b, bi) => {
            if (Math.hypot(en.x-b.x, en.y-b.y) < 45) {
                en.hp -= 4; bullets.splice(bi,1);
                if (en.hp <= 0) { 
                    playSnd(180, 'sawtooth', 0.2, 0.2, 60);
                    enemies.splice(i,1); player.score++; 
                    document.getElementById("score").innerText = player.score; 
                }
            }
        });
        if(en.y > canvas.height + 100) enemies.splice(i,1);
    });
}

function draw() {
    ctx.fillStyle = "#000"; ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "#fff"; stars.forEach(s => ctx.fillRect(s.x, s.y, s.s, s.s));
    
    if (gameState === "LAUNCHING" || stationY < canvas.height + 150) {
        ctx.fillStyle = "#333"; ctx.fillRect(0, planetY, canvas.width, 400);
        ctx.fillStyle = "#111"; ctx.fillRect(canvas.width/2-80, stationY, 160, 40);
    }
    
    if (goalPlanet.active) {
        let g = ctx.createRadialGradient(canvas.width/2, goalPlanet.y, 50, canvas.width/2, goalPlanet.y, goalPlanet.radius);
        g.addColorStop(0, "#f0f"); g.addColorStop(0.5, "#0ff"); g.addColorStop(1, "#ff0");
        ctx.fillStyle = g; ctx.beginPath(); ctx.arc(canvas.width/2, goalPlanet.y, goalPlanet.radius, 0, 7); ctx.fill();
    }
    
    enemies.forEach(en => {
        ctx.fillStyle = "#0f0"; ctx.beginPath(); ctx.arc(en.x, en.y-10, 15, 0, 7); ctx.fill();
        ctx.fillStyle = "#888"; ctx.beginPath(); ctx.ellipse(en.x, en.y, 42, 16, 0, 0, 7); ctx.fill();
    });
    
    bullets.forEach(b => { ctx.fillStyle = "#fff"; ctx.beginPath(); ctx.arc(b.x, b.y, 5, 0, 7); ctx.fill(); });
    enemyBullets.forEach(eb => { ctx.fillStyle = "#f0f"; ctx.beginPath(); ctx.arc(eb.x, eb.y, 8, 0, 7); ctx.fill(); });

    if (gameState === "LAUNCHING" || gameState === "GAME") {
        ctx.save(); ctx.translate(player.x, player.y);
        let fH = 35 + Math.random() * 25;
        let g = ctx.createLinearGradient(0, 35, 0, 35 + fH); g.addColorStop(0, "yellow"); g.addColorStop(1, "transparent");
        ctx.fillStyle = g; ctx.beginPath(); ctx.moveTo(-12, 35); ctx.lineTo(0, 35 + fH); ctx.lineTo(12, 35); ctx.fill();
        ctx.fillStyle = "white"; ctx.beginPath(); ctx.moveTo(0,-60); ctx.lineTo(25,35); ctx.lineTo(-25,35); ctx.fill();
        ctx.fillStyle = "red"; ctx.fillRect(-30, 10, 12, 35); ctx.fillRect(18, 10, 12, 35);
        ctx.fillStyle = "cyan"; ctx.beginPath(); ctx.arc(0, -10, 8, 0, 7); ctx.fill();
        ctx.restore();
    }
    update(); requestAnimationFrame(draw);
}
draw();
selectLevel(0);
</script>
</body>
</html>
