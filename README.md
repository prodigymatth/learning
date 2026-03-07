<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>onclu</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}

/* BACKGROUND */

body{
min-height:100vh;
background:linear-gradient(rgba(30,0,70,0.7), rgba(10,0,30,0.9)),
url('https://media.gettyimages.com/id/881752658/video/journey-through-galaxy.jpg?s=640x640&k=20&c=ITfk5mu21pnyUjb7tTndTm8LMBqpPS4YBMY2Il_nGyQ=') no-repeat center center fixed;
background-size:cover;
color:white;
overflow-x:hidden;
}

/* STARS */

.star{
position:absolute;
background:white;
border-radius:50%;
animation:twinkle 2s infinite alternate;
}

@keyframes twinkle{
0%{opacity:.8}
100%{opacity:.2}
}

/* LOGIN */

#loginScreen{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
display:flex;
justify-content:center;
align-items:center;
background:rgba(20,0,50,.95);
z-index:1000;
}

.container{
background:rgba(255,255,255,.05);
backdrop-filter:blur(20px);
border-radius:20px;
padding:40px 30px;
width:350px;
text-align:center;
box-shadow:0 8px 32px rgba(0,0,0,.6);
}

h2{margin-bottom:20px}

input{
width:90%;
padding:12px;
margin:10px 0;
border:none;
border-radius:10px;
background:rgba(255,255,255,.2);
color:white;
}

button{
width:95%;
padding:12px;
margin-top:10px;
border:none;
border-radius:12px;
background:white;
color:#6a0dad;
font-weight:bold;
cursor:pointer;
}

span{
color:#ffccff;
cursor:pointer;
text-decoration:underline;
}

.message{
font-size:13px;
margin-top:8px;
color:#ffccff;
}

/* HOME */

#homeScreen{
display:none;
flex-direction:column;
align-items:center;
padding-top:80px;
text-align:center;
}

h1{
font-size:70px;
margin-bottom:40px;
text-shadow:0 0 30px #a855f7;
}

.buttonContainer{
display:flex;
flex-direction:column;
gap:12px;
width:280px;
}

.gameBtn{
padding:14px;
background:rgba(60,0,100,.15);
border:1px solid rgba(200,150,255,.3);
border-radius:8px;
color:white;
cursor:pointer;
}

.gameBtn:hover{
background:rgba(120,0,180,.3);
}

/* HOME BUTTON */

#homeBtn{
position:fixed;
top:15px;
left:15px;
display:none;
padding:6px 10px;
background:rgba(0,0,0,.4);
color:white;
border:none;
cursor:pointer;
}

/* IFRAMES */

iframe,embed{
position:fixed;
top:0;
left:0;
width:100%;
height:100vh;
border:none;
display:none;
z-index:5;
}

/* DEV PANEL */

#devPanel{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:#120024;
z-index:2000;
padding-top:100px;
text-align:center;
}

#devPanel input{
width:250px;
}

.userList{
margin-top:10px;
}

.userRow{
margin:4px;
}

audio{display:none}

</style>
</head>
<body>

<!-- LOGIN -->

<div id="loginScreen">

<div class="container">

<div id="signinBox">

<h2>Login</h2>

<input id="signinUser" placeholder="Username">
<input id="signinPass" type="password" placeholder="Password">

<button onclick="signin()">Login</button>

<div class="message" id="signinMsg"></div>

<p>No account? <span onclick="showSignup()">Register</span></p>

</div>

<div id="signupBox" style="display:none">

<h2>Register</h2>

<input id="signupUser" placeholder="Username">
<input id="signupPass" type="password" placeholder="Password">
<input id="signupPass2" type="password" placeholder="Confirm Password">

<button onclick="signup()">Sign Up</button>

<div class="message" id="signupMsg"></div>

<p>Have an account? <span onclick="showSignin()">Login</span></p>

</div>

</div>
</div>

<!-- HOME -->

<div id="homeScreen">

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
<button class="gameBtn" onclick="openGame('agentFrame')">For Khalil</button>

<button class="gameBtn" onclick="openDevTools()">Dev Tools</button>

</div>

</div>

<button id="homeBtn" onclick="goHome()">Home</button>

<!-- IFRAMES -->

<iframe id="hoodaFrame" src="https://www.hoodamath.com/"></iframe>
<iframe id="playFrame" src="https://www.playtropolis.com"></iframe>
<iframe id="gFrame" src="https://ghub-light.neocities.org/"></iframe>
<iframe id="minecraftFrame" src="https://eaglercraft.com/"></iframe>
<embed id="infiniteFrame" src="https://infinite-craft.org/infinite-craft/">
<iframe id="soundboardFrame" src="https://www.myinstants.com/en/index/us/"></iframe>
<iframe id="mathFrame" src="https://www.coolmathgames.com/"></iframe>
<iframe id="cheeseFrame" src="https://stanthecheeseman.github.io/"></iframe>
<iframe id="basketFrame" src="https://www.twoplayergames.org/game/basket-random"></iframe>
<iframe id="agentFrame" src="https://www.twoplayergames.org/game/agent-walker-vs-skibidi-toilets"></iframe>

