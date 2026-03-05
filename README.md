<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>easywaystolearn</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',sans-serif; }

/* BODY & BACKGROUND */
body {
  min-height:100vh;
  background: linear-gradient(rgba(30,0,70,0.7), rgba(10,0,30,0.9)),
  url('https://media.gettyimages.com/id/881752658/video/journey-through-galaxy.jpg?s=640x640&k=20&c=ITfk5mu21pnyUjb7tTndTm8LMBqpPS4YBMY2Il_nGyQ=') no-repeat center center fixed;
  background-size:cover;
  color:white;
  overflow-x:hidden;
  scroll-behavior:smooth;
  position:relative;
}

/* PARTICLE EFFECT */
body::before {
  content:"";
  position:fixed; top:0; left:0; width:100%; height:100%;
  background: radial-gradient(#fff 1px, transparent 1px);
  background-size:3px 3px;
  pointer-events:none;
  animation: twinkle 6s linear infinite;
  opacity:0.3;
}
@keyframes twinkle { 0%{transform:translate(0,0);}50%{transform:translate(1px,1px);}100%{transform:translate(0,0);} }

/* PASSWORD SCREEN */
#passwordScreen, #usernameScreen {
  position:fixed; top:0; left:0; width:100%; height:100vh;
  background: rgba(40,0,80,0.95);
  display:flex; justify-content:center; align-items:center;
  z-index:999;
}
.passwordBox, .usernameBox {
  background: rgba(60,0,110,0.95);
  padding:50px 40px;
  border-radius:20px;
  border:2px solid rgba(200,150,255,0.3);
  box-shadow: 0 0 60px rgba(180,80,255,0.5);
  text-align:center;
  width:400px;
  transition: all 0.4s ease;
  animation: fadeInBox 0.6s ease forwards;
}
@keyframes fadeInBox { 0%{transform:scale(0.7);opacity:0;}100%{transform:scale(1);opacity:1;} }

