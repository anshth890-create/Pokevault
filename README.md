# Pokevault
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>PokeVault</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#111827;
    color:white;
    text-align:center;
}

header{
    background:#ef4444;
    padding:20px;
    font-size:30px;
    font-weight:bold;
}

.container{
    margin:30px auto;
    max-width:400px;
}

input{
    padding:12px;
    width:70%;
    border-radius:10px;
    border:none;
    font-size:16px;
}

button{
    padding:12px;
    margin-top:10px;
    background:#facc15;
    border:none;
    border-radius:10px;
    cursor:pointer;
    font-weight:bold;
}

.card{
    margin-top:25px;
    background:#1f2937;
    padding:20px;
    border-radius:20px;
}

.card img{
    width:200px;
}
</style>

</head>

<body>

<header>
⚡ PokeVault ⚡
</header>

<div class="container">

<input id="search" placeholder="Enter Pokémon name">

<br>

<button onclick="searchPokemon()">Search</button>

<div id="pokemon"></div>

</div>
<script>

async function searchPokemon(){

let name = document.getElementById("search").value.toLowerCase();

let box = document.getElementById("pokemon");

try{

let response = await fetch(
"https://pokeapi.co/api/v2/pokemon/" + name
);

let data = await response.json();


box.innerHTML = `

<div class="card">

<h2>${data.name.toUpperCase()}</h2>

<img src="${data.sprites.other['official-artwork'].front_default}">

<p>⚡ Type: ${data.types[0].type.name}</p>

<p>🔥 Height: ${data.height}</p>

<p>💪 Weight: ${data.weight}</p>

</div>

`;

}

catch{

box.innerHTML = `
<div class="card">
<h2>❌ Pokémon not found!</h2>
<p>Try another name</p>
</div>
`;

}

}

</script>

</body>
</html>
<style>

.card{
    animation: pop 0.5s ease;
    box-shadow:0 0 20px #ef4444;
}

@keyframes pop{
    from{
        transform:scale(0.5);
        opacity:0;
    }
    to{
        transform:scale(1);
        opacity:1;
    }
}

footer{
    margin-top:40px;
    padding:15px;
    background:#000;
}

</style>

<footer>
Made with ❤️ for Pokémon fans
</footer>
<button onclick="randomPokemon()">🎲 Random Pokémon</button>

<script>

async function randomPokemon(){

let id = Math.floor(Math.random() * 151) + 1;

let box = document.getElementById("pokemon");

let response = await fetch(
"https://pokeapi.co/api/v2/pokemon/" + id
);

let data = await response.json();

box.innerHTML = `

<div class="card">

<h2>${data.name.toUpperCase()}</h2>

<img src="${data.sprites.other['official-artwork'].front_default}">

<p>⚡ Type: ${data.types[0].type.name}</p>

<p>⭐ Pokémon ID: ${data.id}</p>

</div>

`;

}

</script>
<h2>🔥 Pokémon Gallery 🔥</h2>

<div id="gallery"></div>

<style>

#gallery{
display:flex;
flex-wrap:wrap;
justify-content:center;
gap:15px;
}

.small-card{
background:#374151;
padding:15px;
border-radius:15px;
width:150px;
}

.small-card img{
width:120px;
}

</style>

<script>

async function loadGallery(){

let gallery = document.getElementById("gallery");

for(let i=1;i<=20;i++){

let res = await fetch(
"https://pokeapi.co/api/v2/pokemon/"+i
);

let data = await res.json();

gallery.innerHTML += `

<div class="small-card">

<h3>${data.name}</h3>

<img src="${data.sprites.other['official-artwork'].front_default}">

<p>Type: ${data.types[0].type.name}</p>

</div>

`;

}

}

loadGallery();

</script>
<button onclick="playSound()">🎵 Pokémon Sound</button>

<style>

.animate-pokemon{
    animation: jump 1s infinite;
}

@keyframes jump{
    0%{
        transform:translateY(0);
    }
    50%{
        transform:translateY(-15px);
    }
    100%{
        transform:translateY(0);
    }
}

