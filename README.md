<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Motivação para Clara 💪</title>
  <style>
    :root {
      --azul-escuro: #1d3557;
      --azul-medio: #457b9d;
      --azul-claro: #a8dadc;
      --branco: #f1faee;
      --verde: #06d6a0;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(180deg, var(--branco), #d9eaf5);
      color: var(--azul-escuro);
      transition: background 1s ease;
    }

    header {
      background: linear-gradient(90deg, var(--azul-escuro), var(--azul-medio));
      color: white;
      text-align: center;
      padding: 2rem;
      font-size: 2rem;
      font-weight: bold;
      letter-spacing: 1px;
    }

    nav {
      display: flex;
      justify-content: center;
      gap: 1rem;
      background-color: var(--azul-medio);
      padding: 1rem;
    }

    nav button {
      background: white;
      border: none;
      color: var(--azul-escuro);
      padding: 0.7rem 1.4rem;
      border-radius: 25px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.3s ease;
    }

    nav button:hover {
      background: var(--azul-claro);
      transform: scale(1.05);
    }

    section {
      display: none;
      max-width: 800px;
      margin: 2rem auto;
      background: white;
      border-radius: 20px;
      padding: 2rem;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      animation: fadeIn 0.6s ease;
    }

    section.active {
      display: block;
    }

    h2 {
      color: var(--azul-medio);
    }

    input, select {
      padding: 0.6rem;
      border-radius: 10px;
      border: 1px solid #ccc;
      outline: none;
      font-size: 1rem;
    }

    button {
      cursor: pointer;
    }

    .meta {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #f9f9f9;
      padding: 0.5rem 1rem;
      margin-top: 0.5rem;
      border-radius: 10px;
      transition: transform 0.2s;
    }

    .meta:hover {
      transform: translateX(3px);
    }

    .concluir {
      background: var(--verde);
      border: none;
      color: white;
      border-radius: 10px;
      padding: 0.4rem 0.7rem;
      font-weight: bold;
    }

    .motivacao {
      margin-top: 1rem;
      background: var(--azul-claro);
      padding: 1rem;
      border-radius: 10px;
      text-align: center;
      font-weight: 500;
      font-size: 1.1rem;
    }

    .celebracao {
      display: none;
      text-align: center;
      font-size: 1.8rem;
      color: var(--verde);
      margin-top: 1rem;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }

    canvas {
      width: 100%;
      max-width: 600px;
      height: 200px;
      background: #f5f9fc;
      border-radius: 10px;
      margin-top: 1rem;
    }
  </style>
