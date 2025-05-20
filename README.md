<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Roleta das Derivadas 🎰</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f0f4f8;
      margin: 0;
      padding: 2rem;
    }
    h1 {
      color: #333;
    }
    .roleta {
      margin: 2rem auto;
      width: 300px;
      height: 300px;
      border: 10px solid #444;
      border-radius: 50%;
      position: relative;
      overflow: hidden;
    }
    .seta {
      width: 0;
      height: 0;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
      border-bottom: 30px solid red;
      position: absolute;
      top: -30px;
      left: calc(50% - 20px);
    }
    .botao {
      padding: 1rem 2rem;
      font-size: 1.2rem;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    iframe {
      margin-top: 2rem;
      width: 560px;
      height: 315px;
      max-width: 90%;
    }
  </style>
</head>
<body>
  <h1>🎲 Roleta das Derivadas 🎲</h1>
  <p>Clique no botão e descubra um vídeo para aprender derivadas!</p>
  <div class="roleta" id="roleta">
    <canvas id="canvas-roleta" width="300" height="300"></canvas>
    <div class="seta"></div>
  </div>
  <button class="botao" id="botao-roleta" onclick="rodarRoleta()">GIRAR A ROLETA!</button>
  <div id="video-container"></div>

  <script>
    const videos = [
      'https://www.youtube.com/embed/I9BdLHVYZx8', // Derivada básica
      'https://www.youtube.com/embed/h5zS_Z1-5D0', // Derivada do seno e cosseno
      'https://www.youtube.com/embed/_z7GRU5zrrs', // Regra da cadeia
      'https://www.youtube.com/embed/m0uU-9v8EKg', // Derivada do produto e quociente
      'https://www.youtube.com/embed/RSUJ4zyy-Lw'  // Aplicações práticas das derivadas
    ];
    const labels = [
      'Básica',
      'Seno/Cosseno',
      'Regra da cadeia',
      'Produto/Quociente',
      'Aplicações'
    ];
    const colors = ['#ff7675', '#74b9ff', '#55efc4', '#ffeaa7', '#fd79a8'];
    const canvas = document.getElementById('canvas-roleta');
    const ctx = canvas.getContext('2d');
    const numSetores = videos.length;
    const anguloSetor = 2 * Math.PI / numSetores;
    let girando = false;

    function desenharRoleta(angulo = 0) {
      ctx.clearRect(0, 0, 300, 300);
      for (let i = 0; i < numSetores; i++) {
        ctx.beginPath();
        ctx.moveTo(150, 150);
        ctx.arc(150, 150, 140, angulo + i * anguloSetor, angulo + (i + 1) * anguloSetor);
        ctx.closePath();
        ctx.fillStyle = colors[i];
        ctx.fill();
        // Texto
        ctx.save();
        ctx.translate(150, 150);
        ctx.rotate(angulo + (i + 0.5) * anguloSetor);
        ctx.textAlign = 'right';
        ctx.font = 'bold 16px Arial';
        ctx.fillStyle = '#333';
        ctx.fillText(labels[i], 120, 10);
        ctx.restore();
      }
    }
    desenharRoleta();

    function rodarRoleta() {
      if (girando) return;
      girando = true;
      document.getElementById('botao-roleta').disabled = true;
      const indice = Math.floor(Math.random() * numSetores);
      const voltas = 5 + Math.random() * 2; // 5 a 7 voltas
      const anguloFinal = 2 * Math.PI * voltas - indice * anguloSetor - anguloSetor / 2;
      let anguloAtual = 0;
      const duracao = 3500; // ms
      const inicio = performance.now();

      function animarRoleta(agora) {
        const tempo = agora - inicio;
        const progresso = Math.min(tempo / duracao, 1);
        // Ease out
        const ease = 1 - Math.pow(1 - progresso, 3);
        anguloAtual = ease * anguloFinal;
        desenharRoleta(anguloAtual);
        if (progresso < 1) {
          requestAnimationFrame(animarRoleta);
        } else {
          girando = false;
          document.getElementById('botao-roleta').disabled = false;
          mostrarVideo(indice);
        }
      }
      requestAnimationFrame(animarRoleta);
    }

    function mostrarVideo(indice) {
      const url = videos[indice];
      const container = document.getElementById('video-container');
      container.innerHTML = `<iframe src="${url}" frameborder="0" allowfullscreen></iframe>`;
    }
  </script>
</body>
</html>