</style>

<script>

function playSound(){

let audio = new Audio(
"https://raw.githubusercontent.com/PokeAPI/cries/main/cries/pokemon/latest/25.ogg"
);

audio.play();

}

</script>
<button onclick="changeMode()">🌙 Change Mode</button>

<div class="pokeball">
<div class="line"></div>
</div>

<style>

.pokeball{
width:100px;
height:100px;
background:red;
border-radius:50%;
margin:20px auto;
border:5px solid black;
position:relative;
animation:rotate 2s infinite linear;
}

.line{
position:absolute;
top:45%;
width:100%;
height:10px;
background:black;
}

.pokeball:after{
content:"";
position:absolute;
top:35px;
left:35px;
width:30px;
height:30px;
background:white;
border-radius:50%;
border:5px solid black;
}

@keyframes rotate{
from{
transform:rotate(0deg);
}
to{
transform:rotate(360deg);
}
}

.light{
background:white;
color:black;
}

</style>

<script>

function changeMode(){

document.body.classList.toggle("light");

}

</script>
<h2>⚔️ Pokémon Battle Arena ⚔️</h2>

<div class="battle">

<div class="trainer">
<h3>🧢 Trainer</h3>
<p>Ansh</p>
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/trainers/1.png">
</div>

<div class="vs">
VS
</div>

<div class="trainer">
<h3>🔥 Pokémon</h3>
<p>Pikachu</p>
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png">
</div>

</div>

<style>

.battle{
display:flex;
justify-content:center;
align-items:center;
gap:20px;
margin:20px;
}

.trainer{
background:#374151;
padding:15px;
border-radius:20px;
}

.trainer img{
width:120px;
}

.vs{
font-size:30px;
font-weight:bold;
color:#facc15;
}

</style>
<button onclick="addFavorite()">❤️ Add Favorite</button>

<div class="card">
<h2>📖 Pokédex Level</h2>
<p id="level">Level: 1</p>
<p id="fav">Favorite: None</p>
</div>

<script>

let level = 1;

function addFavorite(){

let name = document.getElementById("search").value;

if(name==""){
alert("पहले Pokémon का नाम लिखो!");
return;
}

document.getElementById("fav").innerHTML =
"Favorite: ❤️ " + name;

level++;

document.getElementById("level").innerHTML =
"Level: " + level;

}

</script>
body{
background:linear-gradient(135deg,#111827,#1e40af);
}

header{
font-size:35px;
text-shadow:0 0 15px yellow;
}

.logo{
font-size:50px;
animation:glow 2s infinite;
}

@keyframes glow{

0%{
text-shadow:0 0 5px yellow;
}

50%{
text-shadow:0 0 25px red;
}

100%{
text-shadow:0 0 5px yellow;
}

}
<div class="logo">
⚡ PokeVault ⚡
</div>
<h2>🎬 Pokémon Trailer Zone</h2>

<div class="video-box">

<button onclick="openTrailer()">
▶ Watch Pokémon Trailer
</button>

</div>

<style>

.video-box{
background:#1f2937;
padding:20px;
border-radius:20px;
margin:20px;
}

.video-box button{
background:#ef4444;
color:white;
font-size:18px;
}

</style>

<script>

function openTrailer(){

window.open(
"https://www.youtube.com/results?search_query=pokemon+official+trailer",
"_blank"
);

}

</script>
<p>✨ Ability: ${data.abilities[0].ability.name}</p>

<p>⚔️ Move: ${data.moves[0].move.name}</p>
<div class="card">

<h2>${data.name.toUpperCase()}</h2>

<img src="${data.sprites.other['official-artwork'].front_default}">

<p>⚡ Type: ${data.types[0].type.name}</p>

<p>⭐ ID: ${data.id}</p>

<p>✨ Ability: ${data.abilities[0].ability.name}</p>

<p>⚔️ Move: ${data.moves[0].move.name}</p>

</div>
<h2>📜 Search History</h2>

<div id="history"></div>

<h2>❤️ Favorite List</h2>

<div id="favorites"></div>


<script>

let history = JSON.parse(localStorage.getItem("history")) || [];
let favorites = JSON.parse(localStorage.getItem("favorites")) || [];


function saveHistory(name){

history.push(name);

localStorage.setItem(
"history",
JSON.stringify(history)
);

showData();

}


function addFavorite(){

let name = document.getElementById("search").value;

favorites.push(name);

localStorage.setItem(
"favorites",
JSON.stringify(favorites)
);

showData();

}


function showData(){

document.getElementById("history").innerHTML =
history.join(" • ");

document.getElementById("favorites").innerHTML =
favorites.join(" ❤️ ");

}

showData();

</script>
<div id="loader">
⚡ Loading PokeVault...
</div>
#loader{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:#111827;
display:flex;
justify-content:center;
align-items:center;
font-size:25px;
z-index:999;
}
window.onload = function(){

setTimeout(function(){

document.getElementById("loader").style.display="none";

},1500);

}
.card{
    background:#1f2937;
    border-radius:25px;
    padding:25px;
    margin:20px auto;
    max-width:350px;
    box-shadow:0 0 20px #000;
    transition:0.3s;
}

