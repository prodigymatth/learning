<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>onclu</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',sans-serif; }

body {
  min-height:100vh;
  background: linear-gradient(rgba(30,0,70,0.7), rgba(10,0,30,0.9)),
              url('https://media.gettyimages.com/id/881752658/video/journey-through-galaxy.jpg?s=640x640&k=20&c=ITfk5mu21pnyUjb7tTndTm8LMBqpPS4YBMY2Il_nGyQ=') no-repeat center center fixed;
  background-size:cover;
  color:white;
  overflow-x:hidden;
  position:relative;
}

/* Particle effect */
body::before {
  content:"";
  position:fixed; inset:0;
  background: radial-gradient(#fff 1px, transparent 1px);
  background-size:3px 3px;
  pointer-events:none;
  animation: twinkle 6s linear infinite;
  opacity:0.3;
}
@keyframes twinkle { 0%,100%{transform:translate(0,0);} 50%{transform:translate(1px,1px);} }

/* Loader */
#loader {
  position:fixed; inset:0; left:-100%;
  background:linear-gradient(90deg,#2e0255,#5a00a5);
  z-index:15; display:flex; align-items:center; justify-content:center;
  font-size:36px; letter-spacing:6px; font-weight:bold;
  color:#e0c0ff; text-shadow: 0 0 35px #b16eff, 0 0 70px #d18fff;
  transition: left 0.6s ease;
}
#loader.active { left:0; }

/* Home Screen */
.container {
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  min-height:100vh; padding:80px 20px; text-align:center;
}
h1 {
  font-size:72px; letter-spacing:5px; margin-bottom:50px;
  text-shadow:0 0 35px #a855f7, 0 0 70px #d18fff;
}
.buttonContainer {
  display:flex; flex-direction:column; gap:12px; width:280px;
}
button.gameBtn {
  padding:16px; font-size:17px; font-weight:500;
  background:rgba(60,0,100,0.2);
  color:white; border:1px solid rgba(200,150,255,0.3);
  border-radius:10px; cursor:pointer; transition:all 0.3s;
}
button.gameBtn:hover {
  background:rgba(120,0,180,0.4);
  transform:translateY(-4px);
  box-shadow:0 0 25px #d18fff;
}

#homeBtn {
  position:fixed; top:15px; left:15px; padding:8px 14px;
  font-size:14px; background:rgba(255,255,255,0.1);
  border:1px solid rgba(255,255,255,0.2); border-radius:6px;
  color:#ddd; cursor:pointer; display:none; z-index:20;
}
#homeBtn:hover { background:rgba(200,150,255,0.3); color:white; }

/* More content */
.more-content {
  margin-top:200px; text-align:center; padding-bottom:100px;
  opacity:0; transform:translateY(60px); transition:1s ease;
}
.more-content.visible { opacity:1; transform:translateY(0); }

/* Iframes */
iframe, embed {
  position:fixed; inset:0; width:100%; height:100vh;
  border:none; display:none; z-index:5;
}
</style>
</head>
<body>

<div id="loader">onclu</div>
<button id="homeBtn" onclick="goHome()">← Home</button>

<div class="container" id="homeScreen">
  <h1>onclu</h1>
  <div class="buttonContainer">
    <button class="gameBtn" onclick="openGame('hoodaFrame')">HoodaMath</button>
    <button class="gameBtn" onclick="openGame('playFrame')">Playtropolis</button>
    <button class="gameBtn" onclick="openGame('gFrame')">GHub</button>
    <button class="gameBtn" onclick="openGame('minecraftFrame')">Minecraft</button>
    <button class="gameBtn" onclick="openGame('infiniteFrame')">Infinite Craft</button>
    <button class="gameBtn" onclick="openGame('soundboardFrame')">Soundboard</button>
    <button class="gameBtn" onclick="openGame('mathFrame')">Coolmath Games</button>
    <button class="gameBtn" onclick="openGame('cheeseFrame')">Stan The Cheese Man</button>
    <button class="gameBtn" onclick="openGame('basketFrame')">Basket Random</button>
    <button class="gameBtn" onclick="openGame('buildnowFrame')">Build Now GG</button>
    <button class="gameBtn" onclick="openGame('hahaFrame')">Haha Games</button>
    <button class="gameBtn" onclick="openGame('gamaFrame')">Play Gama</button>
    <button class="gameBtn" onclick="openGame('agentFrame')">For Khalil</button>
  </div>
</div>

<div class="more-content" id="moreContent">
  <h2>I might add more features</h2>
  <p>Gimme ideas!</p>
</div>

<!-- Game Frames -->
<iframe id="hoodaFrame" src="https://www.hoodamath.com/" allowfullscreen></iframe>
<iframe id="playFrame" src="https://www.playtropolis.com" allowfullscreen></iframe>
<iframe id="gFrame" src="https://ghub-light.neocities.org/" allowfullscreen></iframe>
<iframe id="minecraftFrame" src="https://eaglercraft.com/" allowfullscreen></iframe>
<embed id="infiniteFrame" src="https://infinite-craft.org/infinite-craft/" allowfullscreen></embed>
<iframe id="soundboardFrame" src="https://www.myinstants.com/en/index/us/" allowfullscreen></iframe>
<iframe id="mathFrame" src="https://www.coolmathgames.com/" allowfullscreen></iframe>
<iframe id="cheeseFrame" src="https://stanthecheeseman.github.io/" allowfullscreen></iframe>
<iframe id="basketFrame" src="https://www.twoplayergames.org/game/basket-random" allowfullscreen></iframe>
<iframe id="buildnowFrame" src="https://buildnow-gg.io/" allowfullscreen></iframe>
<iframe id="hahaFrame" src="https://www.hahagames.com/" allowfullscreen></iframe>
<iframe id="gamaFrame" src="https://playgama.com" allowfullscreen></iframe>
<iframe id="agentFrame" src="https://www.twoplayergames.org/game/agent-walker-vs-skibidi-toilets" allowfullscreen></iframe>

<script>
// Variables
const loader = document.getElementById("loader");
const homeScreen = document.getElementById("homeScreen");
const homeBtn = document.getElementById("homeBtn");
const moreContent = document.getElementById("moreContent");

// Hide all games
function hideAll() {
  document.querySelectorAll("iframe, embed").forEach(el => el.style.display = "none");
}

// Open game
function openGame(id) {
  loader.classList.add("active");
  
  setTimeout(() => {
    homeScreen.style.display = "none";
    hideAll();
    document.getElementById(id).style.display = "block";
    homeBtn.style.display = "block";
    loader.classList.remove("active");
  }, 600);
}

// Go back home
function goHome() {
  hideAll();
  homeScreen.style.display = "flex";
  homeBtn.style.display = "none";
}

// Show "more content" when scrolling
window.addEventListener('scroll', () => {
  if (window.scrollY + window.innerHeight > moreContent.offsetTop - 100) {
    moreContent.classList.add('visible');
  }
});
</script>
</body>
</html>
