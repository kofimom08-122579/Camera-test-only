# Camera-test-only
Basic phone camera

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1">
<title>SmartCart Camera Test</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 20px;
    background: #f5f7fa;
  }
  video {
    width: 100%;
    max-width: 500px;
    background: black;
    border-radius: 12px;
  }
  button {
    padding: 15px;
    margin: 10px;
    font-size: 17px;
    border-radius: 8px;
  }
</style>
</head>
<body>
<h2>SmartCart Camera Test</h2>
<p>Testing your POCO phone camera</p>

<video id="camera" autoplay playsinline muted></video>
<br>
<button onclick="startCamera()">Start Camera</button>
<button onclick="stopCamera()">Stop Camera</button>
<p id="status">Camera not started</p>

<script>
let stream = null;

async function startCamera() {
  const status = document.getElementById("status");

  try {
    stopCamera();

    stream = await navigator.mediaDevices.getUserMedia({
      audio: false,
      video: {
        facingMode: { ideal: "environment" }
      }
    });

    document.getElementById("camera").srcObject = stream;
    status.textContent = "Camera working!";
  } catch (error) {
    status.textContent = "Camera error: " + error.message;
  }
}

function stopCamera() {
  if (stream) {
    stream.getTracks().forEach(track => track.stop());
    stream = null;
  }
  document.getElementById("camera").srcObject = null;
}
</script>
</body>
</html>
