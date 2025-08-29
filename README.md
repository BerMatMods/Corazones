<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Día de las Flores Amarillas ✨🌼</title>
  <style>
    body {
      background: linear-gradient(135deg, #2e026d 0%, #ffea00 100%);
      min-height: 100vh;
      margin: 0;
      font-family: 'Montserrat', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      overflow: hidden;
    }
    h1 {
      color: #fff84b;
      text-shadow: 0 0 10px #ffd700, 0 0 20px #fafa63;
      font-size: 2.8em;
      letter-spacing: 2px;
      margin-top: 40px;
      margin-bottom: 10px;
    }
    p {
      color: #fff;
      font-size: 1.3em;
      text-shadow: 0 0 8px #ffd700;
      margin-bottom: 40px;
      background: rgba(50, 50, 50, 0.3);
      padding: 12px 28px;
      border-radius: 32px;
      border: 2px solid #fff84b;
      box-shadow: 0 0 18px #ffd70044;
      max-width: 600px;
    }
    .flowers {
      position: relative;
      width: 85vw;
      height: 55vh;
      margin-bottom: 40px;
    }
    .flower {
      position: absolute;
      width: 60px;
      height: 60px;
      animation: neonGlow 2s infinite alternate;
      filter: drop-shadow(0 0 12px #ffe400);
      cursor: pointer;
      transition: transform 0.2s;
    }
    .flower:hover {
      transform: scale(1.25) rotate(8deg);
      filter: drop-shadow(0 0 28px #fff200) drop-shadow(0 0 8px #fff200);
    }
    /* Animación de neón */
    @keyframes neonGlow {
      0% { filter: drop-shadow(0 0 8px #ffd700); }
      100% { filter: drop-shadow(0 0 20px #fff200); }
    }
    /* Flor con CSS puro */
    .petal {
      position: absolute;
      width: 24px;
      height: 36px;
      border-radius: 50% 50% 40% 40%;
      background: linear-gradient(135deg, #fff84b 60%, #ffd700 100%);
      box-shadow: 0 0 12px #fff84b;
      border: 2px solid #ffec63;
      z-index: 2;
    }
    .petal1 { transform: rotate(0deg) translateY(-18px);}
    .petal2 { transform: rotate(72deg) translateY(-18px);}
    .petal3 { transform: rotate(144deg) translateY(-18px);}
    .petal4 { transform: rotate(216deg) translateY(-18px);}
    .petal5 { transform: rotate(288deg) translateY(-18px);}
    .center {
      position: absolute;
      top: 18px; left: 18px;
      width: 24px; height: 24px;
      background: radial-gradient(circle, #ffe400 75%, #fff200 100%);
      border-radius: 50%;
      border: 3px solid #fff84b;
      box-shadow: 0 0 16px #fff84b, 0 0 30px #ffd700aa;
      z-index: 3;
    }
    /* Tallo */
    .stem {
      position: absolute;
      left: 28px;
      top: 54px;
      width: 4px; height: 36px;
      background: linear-gradient(180deg, #e3ff3c 30%, #46e800 100%);
      border-radius: 2px;
      z-index: 1;
      box-shadow: 0 0 8px #bfff00;
    }
    /* Hoja */
    .leaf {
      position: absolute;
      left: 30px; top: 75px;
      width: 16px; height: 10px;
      background: linear-gradient(90deg, #bfff00 80%, #46e800 100%);
      border-radius: 50% 50% 25% 25%;
      transform: rotate(-25deg);
      box-shadow: 0 0 6px #bfff00;
      z-index: 1;
    }

    /* Responsive */
    @media (max-width: 700px) {
      h1 { font-size: 1.5em;}
      .flowers { width: 98vw; height: 40vh;}
      .flower { width: 38px; height: 38px;}
    }
  </style>
</head>
<body>
  <h1>✨ Día de las Flores Amarillas ✨</h1>
  <p>
    ¡Hoy celebramos el Día de las Flores Amarillas! Te envío este detalle lleno de flores neón para recordarte que la alegría y el cariño florecen como el sol. ¡Que tu día sea brillante y especial! 🌼💛
  </p>
  <div class="flowers">
    <!-- Se generan varias flores en posiciones diferentes -->
    <div class="flower" style="top:16%; left:8%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:40%; left:17%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:25%; left:35%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:52%; left:55%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:10%; left:68%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:60%; left:80%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <div class="flower" style="top:35%; left:85%;">
      <div class="petal petal1"></div>
      <div class="petal petal2"></div>
      <div class="petal petal3"></div>
      <div class="petal petal4"></div>
      <div class="petal petal5"></div>
      <div class="center"></div>
      <div class="stem"></div>
      <div class="leaf"></div>
    </div>
    <!-- Puedes copiar y pegar más flores cambiando las posiciones top/left -->
  </div>
</body>
</html>
