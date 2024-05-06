<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CONVERTIDOR DE YOUTUBE A MP3</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #1e1e1e;
      color: #fff;
    }
    .container {
      text-align: center;
    }
    input[type="text"] {
      padding: 10px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      width: 70%;
      margin-bottom: 10px;
    }
    #qualitySelect {
      padding: 10px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      background-color: #363636;
      color: #fff;
    }
    #convertBtn {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      background-color: #007bff;
      color: #fff;
      border: none;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>CONVERTIDOR DE YOUTUBE A MP3</h1>
    <input type="text" id="youtubeUrl" placeholder="INTRODUCE EL ENLACE DE YOUTUBE">
    <select id="qualitySelect">
      <option value="128">Calidad estándar (128kbps)</option>
      <option value="192">Calidad alta (192kbps)</option>
      <option value="320">Calidad superior (320kbps)</option>
    </select>
    <a id="convertLink" href="http://wizardmp3.zzz.com.ua" target="_blank"><button id="convertBtn">CONVERTIR A MP3</button></a>
  </div>

  <script>
    document.getElementById('convertBtn').addEventListener('click', function() {
      var youtubeUrl = document.getElementById('youtubeUrl').value;
      if (youtubeUrl) {
        var youtubeVideoId = getYoutubeVideoId(youtubeUrl);
        if (youtubeVideoId) {
          var quality = document.getElementById('qualitySelect').value;
          var audioUrl = 'https://www.convertmp3.io/download/r/' + youtubeVideoId + '/?quality=' + quality;
          downloadFile(audioUrl);
        } else {
          alert('EL ENLACE DE YOUTUBE NO ES VÁLIDO.');
        }
      } else {
        alert('POR FAVOR INTRODUCE UN ENLACE DE YOUTUBE.');
      }
    });

    function getYoutubeVideoId(url) {
      var videoId = '';
      var regExp = /^.*(youtu\.be\/|v\/|e\/|u\/\w+\/|embed\/|v=)([^#\&\?]*).*/;
      var match = url.match(regExp);
      if (match && match[2].length === 11) {
        videoId = match[2];
      }
      return videoId;
    }

    function downloadFile(url) {
      var fileName = 'audio.mp3';
      var a = document.createElement('a');
      a.href = url;
      a.download = fileName;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
    }
  </script>
</body>
</html>
