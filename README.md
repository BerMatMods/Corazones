
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Para Jhorgina Briyidth</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@1,700&family=Montserrat:wght@400;500&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #0a0a1a;
      color: #fff;
      font-family: 'Montserrat', sans-serif;
      overflow: hidden;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      position: relative;
      touch-action: none;
    }

    /* Fondo estrellado sutil */
    body::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: 
        radial-gradient(1px 1px at 10% 20%, #fff, transparent),
        radial-gradient(1px 1px at 50% 10%, #fff, transparent),
        radial-gradient(1px 1px at 90% 30%, #fff, transparent);
      opacity: 0.1;
    }

    /* Título elegante */
    .titulo {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2.5rem, 5vw, 4rem);
      color: #ffff00;
      text-shadow: 
        0 0 10px #ffff00,
        0 0 20px #ffff00,
        0 0 30px #ffff00,
        0 0 50px #ffff00;
      margin: 20px 20px 30px;
      opacity: 0;
      animation: aparecer 2s forwards 0.5s;
      text-align: center;
      z-index: 10;
    }

    @keyframes aparecer {
      from { opacity: 0; transform: translateY(-50px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Jardín desde el centro inferior */
    .jardin {
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 90%;
      max-width: 1000px;
      display: flex;
      justify-content: center;
      gap: 25px;
      flex-wrap: nowrap;
      z-index: 1;
    }

    /* Flor individual */
    .flor {
      position: relative;
      width: 70px;
      height: 0;
      opacity: 0;
      transform-origin: bottom center;
      transition: transform 0.4s ease-out;
    }

    /* Animación de crecimiento */
    .flor-animada {
      animation: crecer 4s ease-out forwards;
    }

    @keyframes crecer {
      0% { height: 0; opacity: 0; }
      60% { height: 200px; }
      80% { height: 260px; }
      100% { height: calc(var(--altura) * 1px); opacity: 1; }
    }

    /* Tallo realista */
    .tallo {
      position: absolute;
      width: 9px;
      height: 100%;
      background: linear-gradient(to top, #006611, #00cc33 50%, #00aa22);
      bottom: 0;
      left: 30.5px;
      border-radius: 10px 10px 0 0;
      box-shadow: 0 0 15px rgba(0, 200, 50, 0.6);
    }

    /* Hojas */
    .hoja {
      position: absolute;
      width: 38px;
      height: 16px;
      background: #00e639;
      border-radius: 60% 50% 0 50%;
      box-shadow: 0 0 12px rgba(0, 230, 57, 0.8);
      opacity: 0;
    }

    .hoja.izq {
      left: 10px;
      bottom: calc(var(--altura) * 0.35px);
      transform: rotate(-50deg) scale(0);
      animation: hoja-entrar 1s ease-out forwards;
    }
    .hoja.der {
      right: 10px;
      bottom: calc(var(--altura) * 0.55px);
      transform: rotate(50deg) scale(0);
      animation: hoja-entrar 1s ease-out forwards;
    }

    @keyframes hoja-entrar {
      0% { opacity: 0; transform: rotate(-90deg) scale(0); }
      70% { opacity: 0.8; transform: rotate(-50deg) scale(0.9); }
      100% { opacity: 1; transform: rotate(-50deg) scale(1); }
    }

    /* Flor realista (como caléndula) */
    .flor-real {
      position: absolute;
      top: calc(var(--altura) * -0.18px);
      left: 10px;
      width: 52px;
      height: 52px;
      opacity: 0;
      transform-origin: center bottom;
      transition: transform 0.3s ease-out;
    }

    .flor-animada .flor-real {
      animation: abrir-flor 1.4s ease-out forwards;
      animation-delay: 4.2s;
    }

    @keyframes abrir-flor {
      0% { opacity: 0; transform: scale(0.2); }
      100% { opacity: 1; transform: scale(1); }
    }

    /* Pétalos externos (amarillos brillantes) */
    .petalo-ext {
      position: absolute;
      width: 52px;
      height: 24px;
      background: linear-gradient(to bottom, #ffff66, #ffcc00);
      border-radius: 50% 50% 0 0;
      bottom: 0;
      left: 0;
      transform-origin: bottom center;
    }

    .petalo-ext:nth-child(1)  { transform: rotate(0deg); }
    .petalo-ext:nth-child(2)  { transform: rotate(30deg); }
    .petalo-ext:nth-child(3)  { transform: rotate(60deg); }
    .petalo-ext:nth-child(4)  { transform: rotate(90deg); }
    .petalo-ext:nth-child(5)  { transform: rotate(120deg); }
    .petalo-ext:nth-child(6)  { transform: rotate(150deg); }
    .petalo-ext:nth-child(7)  { transform: rotate(180deg); }
    .petalo-ext:nth-child(8)  { transform: rotate(210deg); }
    .petalo-ext:nth-child(9)  { transform: rotate(240deg); }
    .petalo-ext:nth-child(10) { transform: rotate(270deg); }
    .petalo-ext:nth-child(11) { transform: rotate(300deg); }
    .petalo-ext:nth-child(12) { transform: rotate(330deg); }

    /* Pétalos internos (más oscuros) */
    .petalo-int {
      position: absolute;
      width: 42px;
      height: 20px;
      background: linear-gradient(to bottom, #ffcc00, #ff9900);
      border-radius: 50% 50% 0 0;
      bottom: 20px;
      left: 5px;
      transform-origin: bottom center;
    }

    .petalo-int:nth-child(1)  { transform: rotate(0deg); }
    .petalo-int:nth-child(2)  { transform: rotate(45deg); }
    .petalo-int:nth-child(3)  { transform: rotate(90deg); }
    .petalo-int:nth-child(4)  { transform: rotate(135deg); }
    .petalo-int:nth-child(5)  { transform: rotate(180deg); }
    .petalo-int:nth-child(6)  { transform: rotate(225deg); }
    .petalo-int:nth-child(7)  { transform: rotate(270deg); }
    .petalo-int:nth-child(8)  { transform: rotate(315deg); }

    /* Centro de la flor */
    .centro {
      position: absolute;
      width: 22px;
      height: 22px;
      background: #e65100;
      border-radius: 50%;
      bottom: 30px;
      left: 15px;
      box-shadow: 0 0 20px #ff6a00, 0 0 40px #ff6a00;
      animation: latido-centro 2s infinite ease-in-out;
      animation-delay: 0.5s;
    }

    @keyframes latido-centro {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); box-shadow: 0 0 30px #ff6a00, 0 0 60px #ff6a00; }
    }

    /* Carta personalizada */
    .carta {
      position: relative;
      max-width: 90%;
      margin: 20px auto;
      padding: 30px;
      background: rgba(30, 30, 60, 0.85);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      border: 1px solid rgba(255, 255, 0, 0.3);
      box-shadow: 0 0 30px rgba(255, 255, 0, 0.2);
      font-family: 'Playfair Display', serif;
      line-height: 1.9;
      color: #fffef0;
      text-align: center;
      opacity: 0;
      transform: scale(0.7);
      animation: subir-carta 1.6s forwards 8s;
      z-index: 10;
      font-size: clamp(1rem, 4vw, 1.2rem);
    }

    @keyframes subir-carta {
      to { opacity: 1; transform: scale(1); }
    }

    .carta p {
      margin-bottom: 18px;
      opacity: 0;
    }

    .carta p:nth-child(1) { animation: tipo 0.8s forwards; animation-delay: 8.5s; }
    .carta p:nth-child(2) { animation: tipo 1.1s forwards; animation-delay: 9.8s; }
    .carta p:nth-child(3) { animation: tipo 1.1s forwards; animation-delay: 11.3s; }
    .carta p:nth-child(4) { animation: tipo 1.1s forwards; animation-delay: 12.8s; }
    .carta p:nth-child(5) { animation: tipo 0.9s forwards; animation-delay: 14.3s; }

    @keyframes tipo {
      to { opacity: 1; transform: translateY(0); }
    }

    /* Mariposas */
    .mariposa {
      position: absolute;
      width: 30px;
      height: 30px;
      background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23ffff00"><path d="M12 2C8 2 4 5 4 9c0 3 2 5 4 6 1.6 1 3 2 4 2s2.4-1 4-2c2-1 4-3 4-6 0-4-4-7-8-7zm0 10c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2z"/><circle cx="12" cy="9" r="1"/><path d="M7 14c-.5 1-1 2-1 3 0 2 1 3 2 3s2-1 2-3c0-1-.5-2-1-3zm10 0c-.5 1-1 2-1 3 0 2 1 3 2 3s2-1 2-3c0-1-.5-2-1-3z"/></svg>') no-repeat center / contain;
      pointer-events: none;
      z-index: 0;
      opacity: 0.9;
      filter: drop-shadow(0 0 8px #ffff00);
    }

    /* Responsive para celular */
    @media (max-width: 768px) {
      .jardin { gap: 20px; }
      .titulo { font-size: 3rem; }
      .carta { padding: 25px; }
    }
  </style>
</head>
<body>

  <!-- Título -->
  <h1 class="titulo">Para Jhorgina Briyidth</h1>

  <!-- Jardín -->
  <div class="jardin" id="jardin"></div>

  <!-- Carta -->
  <div class="carta">
    <p>Jhorgina Briyidth,</p>
    <p>Cada flor que ves aquí nació pensando en ti. No son perfectas, pero son reales, como el amor que siento. Cada pétalo, cada hoja, cada tallo, crece para saludarte.</p>
    <p>Tu presencia ilumina mi mundo como el sol al amanecer. Tu risa es música, tu mirada es hogar.</p>
    <p>Gracias por existir, por ser quien eres, por llenar mi vida de luz y calma.</p>
    <p>Con todo mi corazón.</p>
  </div>

  <!-- Mariposas -->
  <div id="mariposas"></div>

  <script>
    // Generar flores
    const jardin = document.getElementById('jardin');
    for (let i = 0; i < 16; i++) {
      const altura = Math.floor(Math.random() * 120) + 240; // 240 a 360px
      const delay = (Math.random() * 2 + 0.5).toFixed(2);
      const rotacion = (Math.random() * 10 - 5);

      const flor = document.createElement('div');
      flor.classList.add('flor', 'flor-animada');
      flor.style.setProperty('--altura', altura);
      flor.style.animationDelay = delay + 's';
      flor.style.transform = `rotate(${rotacion}deg)`;
      flor.dataset.x = 0;

      const tallo = document.createElement('div');
      tallo.classList.add('tallo');
      flor.appendChild(tallo);

      const hojaIzq = document.createElement('div');
      hojaIzq.classList.add('hoja', 'izq');
      flor.appendChild(hojaIzq);

      const hojaDer = document.createElement('div');
      hojaDer.classList.add('hoja', 'der');
      flor.appendChild(hojaDer);

      const florReal = document.createElement('div');
      florReal.classList.add('flor-real');

      for (let j = 0; j < 12; j++) {
        const p = document.createElement('div');
        p.classList.add('petalo-ext');
        florReal.appendChild(p);
      }
      for (let j = 0; j < 8; j++) {
        const p = document.createElement('div');
        p.classList.add('petalo-int');
        florReal.appendChild(p);
      }
      const centro = document.createElement('div');
      centro.classList.add('centro');
      florReal.appendChild(centro);

      flor.appendChild(florReal);
      jardin.appendChild(flor);
    }

    // Sigue el mouse/touch
    let clientX = window.innerWidth / 2;
    let clientY = window.innerHeight;

    document.addEventListener('mousemove', e => {
      clientX = e.clientX;
      clientY = e.clientY;
    });

    document.addEventListener('touchmove', e => {
      clientX = e.touches[0].clientX;
      clientY = e.touches[0].clientY;
    }, { passive: true });

    // Movimiento de flores hacia el mouse
    setInterval(() => {
      const flores = document.querySelectorAll('.flor');
      flores.forEach(flor => {
        const rect = flor.getBoundingClientRect();
        const centerX = rect.left + rect.width / 2;
        const centerY = rect.top + rect.height * 0.3;

        const angleX = (clientY - centerY) * 0.0005;
        const angleY = (clientX - centerX) * 0.0005;

        flor.style.transform = `rotate(${angleY * 20 - 5 + (Math.random() * 10 - 5)}deg)`;
        if (flor.querySelector('.flor-real')) {
          flor.querySelector('.flor-real').style.transform = `rotateX(${angleX * 30}deg) rotateY(${angleY * 30}deg)`;
        }
      });
    }, 100);

    // Mariposas volando
    const mariposas = document.getElementById('mariposas');
    for (let i = 0; i < 8; i++) {
      const b = document.createElement('div');
      b.classList.add('mariposa');
      b.style.left = Math.random() * 100 + 'vw';
      b.style.top = Math.random() * 80 + 'vh';
      b.style.animation = `volar ${Math.random() * 10 + 10}s linear infinite`;
      b.style.opacity = 0.7 + Math.random() * 0.3;
      mariposas.appendChild(b);

      // Animación de vuelo
      const keyframes = `
        @keyframes volar {
          0% { transform: translate(0, 0) rotate(0deg); }
          25% { transform: translate(${Math.random()*200-100}px, ${Math.random()*100-50}px) rotate(${Math.random()*360}deg); }
          50% { transform: translate(${Math.random()*200-100}px, ${Math.random()*100-50}px) rotate(${Math.random()*360}deg); }
          75% { transform: translate(${Math.random()*200-100}px, ${Math.random()*100-50}px) rotate(${Math.random()*360}deg); }
          100% { transform: translate(${Math.random()*200-100}px, ${Math.random()*100-50}px) rotate(${Math.random()*360}deg); }
        }
      `;
      const style = document.createElement('style');
      style.textContent = keyframes;
      document.head.appendChild(style);
    }

    // Partículas sutiles
    for (let i = 0; i < 30; i++) {
      const p = document.createElement('div');
      p.style.position = 'absolute';
      p.style.width = '4px';
      p.style.height = '4px';
      p.style.background = '#ffff00';
      p.style.borderRadius = '50%';
      p.style.boxShadow = '0 0 8px #ffff00';
      p.style.left = Math.random() * 100 + 'vw';
      p.style.top = Math.random() * 100 + 'vh';
      p.style.opacity = 0.3;
      p.style.zIndex = 0;
      p.style.pointerEvents = 'none';
      document.body.appendChild(p);
    }
  </script>

</body>
</html>
