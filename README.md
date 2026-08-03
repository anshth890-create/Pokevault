# Pokevault
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PokeVault Pro</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

body{
background:linear-gradient(135deg,#0f172a,#1e293b,#111827);
min-height:100vh;
display:flex;
justify-content:center;
align-items:center;
padding:20px;
color:#fff;
}

.container{
width:100%;
max-width:500px;
background:#1e293b;
border-radius:20px;
padding:25px;
box-shadow:0 0 25px rgba(0,0,0,.5);
text-align:center;
}

.logo{
font-size:34px;
font-weight:700;
color:#ffcb05;
margin-bottom:20px;
}

.searchBox{
display:flex;
gap:10px;
margin-bottom:20px;
}

.searchBox input{
flex:1;
padding:12px;
border:none;
border-radius:12px;
font-size:16px;
outline:none;
}

.searchBox button{
padding:12px 18px;
border:none;
border-radius:12px;
background:#ffcb05;
font-weight:bold;
cursor:pointer;
transition:.3s;
}

.searchBox button:hover{
transform:scale(1.05);
}

#pokemon{
margin-top:20px;
}

.card img{
width:220px;
height:220px;
object-fit:contain;
animation:float 2s ease-in-out infinite;
}

@keyframes float{
0%{transform:translateY(0);}
50%{transform:translateY(-10px);}
100%{transform:translateY(0);}
}
  .info{
margin-top:20px;
text-align:left;
background:#0f172a;
padding:15px;
border-radius:15px;
display:none;
}

.info h2{
text-align:center;
color:#ffcb05;
margin-bottom:15px;
}

.row{
display:flex;
justify-content:space-between;
margin:8px 0;
font-size:16px;
}

.stats{
margin-top:20px;
}

.bar{
background:#374151;
height:10px;
border-radius:20px;
overflow:hidden;
margin-bottom:12px;
}

.fill{
height:100%;
background:#22c55e;
width:0%;
transition:1s;
}

button.play{
margin-top:20px;
width:100%;
padding:12px;
border:none;
border-radius:12px;
background:#22c55e;
color:white;
font-size:16px;
cursor:pointer;
}

footer{
margin-top:25px;
color:#9ca3af;
font-size:14px;
}

.loading{
font-size:18px;
margin-top:20px;
color:#ffcb05;
}

.error{
color:#ef4444;
margin-top:20px;
font-size:18px;
}

</style>
</head>

<body>

<div class="container">

<h1 class="logo">⚡ PokeVault Pro</h1>

<div class="searchBox">

<input
type="text"
id="pokeName"
placeholder="Enter Pokémon Name">

<button onclick="loadPokemon()">
Search
</button>

</div>

<div id="pokemon"></div>

<audio id="cry"></audio>

<footer>
Made with ❤️ by <b>Ansh Thakur</b>
</footer>

<script>
const pokemon=document.getElementById("pokemon");
const cry=document.getElementById("cry");
  async function loadPokemon(){

const name=document.getElementById("pokeName").value.toLowerCase()||"pikachu";

pokemon.innerHTML='<div class="loading">Loading Pokémon...</div>';

try{

const res=await fetch("https://pokeapi.co/api/v2/pokemon/"+name);

if(!res.ok) throw new Error();

const data=await res.json();

pokemon.innerHTML=`

<div class="card">

<img src="${data.sprites.other["official-artwork"].front_default}" alt="${data.name}">

<div class="info" style="display:block;">

<h2>${data.name.toUpperCase()}</h2>

<div class="row">
<span>Type</span>
<span>${data.types.map(t=>t.type.name).join(", ")}</span>
</div>

<div class="row">
<span>Height</span>
<span>${data.height}</span>
</div>

<div class="row">
<span>Weight</span>
<span>${data.weight}</span>
</div>

<div class="row">
<span>Ability</span>
<span>${data.abilities.map(a=>a.ability.name).join(", ")}</span>
</div>

<div class="stats">

<p>HP</p>
<div class="bar">
<div class="fill" style="width:${data.stats[0].base_stat}%"></div>
</div>

<p>Attack</p>
<div class="bar">
<div class="fill" style="width:${data.stats[1].base_stat}%"></div>
</div>

<p>Defense</p>
<div class="bar">
<div class="fill" style="width:${data.stats[2].base_stat}%"></div>
</div>
<p>Special Attack</p>
<div class="bar">
<div class="fill" style="width:${data.stats[3].base_stat}%"></div>
</div>

<p>Special Defense</p>
<div class="bar">
<div class="fill" style="width:${data.stats[4].base_stat}%"></div>
</div>

<p>Speed</p>
<div class="bar">
<div class="fill" style="width:${data.stats[5].base_stat}%"></div>
</div>

</div>

<button class="play" onclick="playCry('${data.cries.latest}')">
🔊 Play Pokémon Cry
</button>

</div>

</div>
`;

}catch{

pokemon.innerHTML=`
<div class="error">
❌ Pokémon Not Found
</div>
`;

}

}