.card:hover{
    transform:scale(1.05);
}

.type{
    padding:8px 15px;
    border-radius:20px;
    font-weight:bold;
}


/* Pokémon Type Style */

.fire{
    background:#ef4444;
}

.water{
    background:#3b82f6;
}

.grass{
    background:#22c55e;
}

.electric{
    background:#facc15;
    color:black;
}

.psychic{
    background:#ec4899;
}

.ice{
    background:#67e8f9;
    color:black;
}

.dragon{
    background:#7c3aed;
}

.normal{
    background:#9ca3af;
}
<h2>📚 Complete Pokédex</h2>

<button onclick="loadAllPokemon()">
Show Pokémon List
</button>

<div id="pokedex"></div>


<style>

#pokedex{
display:flex;
flex-wrap:wrap;
justify-content:center;
gap:15px;
}

.poke-box{
background:#374151;
padding:15px;
border-radius:15px;
width:140px;
}

.poke-box img{
width:100px;
}

</style>


<script>

async function loadAllPokemon(){

let box = document.getElementById("pokedex");

box.innerHTML="Loading Pokémon...";


let res = await fetch(
"https://pokeapi.co/api/v2/pokemon?limit=151"
);

let data = await res.json();


box.innerHTML="";


data.results.forEach((pokemon,index)=>{

box.innerHTML += `

<div class="poke-box">

<h3>#${index+1}</h3>

<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index+1}.png">

<p>${pokemon.name}</p>

</div>

`;

});

}

</script>
<h2>🔄 Evolution Chain</h2>

<div class="evolution">

<div>
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/4.png">
<p>Charmander</p>
</div>

➡️

<div>
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/5.png">
<p>Charmeleon</p>
</div>

➡️

<div>
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/6.png">
<p>Charizard</p>
</div>

</div>


<style>

.evolution{
display:flex;
justify-content:center;
align-items:center;
gap:15px;
background:#1f2937;
padding:20px;
border-radius:20px;
}

.evolution img{
width:100px;
}

</style>
<h2>⚔️ Battle Mode</h2>

<div class="battle-card">

<h3>🔥 Pikachu Battle</h3>

<p>HP</p>

<div class="hp">
<div id="hpbar"></div>
</div>

<button onclick="attack()">
⚡ Thunder Attack
</button>

<p id="result"></p>

</div>


<style>

.battle-card{
background:#1f2937;
padding:20px;
border-radius:20px;
margin:20px;
}

.hp{
width:100%;
height:20px;
background:#555;
border-radius:20px;
}

#hpbar{
height:100%;
width:100%;
background:green;
border-radius:20px;
}

</style>


<script>

let hp=100;