.passwordBox h2, .usernameBox h2 {
  font-size:36px; margin-bottom:25px;
  color:#d5b3ff; letter-spacing:2px;
  text-shadow:0 0 30px #a855f7, 0 0 60px #d18fff;
  animation: glowText 2.5s infinite alternate;
}
@keyframes glowText { from{text-shadow:0 0 25px #b16eff,0 0 50px #d18fff;} to{text-shadow:0 0 45px #d18fff,0 0 70px #f1c0ff;} }

.passwordBox input, .usernameBox input {
  width:100%; padding:16px; font-size:18px;
  border-radius:12px; border:none; margin-bottom:15px;
  outline:none; text-align:center;
  background: rgba(255,255,255,0.05);
  color:white; box-shadow: inset 0 0 10px rgba(0,0,0,0.5);
  transition:0.3s;
}
.passwordBox input:focus, .usernameBox input:focus { background: rgba(255,255,255,0.12); }

.passwordBox button, .usernameBox button {
  width:100%; padding:16px; font-size:18px; font-weight:bold;
  border:none; border-radius:12px;
  background: linear-gradient(45deg, #a855f7, #7c3aed);
  color:white; cursor:pointer;
  box-shadow: 0 0 30px rgba(168,85,247,0.7);
  transition:0.3s;
}
.passwordBox button:hover, .usernameBox button:hover {
  transform: scale(1.05);
  box-shadow: 0 0 50px rgba(200,120,255,0.9);
}

#hintText, #attemptCounter, #usernameHint {
  margin-top:12px; font-size:14px; min-height:20px;
  color:#caaeff; opacity:0; transition:0.5s;
}

/* LOADER */
#loader {
  position:fixed; top:0; left:-100%; width:100%; height:100%;
  background:linear-gradient(90deg,#2e0255,#5a00a5);
  z-index:15; display:flex; align-items:center; justify-content:center;
  font-size:36px; letter-spacing:6px; color:#e0c0ff; font-weight:bold;
  text-shadow: 0 0 35px #b16eff, 0 0 70px #d18fff;
  animation: pulseLoader 2s infinite alternate;
}
#loader.active { left:0; }
@keyframes pulseLoader { 0% { text-shadow:0 0 35px #b16eff,0 0 70px #d18fff;} 100% { text-shadow:0 0 50px #d18fff,0 0 90px #f1c0ff;} }

/* HOME SCREEN */
.fade-start { opacity:0; transform: translateY(40px); animation: fadeSlide 1.2s ease forwards; }
@keyframes fadeSlide { to { opacity:1; transform: translateY(0); } }
.container { display:flex; flex-direction:column; align-items:center; justify-content:center; padding-top:80px; text-align:center; }
h1 { font-size:72px; letter-spacing:5px; margin-bottom:50px; text-shadow:0 0 35px #a855f7, 0 0 70px #d18fff;}
.buttonContainer { display:flex; flex-direction:column; gap:15px; width:280px; }
button.gameBtn { padding:15px; font-size:17px; background: rgba(60,0,100,0.15); color:white; border:1px solid rgba(200,150,255,0.3); border-radius:8px; cursor:pointer; transition:0.3s; }
button.gameBtn:hover { background: rgba(120,0,180,0.3); transform:translateY(-3px); box-shadow:0 0 25px #d18fff;}

#homeBtn { position:fixed; top:15px; left:15px; padding:6px 10px; font-size:13px; background:rgba(255,255,255,0.08); border:1px solid rgba(0,0,0,0.2); border-radius:4px; color:#ccc; cursor:pointer; display:none; z-index:20; transition:0.3s;}
#homeBtn:hover { background:rgba(200,150,255,0.25); color:white; }

/* BOTTOM BUTTONS */
#bottomButtons { position:fixed; bottom:15px; left:50%; transform:translateX(-50%); display:flex; gap:15px; z-index:20; }
#bottomButtons button { padding:10px 14px; font-size:14px; border:none; border-radius:6px; cursor:pointer; background: rgba(100,0,200,0.5); color:white; }
#bottomButtons button:hover { background: rgba(140,0,250,0.7); }

/* DEV CONSOLE */
#devConsole { position:fixed; bottom:60px; right:15px; background:rgba(20,0,60,0.95); padding:15px; border-radius:10px; border:1px solid rgba(150,100,255,0.3); color:white; display:none; z-index:30; width:300px; }
#devConsole input { width:100%; padding:6px; margin-top:5px; border-radius:6px; border:none; outline:none; }
#devConsole button { margin-top:5px; padding:6px 10px; border:none; border-radius:6px; background:#7c3aed; color:white; cursor:pointer; }

iframe, embed { position:fixed; top:0; left:0; width:100%; height:100vh; border:none; display:none; z-index:5; }

/* AUDIO */
audio { display:none; }
</style>
</head>
<body>

<!-- PASSWORD SCREEN -->
<div id="passwordScreen">
  <div class="passwordBox">
    <h2>Access Required</h2>
    <input type="password" id="passwordInput" placeholder="Enter Password">
    <button onclick="checkPassword()">Enter</button>
    <div id="hintText"></div>
    <div id="attemptCounter">Attempts: 0</div>
  </div>
</div>

<!-- USERNAME SCREEN -->
<div id="usernameScreen" style="display:none;">
  <div class="usernameBox">
    <h2>Enter Username</h2>
    <input type="text" id="usernameInput" placeholder="Your username">
    <button onclick="setUsername()">Join</button>
    <div id="usernameHint"></div>
  </div>
</div>

<div id="loader">onclu</div>
<button id="homeBtn" onclick="goHome()">home</button>

<div class="container fade-start" id="homeScreen" style="display:none;">
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
    <button class="gameBtn" onclick="openGame('twoplayFrame')">Two Player Games</button>
  </div>
</div>

<!-- BOTTOM BUTTONS -->
<div id="bottomButtons">
  <button onclick="toggleDev()">Dev Only</button>
  <button onclick="showActivePlayers()">Active Players</button>
</div>

<!-- DEV CONSOLE -->
<div id="devConsole">
  <strong>Dev Console</strong>
  <div>Password: <input type="password" id="devPassword" placeholder="Enter Dev Password"></div>
  <button onclick="loginDev()">Login</button>
  <div id="devActions" style="display:none;">
    <input type="text" id="banUserInput" placeholder="Username to ban">
    <button onclick="banUser()">Ban User</button>
  </div>
</div>

<iframe id="hoodaFrame" src="https://www.hoodamath.com/" allowfullscreen></iframe>
<iframe id="playFrame" src="https://www.playtropolis.com" allowfullscreen></iframe>
<iframe id="gFrame" src="https://ghub-light.neocities.org/" allowfullscreen></iframe>
<iframe id="minecraftFrame" src="https://eaglercraft.com/" allowfullscreen></iframe>
<embed id="infiniteFrame" src="https://infinite-craft.org/infinite-craft/" width="100%" height="100%" style="display:none;" allowfullscreen>
<iframe id="soundboardFrame" src="https://www.myinstants.com/en/index/us/" allowfullscreen></iframe>
<iframe id="mathFrame" src="https://www.coolmathgames.com/" allowfullscreen></iframe>
<iframe id="cheeseFrame" src="https://stanthecheeseman.github.io/" allowfullscreen></iframe>
<iframe id="twoplayFrame" src="https://www.twoplayergames.org" allowfullscreen></iframe>

<!-- AUDIO -->
<audio id="buzzer" src="https://www.soundjay.com/button/sounds/button-10.mp3"></audio>
<audio id="ding" src="https://www.soundjay.com/button/sounds/button-3.mp3"></audio>
<audio id="lofi" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

<script>
let attempts = 0;
const correctPassword = "goldy";
const bannedUsers = JSON.parse(localStorage.getItem("bannedUsers")||"[]");
let onlineUsers = JSON.parse(localStorage.getItem("onlineUsers")||"[]");
let currentUsername = localStorage.getItem("currentUser")||"";

const badWords = ["badword1","badword2","badword3"]; // add more here

const buzzer = document.getElementById("buzzer");
const ding = document.getElementById("ding");
const lofi = document.getElementById("lofi");
const screen = document.getElementById("passwordScreen");
const box = document.querySelector(".passwordBox");
const loaderEl = document.getElementById("loader");
const usernameScreen = document.getElementById("usernameScreen");
const onlineList = document.createElement("ul");

const hints = [
  "Hint 1: 5 letters",
  "Hint 2: Starts with 'g'",
  "Hint 3: Ends with 'y'",
  "Hint 4: Think shiny metal 😉",
  "Hint 5: It's a nickname for treasure",
  "Hint 6: Common in RPGs",
  "Hint 7: Short and catchy",
  "Hint 8: Often golden in color",
  "Hint 9: Legendary and valuable",
  "Hint 10: The password itself is goldy"
];

function fadeOutAudio(audio,duration=1000){
  const step = 0.05;
  const interval = duration*step/audio.volume;
  const fade = setInterval(()=>{
    if(audio.volume>0.05) audio.volume-=step;
    else { audio.pause(); audio.volume=0.2; clearInterval(fade);}
  },interval);
}

function checkPassword(){
  const entered = document.getElementById("passwordInput").value;
  const hint = document.getElementById("hintText");
  const counter = document.getElementById("attemptCounter");
  if(entered === correctPassword){
    ding.play();
    screen.classList.add("flash-green");
    box.style.animation = "upDown 0.5s";
    loaderEl.classList.add("active");
    setTimeout(()=>{
      screen.style.display="none";
      usernameScreen.style.display="flex";
      loaderEl.classList.remove("active");
      screen.classList.remove("flash-green");
      box.style.animation = "";
    },2500);
  } else {
    attempts++;
    counter.innerText = "Attempts: " + attempts;
    if(attempts<=hints.length) hint.innerText = hints[attempts-1];
    else if(attempts>=50){ hint.innerText = "Password: goldy"; }
    hint.style.opacity=1;
    screen.classList.add("flash-red");
    box.style.animation = "shake 0.5s";
    buzzer.play();
    setTimeout(()=>{ screen.classList.remove("flash-red"); box.style.animation="";},500);
  }
}

document.getElementById("passwordInput").addEventListener("keypress", e=>{ if(e.key==="Enter") checkPassword(); });

function setUsername(){
  const input = document.getElementById("usernameInput");
  const hint = document.getElementById("usernameHint");
  const name = input.value.trim();
  if(name.length<3){ hint.innerText="Username too short"; hint.style.opacity=1; return; }
  if(badWords.some(word => name.toLowerCase().includes(word))){ hint.innerText="Bad username detected"; hint.style.opacity=1; return; }
  if(bannedUsers.includes(name)){ hint.innerText="You are banned"; hint.style.opacity=1; return; }

  currentUsername = name;
  if(!onlineUsers.includes(name)) onlineUsers.push(name);
  localStorage.setItem("currentUser", name);
  localStorage.setItem("onlineUsers", JSON.stringify(onlineUsers));

  usernameScreen.style.display="none";
  document.getElementById("homeScreen").style.display="flex";
  lofi.volume=0.2; lofi.play();
}

function toggleDev(){ document.getElementById("devConsole").style.display="block"; }
function loginDev(){ 
  const pw = document.getElementById("devPassword").value;
  if(pw==="Emil2014") document.getElementById("devActions").style.display="block"; 
  else alert("Wrong password!"); 
}

function banUser(){
  const name = document.getElementById("banUserInput").value.trim();
  if(!name){ alert("Enter a username"); return; }
  if(!onlineUsers.includes(name)){ alert("User not found"); return; }
  bannedUsers.push(name);
  const idx = onlineUsers.indexOf(name);
  if(idx>-1) onlineUsers.splice(idx,1);
  localStorage.setItem("bannedUsers", JSON.stringify(bannedUsers));
  localStorage.setItem("onlineUsers", JSON.stringify(onlineUsers));
  alert(name+" has been banned!");
}

function showActivePlayers(){
  const list = onlineUsers.filter(u=>!bannedUsers.includes(u));
  alert("Active Players:\n" + (list.length?list.join("\n"):"No active players"));
}

// GAME FUNCTIONS
const home=document.getElementById("homeScreen");
const homeBtn=document.get
