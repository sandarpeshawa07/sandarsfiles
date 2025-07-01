<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Sandars Files - Selfie Cam</title>
  <style>
    body, html {
      margin: 0; padding: 0;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      background: black;
      color: white;
      font-family: Arial, sans-serif;
      overflow: hidden;
      flex-direction: column;
    }
    video, canvas {
      width: 100vw;
      height: 100vh;
      object-fit: cover;
      position: absolute;
      top: 0; left: 0;
    }
    #snapBtn, #sendBtn {
      position: relative;
      z-index: 2;
      background-color: rgba(255,255,255,0.2);
      border: 2px solid white;
      border-radius: 50%;
      width: 80px;
      height: 80px;
      font-size: 30px;
      color: white;
      cursor: pointer;
      outline: none;
      margin-bottom: 40px;
      transition: background-color 0.3s ease;
    }
    #snapBtn:hover {
      background-color: rgba(255,255,255,0.4);
    }
    #sendBtn {
      display: none;
      font-size: 16px;
      color: white;
      text-decoration: none;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <video id="video" autoplay playsinline></video>
  <canvas id="canvas" style="display:none;"></canvas>
  <button id="snapBtn">📸</button>
  <a id="sendBtn" download="selfie.png">⬇️ Download</a>

  <script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('canvas');
    const snapBtn = document.getElementById('snapBtn');
    const sendBtn = document.getElementById('sendBtn');
    const ctx = canvas.getContext('2d');

    navigator.mediaDevices.getUserMedia({ video: { facingMode: 'user' } })
      .then(stream => {
        video.srcObject = stream;
      })
      .catch(() => alert('Camera access is needed to use this.'));

    snapBtn.addEventListener('click', () => {
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
      video.style.display = 'none';
      canvas.style.display = 'block';
      snapBtn.style.display = 'none';
      sendBtn.style.display = 'inline-block';
      sendBtn.href = canvas.toDataURL('image/png');
    });
  </script>
</body>
</html>