function attack(){

hp = hp - 20;

if(hp<0){
hp=0;
}

document.getElementById("hpbar").style.width =
hp+"%";

document.getElementById("result").innerHTML =
"⚡ Attack! HP: "+hp;

}

</script>
<h2>🏆 Trainer Points</h2>

<div class="card">

<p id="coins">
🪙 Coins: 0
</p>

<p id="points">
⭐ Points: 0
</p>

<button onclick="winBattle()">
🏅 Win Battle
</button>

</div>


<script>

let coins = Number(localStorage.getItem("coins")) || 0;
let points = Number(localStorage.getItem("points")) || 0;


function winBattle(){

coins += 10;
points += 5;


localStorage.setItem("coins",coins);
localStorage.setItem("points",points);


document.getElementById("coins").innerHTML =
"🪙 Coins: " + coins;


document.getElementById("points").innerHTML =
"⭐ Points: " + points;

}


document.getElementById("coins").innerHTML =
"🪙 Coins: " + coins;


document.getElementById("points").innerHTML =
"⭐ Points: " + points;


</script>
<h2>🏅 Trainer Badges</h2>

<div class="badges">

<div class="badge">
⚡<br>
Thunder Badge
</div>

<div class="badge">
🔥<br>
Fire Badge
</div>

<div class="badge">
🌊<br>
Water Badge
</div>

</div>


<style>

.badges{
display:flex;
justify-content:center;
gap:15px;
flex-wrap:wrap;
}

.badge{
background:#374151;
padding:20px;
border-radius:20px;
font-size:18px;
box-shadow:0 0 15px black;
}

.badge:hover{
transform:scale(1.1);
}

</style>
<h2>🧢 Trainer Profile</h2>

<div class="card">

<input id="trainerName" placeholder="Enter Trainer Name">

<br>

<button onclick="saveTrainer()">
Save Trainer
</button>

<h3 id="showTrainer">
Trainer: Guest
</h3>

</div>


<script>

function saveTrainer(){

let name = document.getElementById("trainerName").value;

if(name==""){
name="Guest";
}

localStorage.setItem("trainer",name);

document.getElementById("showTrainer").innerHTML =
"Trainer: 🧢 " + name;

}


let savedName = localStorage.getItem("trainer");

if(savedName){

document.getElementById("showTrainer").innerHTML =
"Trainer: 🧢 " + savedName;

}

</script>
<h2>👥 My Pokémon Team</h2>

<input id="teamPokemon" placeholder="Enter Pokémon name">

<button onclick="addTeam()">
➕ Add to Team
</button>

<div id="team"></div>


<style>

.team-card{
display:inline-block;
background:#374151;
padding:15px;
margin:10px;
border-radius:20px;
}

.team-card img{
width:100px;
}

</style>


<script>

let team=[];

function addTeam(){

let name=document
.getElementById("teamPokemon")
.value
.toLowerCase();


if(team.length>=6){

alert("Your team is full! (6 Pokémon)");

return;

}


fetch("https://pokeapi.co/api/v2/pokemon/"+name)

.then(res=>res.json())

.then(data=>{

team.push(data.name);


document.getElementById("team").innerHTML += `

<div class="team-card">

<h3>${data.name}</h3>

<img src="${data.sprites.other['official-artwork'].front_default}">

</div>

`;

})

.catch(()=>{

alert("Pokémon not found!");

});

}

</script>
<h2>🔴 Catch Pokémon</h2>

<button onclick="catchPokemon()">
🔴 Throw Pokéball
</button>

<div id="catchResult"></div>


<style>

.catch-ball{
font-size:60px;
animation:throw 1s;
}

@keyframes throw{

0%{
transform:translateY(0);
}

50%{
transform:translateY(-80px);
}

100%{
transform:translateY(0);
}

}

</style>


<script>

function catchPokemon(){

let box=document.getElementById("catchResult");

box.innerHTML=`
<div class="catch-ball">
🔴
</div>
`;

setTimeout(()=>{

box.innerHTML=
"🎉 Pokémon Caught!";

},1000);

}

</script>

