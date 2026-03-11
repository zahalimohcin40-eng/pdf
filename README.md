<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>عرض PDF بملء الشاشة</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      overflow: hidden;
      background: #000;
    }
    #viewer {
      width: 100%;
      height: 100vh;
    }
    canvas {
      display: block;
      margin: 0 auto;
    }
  </style>
</head>
<body>

<div id="viewer"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.9.179/pdf.min.js"></script>
<script>
const url = 'https://zahalimohcin40-eng.github.io/math/'; // رابط PDF

const container = document.getElementById('viewer');
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.9.179/pdf.worker.min.js';

pdfjsLib.getDocument(url).promise.then(pdf => {
  pdf.getPage(1).then(page => { // يعرض الصفحة الأولى فقط
    const viewport = page.getViewport({ scale: Math.max(window.innerWidth / page.getViewport({ scale:1 }).width, window.innerHeight / page.getViewport({ scale:1 }).height) });
    const canvas = document.createElement('canvas');
    const context = canvas.getContext('2d');
    canvas.width = viewport.width;
    canvas.height = viewport.height;
    container.appendChild(canvas);

    page.render({ canvasContext: context, viewport: viewport });
  });
});
</script>

</body>
</html>