<!-- DEV PANEL -->

<div id="devPanel">

<h1>Developer Tools</h1>

<h3>Active Players</h3>
<div id="activePlayers"></div>

<h3>Ban User</h3>

<input id="banUserInput" placeholder="username">

<button onclick="banUser()">Ban</button>

<h3>Banned Users</h3>
<div id="banList"></div>

<br>
<button onclick="closeDevTools()">Close</button>

</div>

<audio id="lofi" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

<script>

/* STARS */

for(let i=0;i<100;i++){
let star=document.createElement("div")
star.className="star"
star.style.top=Math.random()*100+"%"
star.style.left=Math.random()*100+"%"
star.style.width=star.style.height=(Math.random()*2+1)+"px"
document.body.appendChild(star)
}

/* LOGIN UI */

function showSignup(){signinBox.style.display="none";signupBox.style.display="block";}
function showSignin(){signupBox.style.display="none";signinBox.style.display="block";}

function signup(){
let u=signupUser.value.trim()
let p=signupPass.value.trim()
let p2=signupPass2.value.trim()
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")

if(banned.includes(u)){signupMsg.innerText="You are banned";return;}
if(!u||!p||!p2){signupMsg.innerText="Fill all fields";return;}
if(p!==p2){signupMsg.innerText="Passwords don't match";return;}
if(localStorage.getItem(u)){signupMsg.innerText="Username exists";return;}

localStorage.setItem(u,p)
localStorage.setItem("currentUser",u)
loginSuccess()
}

function signin(){
let u=signinUser.value.trim()
let p=signinPass.value.trim()
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")
if(banned.includes(u)){signinMsg.innerText="You are banned";return;}
let stored=localStorage.getItem(u)
if(stored!==p){signinMsg.innerText="Invalid login";return;}
localStorage.setItem("currentUser",u)
loginSuccess()
}

function loginSuccess(){
loginScreen.style.display="none"
homeScreen.style.display="flex"
addActivePlayer(localStorage.getItem("currentUser"))
lofi.volume=.2
lofi.play()
}

/* AUTO LOGIN WITH BAN CHECK */

window.onload=function(){
let user=localStorage.getItem("currentUser")
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")
if(user){
if(banned.includes(user)){
alert("You are banned!"); localStorage.removeItem("currentUser"); return;}
loginSuccess()
}
}

/* ACTIVE PLAYERS */

function addActivePlayer(user){
let list=JSON.parse(localStorage.getItem("activePlayers")||"[]")
if(!list.includes(user)){
list.push(user)
localStorage.setItem("activePlayers",JSON.stringify(list))
}
}

/* GAME SYSTEM */

const homeBtn=document.getElementById("homeBtn")

function hideAll(){document.querySelectorAll("iframe,embed").forEach(e=>e.style.display="none")}

function openGame(id){
homeScreen.style.display="none"
hideAll()
document.getElementById(id).style.display="block"
homeBtn.style.display="block"
}

function goHome(){hideAll();homeScreen.style.display="flex";homeBtn.style.display="none"}

/* DEV TOOLS */

function openDevTools(){
let pass=prompt("Enter dev password")
if(pass!=="Emilk2014"){alert("Wrong password");return;}
devPanel.style.display="block"
updateBanList()
updateActivePlayers()
}

function closeDevTools(){devPanel.style.display="none"}

function banUser(){
let user=banUserInput.value.trim()
if(!user)return
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")
if(!banned.includes(user)) banned.push(user)
localStorage.setItem("bannedUsers",JSON.stringify(banned))
updateBanList()
}

function unbanUser(user){
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")
banned=banned.filter(x=>x!==user)
localStorage.setItem("bannedUsers",JSON.stringify(banned))
updateBanList()
}

function updateBanList(){
let banned=JSON.parse(localStorage.getItem("bannedUsers")||"[]")
banList.innerHTML=""
banned.forEach(u=>{
banList.innerHTML+=`<div class="userRow">${u} <button onclick="unbanUser('${u}')">Unban</button></div>`
})
}

function updateActivePlayers(){
let list=JSON.parse(localStorage.getItem("activePlayers")||"[]")
activePlayers.innerHTML=""
list.forEach(u=>{activePlayers.innerHTML+=`<div>${u}</div>`})
}

</script>

</body>
</html>
