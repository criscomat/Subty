<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Subty</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      background: #000;
      color: #ffd400;
      font-family: Arial, sans-serif;
      height: 100vh;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    h1 {
      position: absolute;
      top: 20px;
      font-size: 24px;
      letter-spacing: 5px;
    }

    #subtitulo {
      width: 90%;
      max-width: 1100px;
      text-align: center;
      font-size: clamp(32px, 6vw, 72px);
      font-weight: bold;
      line-height: 1.15;

      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;

      min-height: 170px;
    }

    button {
      position: absolute;
      bottom: 35px;
      background: #ffd400;
      color: #000;
      border: none;
      padding: 15px 32px;
      border-radius: 30px;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      transform: scale(1.05);
    }
  </style>
</head>

<body>

  <h1>SUBTY</h1>

  <div id="subtitulo">
    Hola, ¿cómo estás?
  </div>

  <button onclick="escuchar()">🎤 Hablar</button>

  <script>
    function escuchar() {

      const Reconocimiento =
        window.SpeechRecognition ||
        window.webkitSpeechRecognition;

      if (!Reconocimiento) {
        alert("Tu navegador no permite reconocimiento de voz.");
        return;
      }

      const reconocimiento = new Reconocimiento();

      reconocimiento.lang = "es-CL";
      reconocimiento.continuous = true;
      reconocimiento.interimResults = true;

      reconocimiento.onresult = function(event) {

        let fraseActual = "";

        for (
          let i = event.resultIndex;
          i < event.results.length;
          i++
        ) {
          fraseActual += event.results[i][0].transcript;
        }

        document.getElementById("subtitulo").textContent =
          fraseActual.trim();
      };

      reconocimiento.onerror = function(event) {
        console.log("Error:", event.error);
      };

      reconocimiento.start();
    }
  </script>

</body>
</html>