function playCry(url){

cry.src=url;

cry.play();

}

document.getElementById("pokeName").addEventListener("keypress",function(e){

if(e.key==="Enter"){

loadPokemon();

}

});

loadPokemon();
  function randomPokemon(){

const pokemonList=[
"pikachu",
"charizard",
"bulbasaur",
"squirtle",
"charmander",
"lucario",
"greninja",
"gengar",
"mew",
"mewtwo",
"rayquaza",
"garchomp",
"dragonite",
"eevee",
"snorlax",
"blaziken",
"sceptile",
"luxray",
"lapras",
"tyranitar"
];

const randomName=pokemonList[Math.floor(Math.random()*pokemonList.length)];

document.getElementById("pokeName").value=randomName;

loadPokemon();

}

const randomBtn=document.createElement("button");

randomBtn.innerHTML="🎲 Random Pokémon";

randomBtn.style.width="100%";
randomBtn.style.marginTop="15px";
randomBtn.style.padding="12px";
randomBtn.style.border="none";
randomBtn.style.borderRadius="12px";
randomBtn.style.background="#3b82f6";
randomBtn.style.color="#fff";
randomBtn.style.fontSize="16px";
randomBtn.style.cursor="pointer";

randomBtn.onclick=randomPokemon;

document.querySelector(".container").appendChild(randomBtn);
  <style>

.type{
display:inline-block;
padding:6px 12px;
border-radius:20px;
margin:5px;
font-weight:bold;
text-transform:capitalize;
background:#facc15;
color:#111;
}

.pokemon-card{
animation:show .5s ease;
}

@keyframes show{
from{
opacity:0;
transform:scale(.8);
}
to{
opacity:1;
transform:scale(1);
}
}

</style>


<script>

function capitalize(text){

return text.charAt(0).toUpperCase()+text.slice(1);

}


function showTypes(types){

return types.map(t=>{

return `<span class="type">${capitalize(t.type.name)}</span>`;

}).join("");

}


</script>
<script>

async function getPokemonSpecies(name){

try{

const res = await fetch(
"https://pokeapi.co/api/v2/pokemon-species/"+name
);

const data = await res.json();

let evolutionURL=data.evolution_chain.url;

const evoRes=await fetch(evolutionURL);

const evoData=await evoRes.json();

let first=evoData.chain.species.name;

let second=evoData.chain.evolves_to[0]?.species.name || "None";

let third=evoData.chain.evolves_to[0]?.evolves_to[0]?.species.name || "None";


console.log(
"Evolution:",
first,
second,
third
);

}catch(error){

console.log("Evolution not found");

}

}


function loading(){

pokemon.innerHTML=`
<div class="loading">
⚡ Finding Pokémon...
</div>
`;

}


</script>
<script>

// Default Pokémon load
window.onload=function(){
loadPokemon();
};


// Clear Search Button
const clearBtn=document.createElement("button");

clearBtn.innerHTML="🗑️ Clear";

clearBtn.style.width="100%";
clearBtn.style.marginTop="10px";
clearBtn.style.padding="12px";
clearBtn.style.border="none";
clearBtn.style.borderRadius="12px";
clearBtn.style.background="#ef4444";
clearBtn.style.color="white";
clearBtn.style.fontSize="16px";
clearBtn.style.cursor="pointer";


clearBtn.onclick=function(){

document.getElementById("pokeName").value="";
pokemon.innerHTML="";

};


document.querySelector(".container").appendChild(clearBtn);


</script>

</body>
</html>
<div class="gallery">

<h2>🔥 Popular Pokémon</h2>

<div class="pokemon-list">

<div class="poke-card" onclick="loadPokemonByName('pikachu')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png">
<p>Pikachu</p>
</div>

<div class="poke-card" onclick="loadPokemonByName('charizard')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png">
<p>Charizard</p>
</div>

<div class="poke-card" onclick="loadPokemonByName('bulbasaur')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png">
<p>Bulbasaur</p>
</div>

<div class="poke-card" onclick="loadPokemonByName('squirtle')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png">
<p>Squirtle</p>
</div>

<div class="poke-card" onclick="loadPokemonByName('lucario')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/448.png">
<p>Lucario</p>
</div>

<div class="poke-card" onclick="loadPokemonByName('mewtwo')">
<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png">
<p>Mewtwo</p>
</div>

</div>
</div>
<style>

.gallery{
margin-top:30px;
}

.pokemon-list{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:15px;
margin-top:15px;
}

.poke-card{
background:#0f172a;
border-radius:15px;
padding:10px;
cursor:pointer;
transition:.3s;
}

.poke-card:hover{
transform:scale(1.08);
}

.poke-card img{
width:80px;
height:80px;
object-fit:contain;
}

.poke-card p{
font-weight:bold;
}

</style>
function loadPokemonByName(name){

document.getElementById("pokeName").value=name;

loadPokemon();

}
