<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Clara — Diversão & Bem-Estar 🐰</title>
<style>
:root {
  --rosa-claro: #ffc0cb;
  --rosa-forte: #ff69b4;
  --amarelo: #fff176;
  --verde: #90ee90;
  --lilas: #dda0dd;
}

body {
  margin: 0;
  font-family: 'Comic Sans MS', cursive, sans-serif;
  background: linear-gradient(135deg, var(--rosa-claro), var(--lilas));
  transition: background 3s ease;
  overflow-x: hidden;
}

header {
  text-align: center;
  font-size: 2rem;
  padding: 2rem;
  color: white;
  background: var(--rosa-forte);
  box-shadow: 0 4px 6px rgba(0,0,0,0.2);
}

nav {
  display: flex;
  justify-content: center;
  gap: 1rem;
  padding: 1rem;
  background: var(--lilas);
}

nav button {
  padding: 0.6rem 1.2rem;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-weight: bold;
  background: var(--amarelo);
  transition: transform 0.2s;
}

nav button:hover {
  transform: scale(1.1);
  background: var(--verde);
}

section {
  max-width: 700px;
  margin: 2rem auto;
  padding: 2rem;
  background: white;
  border-radius: 20px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  display: none;
  animation: aparecer 0.5s ease;
  position: relative;
}

section.active { display: block; }

@keyframes aparecer {
  from { opacity: 0; transform: translateY(20px);}
  to { opacity: 1; transform: translateY(0);}
}

h2 {
  text-align: center;
  color: var(--rosa-forte);
}

input, select {
  width: 100%;
  padding: 0.5rem;
  margin-top: 0.5rem;
  border-radius: 10px;
  border: 1px solid #ccc;
  outline: none;
}

button.faz-tudo {
  margin-top: 0.5rem;
  background: var(--rosa-forte);
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  font-weight: bold;
  transition: 0.3s;
}

button.faz-tudo:hover {
  transform: scale(1.1);
  background: var(--verde);
}

.meta, .mensagem, .humor {
  padding: 0.5rem 1rem;
  margin: 0.5rem 0;
  border-radius: 15px;
  background: var(--amarelo);
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.concluir {
  background: var(--rosa-forte);
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  padding: 0.2rem 0.6rem;
}

.celebracao {
  text-align: center;
  font-size: 2rem;
  display: none;
  margin-top: 1rem;
}

.mascote {
  position: fixed;
  bottom: 10px;
  right: 10px;
  font-size: 3rem;
  cursor: pointer;
  user-select: none;
  transition: transform 0.2s;
}

.mascote:hover {
  transform: scale(1.3) rotate(-15deg);
}
</style>
</head>
<body>

<header>🎀 Clara — Diversão & Bem-Estar 🐰</header>

<nav>
  <button onclick="mostrar('estudos')">Estudos</button>
  <button onclick="mostrar('mensagens')">Mensagens</button>
  <button onclick="mostrar('humor')">Humor</button>
</nav>

<!-- ESTUDOS -->
<section id="estudos" class="active">
  <h2>📚 Metinhas Divertidas</h2>
  <input type="text" id="novaMeta" placeholder="Ex: Estudar 20 min 💖">
  <button class="faz-tudo" onclick="adicionarMeta()">Adicionar meta</button>
  <div id="listaMetas"></div>
  <div class="celebracao" id="celebracao">🎉 Uhul! Concluído! 🌟</div>
</section>

<!-- MENSAGENS -->
<section id="mensagens">
  <h2>💌 Mensagens Fofas</h2>
  <div class="mensagem" id="msgFofa"></div>
  <button class="faz-tudo" onclick="novaMensagem()">Nova mensagem 💖</button>
</section>

<!-- HUMOR -->
<section id="humor">
  <h2>😊 Como você está?</h2>
  <select id="humorHoje">
    <option value="">Escolha...</option>
    <option value="feliz">Feliz 😄</option>
    <option value="ok">Mais ou menos 🙂</option>
    <option value="triste">Triste 😢</option>
  </select>
  <button class="faz-tudo" onclick="registrarHumor()">Salvar</button>
  <div class="humor" id="resultadoHumor"></div>
</section>

<div class="mascote" id="mascote">🐰</div>

<script>
function mostrar(secao) {
  document.querySelectorAll("section").forEach(s => s.classList.remove("active"));
  document.getElementById(secao).classList.add("active");
}

// --- METAS ---
function adicionarMeta() {
  const meta = document.getElementById('novaMeta').value.trim();
  if(!meta) return;
  const div = document.createElement('div');
  div.className = 'meta';
  div.innerHTML = `${meta} <button class="concluir" onclick="concluirMeta(this)">✔</button>`;
  document.getElementById('listaMetas').appendChild(div);
  document.getElementById('novaMeta').value = '';
}

function concluirMeta(botao) {
  botao.parentElement.remove();
  const c = document.getElementById('celebracao');
  c.style.display = 'block';
  confete();
  boostPositividade();
  setTimeout(()=>c.style.display='none',2000);
}

// --- MENSAGENS FOFA ---
const mensagens = [
  "Você é incrível, Clara! 🌸",
  "Cada passo seu é uma vitória 💖",
  "Continue sorrindo! 😄",
  "O mundo fica melhor com você 💕",
  "Você merece todo amor e alegria 🌟"
];

function novaMensagem() {
  const msg = mensagens[Math.floor(Math.random()*mensagens.length)];
  document.getElementById('msgFofa').innerText = msg;
}

// --- HUMOR ---
function registrarHumor() {
  const humor = document.getElementById('humorHoje').value;
  let msg = "";
  if(humor==="feliz") msg="Que ótimo ver você sorrindo! 😄";
  else if(humor==="ok") msg="Está tudo bem ter dias assim 🙂";
  else if(humor==="triste") msg="Tudo bem se sentir triste às vezes ❤️";
  document.getElementById('resultadoHumor').innerText = msg;
}

// --- CONFETE ---
function confete(){
  for(let i=0;i<50;i++){
    const c=document.createElement('div');
    c.style.position='fixed';
    c.style.width='10px';
    c.style.height='10px';
    c.style.background=`hsl(${Math.random()*360},80%,60%)`;
    c.style.top='0px';
    c.style.left=Math.random()*window.innerWidth+'px';
    c.style.borderRadius='50%';
    document.body.appendChild(c);
    const anim=c.animate([{transform:'translateY(0) rotate(0deg)',opacity:1},{transform:`translateY(${window.innerHeight}px) rotate(720deg)`,opacity:0}],{duration:2000+Math.random()*2000,easing:'ease-out'});
    anim.onfinish=()=>c.remove();
  }
}

// --- BOOST DE POSITIVIDADE ---
function boostPositividade(){
  document.body.style.background = `linear-gradient(135deg, hsl(${Math.random()*360},70%,80%), hsl(${Math.random()*360},70%,85%))`;
}

// --- MASCOTE INTERATIVO ---
const mascote = document.getElementById('mascote');
mas

  </script>
</body>
</html>