</head>
<body>
  <header>💼 Site Motivacional da Clara</header>

  <nav>
    <button onclick="mostrarSecao('estudos')">Estudos</button>
    <button onclick="mostrarSecao('apoio')">Apoio</button>
    <button onclick="mostrarSecao('humor')">Humor</button>
  </nav>

  <!-- SEÇÃO ESTUDOS -->
  <section id="estudos" class="active">
    <h2>📘 Foco nos Estudos</h2>
    <p>Crie suas metas e comemore cada conquista, Clara!</p>
    <input type="text" id="novaMeta" placeholder="Digite sua meta...">
    <button onclick="adicionarMeta()">Adicionar</button>
    <div id="listaMetas"></div>
    <div class="celebracao" id="celebracao">🎉 Parabéns, Clara! Você está brilhando! 🌟</div>
  </section>

  <!-- SEÇÃO APOIO -->
  <section id="apoio">
    <h2>💖 Palavras de Apoio</h2>
    <div class="motivacao" id="mensagemMotivacional"></div>
    <button onclick="novaMensagem()">Nova mensagem 💬</button>
  </section>

  <!-- SEÇÃO HUMOR -->
  <section id="humor">
    <h2>😊 Como você está hoje?</h2>
    <select id="humorHoje">
      <option value="">Escolha...</option>
      <option value="feliz">Feliz 😄</option>
      <option value="ok">Mais ou menos 🙂</option>
      <option value="triste">Triste 😢</option>
    </select>
    <button onclick="registrarHumor()">Salvar</button>
    <div id="resultadoHumor"></div>
    <canvas id="graficoHumor"></canvas>
  </section>

  <audio id="somCelebracao" src="https://cdn.pixabay.com/audio/2022/03/15/audio_1d7e0b1c54.mp3"></audio>

  <script>
    function mostrarSecao(id) {
      document.querySelectorAll("section").forEach(s => s.classList.remove("active"));
      document.getElementById(id).classList.add("active");
    }

    // === Metas ===
    function adicionarMeta() {
      const metaTexto = document.getElementById('novaMeta').value.trim();
      if (!metaTexto) return;
      const lista = document.getElementById('listaMetas');
      const div = document.createElement('div');
      div.className = 'meta';
      div.innerHTML = `${metaTexto} <button class="concluir" onclick="concluirMeta(this)">✔</button>`;
      lista.appendChild(div);
      document.getElementById('novaMeta').value = '';
    }

    function concluirMeta(botao) {
      botao.parentElement.remove();
      const celebracao = document.getElementById('celebracao');
      celebracao.style.display = 'block';
      document.getElementById('somCelebracao').play();
      confete();
      setTimeout(() => celebracao.style.display = 'none', 3000);
    }

    // === Mensagens motivacionais ===
    const mensagens = [
      "Você é uma força imparável, Clara!",
      "Cada meta cumprida é uma vitória do seu esforço 💪",
      "Você está crescendo todos os dias, mesmo quando não percebe!",
      "Acredite em você — é aí que tudo começa!",
      "Orgulhe-se do seu progresso, Clara 🌟"
    ];

    function novaMensagem() {
      const msg = mensagens[Math.floor(Math.random() * mensagens.length)];
      document.getElementById('mensagemMotivacional').innerText = msg;
    }

    novaMensagem();
    setInterval(novaMensagem, 15000); // muda automaticamente a cada 15s

    // === Humor + gráfico ===
    let historicoHumor = [];

    function registrarHumor() {
      const humor = document.getElementById('humorHoje').value;
      if (!humor) return;
      historicoHumor.push(humor);
      desenharGrafico();
      let msg = "";
      if (humor === "feliz") msg = "Que bom te ver sorrindo! Continue espalhando essa energia ✨";
      else if (humor === "ok") msg = "Tudo bem ter dias neutros. Você está indo bem 💪";
      else msg = "Você é forte, Clara. Dias ruins passam, mas você fica 💖";
      document.getElementById('resultadoHumor').innerText = msg;
    }

    function desenharGrafico() {
      const ctx = document.getElementById('graficoHumor').getContext('2d');
      ctx.clearRect(0, 0, 600, 200);
      ctx.beginPath();
      ctx.moveTo(10, 180);
      historicoHumor.forEach((h, i) => {
        let y = h === "feliz" ? 60 : h === "ok" ? 120 : 180;
        ctx.lineTo(10 + i * 60, y);
      });
      ctx.strokeStyle = "#457b9d";
      ctx.lineWidth = 3;
      ctx.stroke();
    }

    // === Confete ===
    function confete() {
      const total = 60;
      for (let i = 0; i < total; i++) {
        const conf = document.createElement('div');
        conf.style.position = 'fixed';
        conf.style.width = '10px';
        conf.style.height = '10px';
        conf.style.background = `hsl(${Math.random() * 360}, 80%, 60%)`;
        conf.style.top = '0px';
        conf.style.left = Math.random() * window.innerWidth + 'px';
        conf.style.borderRadius = '50%';
        conf.style.opacity = '0.9';
        document.body.appendChild(conf);

        const anim = conf.animate([
          { transform: `translateY(0) rotate(0deg)`, opacity: 1 },
          { transform: `translateY(${window.innerHeight}px) rotate(720deg)`, opacity: 0 }
        ], { duration: 2000 + Math.random() * 2000, easing: 'ease-out' });

        anim.onfinish = () => conf.remove();
      }
    }
  </script>
</body>
</html>


