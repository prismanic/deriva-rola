# deriva-rola
roleta de derivadas cod.
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
  <div class="roleta">
    <div class="seta"></div>
  </div>
  <button class="botao" onclick="rodarRoleta()">GIRAR A ROLETA!</button>
  <div id="video-container"></div>

  <script>
    const videos = [
      'https://www.youtube.com/embed/I9BdLHVYZx8', // Derivada básica
      'https://www.youtube.com/embed/h5zS_Z1-5D0', // Derivada do seno e cosseno
      'https://www.youtube.com/embed/_z7GRU5zrrs', // Regra da cadeia
      'https://www.youtube.com/embed/m0uU-9v8EKg', // Derivada do produto e quociente
      'https://www.youtube.com/embed/RSUJ4zyy-Lw'  // Aplicações práticas das derivadas
    ];

    function rodarRoleta() {
      const indice = Math.floor(Math.random() * videos.length);
      const url = videos[indice];
      const container = document.getElementById('video-container');
      container.innerHTML = `<iframe src="${url}" frameborder="0" allowfullscreen></iframe>`;
    }
  </script>
</body>
</html>
