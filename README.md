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


