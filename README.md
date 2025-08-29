
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Día de las Flores Amarillas</title>
  <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Montserrat:wght@700&display=swap" rel="stylesheet">
  <style>
    :root {
      --fondo: #181825;
      --amarillo-neon: #ffe900;
      --amarillo-brillo: #fff771;
      --hoja: #69e26c;
      --tallo: #2cce36;
      --mariposa-ala: #fffb00;
      --mariposa-cuerpo: #ffae00;
    }
    body {
      margin: 0;
      padding: 0;
      background: var(--fondo);
      min-height: 100vh;
      overflow-x: hidden;
      font-family: 'Montserrat', sans-serif;
    }
    /* Animación de escritura */
    .carta {
      position: absolute;
      top: 10vw;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(255,255,255,0.1);
      border-radius: 2em;
      box-shadow: 0 8px 32px rgba(255,255,100,0.16);
      padding: 2.5em 3em;
      max-width: 500px;
      width: 90vw;
      color: #fff;
      font-family: 'Great Vibes', cursive;
      font-size: 2.2em;
      letter-spacing: 0.07em;
      border: 3px solid var(--amarillo-brillo);
      backdrop-filter: blur(5px);
      overflow: hidden;
    }
    .carta span {
      opacity: 0;
      animation: escribir 0.17s forwards;
    }
    .carta span:nth-child(n) { animation-delay: calc(var(--i) * 0.09s); }
    @keyframes escribir {
      to { opacity: 1; }
    }
    /* Flores */
    .flores-container {
      position: fixed;
      bottom: 0; left: 0; right: 0;
      height: 48vh;
      pointer-events: none;
      z-index: 1;
    }
    .flor {
      position: absolute;
      bottom: 0;
      transform-origin: bottom center;
      will-change: transform;
      animation: crecer var(--tiempo-flor, 2s) cubic-bezier(.32,1.28,.54,.88) forwards;
      opacity: 0;
      filter: drop-shadow(0 0 14px var(--amarillo-brillo));
    }
    @keyframes crecer {
      0% { transform: scaleY(0.1) scaleX(0.1) translateY(60px); opacity: 0;}
      60% { opacity: 1;}
      100% { transform: scaleY(1) scaleX(1) translateY(0); opacity: 1;}
    }
    /* Estilos SVG flor */
    .flor svg {
      display: block;
      width: var(--tam-flor, 80px);
      height: var(--tam-flor, 80px);
    }
    /* Mariposas */
    .mariposa {
      position: absolute;
      left: 0;
      top: 0;
      width: 48px;
      height: 48px;
      z-index: 2;
      animation: vuelo-mariposa 9s linear infinite;
      will-change: transform;
      pointer-events: none;
    }
    /* Animación aleteo */
    .mariposa .ala {
      transform-origin: 50% 50%;
      animation: aleteo-ala 0.45s infinite alternate;
    }
    @keyframes aleteo-ala {
      to { transform: scaleY(1.14) rotate(-7deg);}
    }
    /* Animación de vuelo (trayectoria) */
    @keyframes vuelo-mariposa {
      0% { transform: translate(var(--x1), var(--y1)) scale(1);}
      15% { transform: translate(var(--x2), var(--y2)) scale(1.01);}
      30% { transform: translate(var(--x3), var(--y3)) scale(1);}
      45% { transform: translate(var(--x4), var(--y4)) scale(1.05);}
      60% { transform: translate(var(--x5), var(--y5)) scale(1);}
      75% { transform: translate(var(--x6), var(--y6)) scale(1.02);}
      100% { transform: translate(var(--x1), var(--y1)) scale(1);}
    }
  </style>
</head>
<body>
  <div class="flores-container" id="flores"></div>
  <div id="mariposas"></div>
  <div class="carta" id="carta"></div>
  <script>
    // CARTA animada
    const textoCarta = `
      ¡Feliz Día de las Flores Amarillas!<br>
      Hoy el mundo se llena de luz, esperanza y alegría.<br>
      Estas flores son símbolo de amor, sueños y nuevos comienzos.<br>
      Que cada pétalo te recuerde lo especial que eres y que la vida florece con tu sonrisa.<br>
      ¡Que el amor y la magia te acompañen siempre!
    `;
    const cartaDiv = document.getElementById('carta');
    cartaDiv.innerHTML = '';
    let i = 0;
    for (const char of textoCarta) {
      const span = document.createElement('span');
      span.textContent = char;
      if (char === '<') { // manejar <br>
        const br = document.createElement('br');
        cartaDiv.appendChild(br);
        continue;
      }
      span.style.setProperty('--i', i);
      cartaDiv.appendChild(span);
      i += 1;
    }

    // GENERAR FLORES AMARILLAS
    const floresDiv = document.getElementById('flores');
    const floresParams = [
      // x%, tamaño, altura, tiempo animación
      [5,  68, 110, 2.1], [12, 100, 160, 2.4], [17, 80, 140, 2.7], [20, 60, 115, 1.9],
      [25, 74, 130, 2.5], [33, 120, 180, 2.8], [38, 95, 140, 2.6], [44, 66, 100, 2.2],
      [50, 105, 170, 3.0], [56, 70, 120, 2.3], [61, 90, 140, 2.6], [67, 65, 110, 2.0],
      [73, 86, 150, 2.7], [80, 110, 180, 2.9], [87, 78, 120, 2.5], [93, 60, 100, 2.1]
    ];
    floresParams.forEach((f, idx) => {
      const flor = document.createElement('div');
      flor.className = 'flor';
      flor.style.left = `${f[0]}vw`;
      flor.style.setProperty('--tam-flor', `${f[1]}px`);
      flor.style.setProperty('--tiempo-flor', `${f[3]}s`);
      flor.innerHTML = `
      <svg viewBox="0 0 80 180">
        <!-- Tallo -->
        <rect x="38" y="60" width="4" height="${f[2]}" rx="2" fill="var(--tallo)" />
        <!-- Hojas -->
        <ellipse cx="32" cy="90" rx="8" ry="24" fill="var(--hoja)" transform="rotate(-25 32 90)" opacity="0.8"/>
        <ellipse cx="48" cy="120" rx="7" ry="22" fill="var(--hoja)" transform="rotate(18 48 120)" opacity="0.7"/>
        <!-- Flor amarilla (pétalos) -->
        <g>
          ${Array.from({length: 7}, (_,i)=>`
            <ellipse cx="40" cy="45" rx="14" ry="20"
              fill="url(#petalo${idx})"
              transform="rotate(${i*360/7} 40 45)" />
            <defs>
              <radialGradient id="petalo${idx}" cx="50%" cy="50%" r="60%">
                <stop offset="0%" stop-color="var(--amarillo-brillo)" />
                <stop offset="60%" stop-color="var(--amarillo-neon)" />
                <stop offset="100%" stop-color="#fff200" />
              </radialGradient>
            </defs>
          `).join('')}
          <!-- Centro -->
          <circle cx="40" cy="45" r="11"
            fill="yellow"
            stroke="#fff800"
            stroke-width="3"
            filter="url(#neon-centro${idx})"
          />
          <defs>
            <filter id="neon-centro${idx}">
              <feDropShadow dx="0" dy="0" stdDeviation="3" flood-color="#fff93e"/>
            </filter>
          </defs>
        </g>
      </svg>
      `;
      floresDiv.appendChild(flor);
    });

    // Animar mariposas
    function crearMariposa(num, colorAla, colorCuerpo) {
      const mariposa = document.createElement('div');
      mariposa.className = 'mariposa';
      // Trayectorias variadas por mariposa
      const trayectorias = [
        [ '7vw', '18vh', '13vw', '10vh', '24vw', '24vh', '35vw', '12vh', '47vw', '21vh', '24vw', '29vh' ],
        [ '63vw', '9vh', '70vw', '24vh', '80vw', '9vh', '90vw', '30vh', '80vw', '35vh', '60vw', '18vh' ],
        [ '28vw', '37vh', '44vw', '21vh', '52vw', '31vh', '56vw', '8vh', '62vw', '33vh', '48vw', '16vh' ],
        [ '88vw', '42vh', '77vw', '27vh', '93vw', '12vh', '81vw', '17vh', '72vw', '39vh', '90vw', '32vh' ]
      ];
      const t = trayectorias[num % trayectorias.length];
      mariposa.style.setProperty('--x1', t[0]);
      mariposa.style.setProperty('--y1', t[1]);
      mariposa.style.setProperty('--x2', t[2]);
      mariposa.style.setProperty('--y2', t[3]);
      mariposa.style.setProperty('--x3', t[4]);
      mariposa.style.setProperty('--y3', t[5]);
      mariposa.style.setProperty('--x4', t[6]);
      mariposa.style.setProperty('--y4', t[7]);
      mariposa.style.setProperty('--x5', t[8]);
      mariposa.style.setProperty('--y5', t[9]);
      mariposa.style.setProperty('--x6', t[10]);
      mariposa.style.setProperty('--y6', t[11]);
      mariposa.style.animationDelay = `${num*1.7}s`;
      mariposa.innerHTML = `
        <svg viewBox="0 0 48 48">
          <g>
            <!-- Alas -->
            <ellipse class="ala" cx="16" cy="18" rx="15" ry="12" fill="${colorAla}" opacity="0.96"/>
            <ellipse class="ala" cx="32" cy="18" rx="15" ry="12" fill="${colorAla}" opacity="0.96"/>
            <!-- Cuerpo -->
            <rect x="22" y="18" width="4.5" height="17" rx="2.3" fill="${colorCuerpo}" />
            <!-- Antenas -->
            <path d="M24 18 Q23 11 16 8" stroke="#f4b800" stroke-width="1.7" fill="none"/>
            <path d="M24 18 Q25 10 32 7" stroke="#f4b800" stroke-width="1.7" fill="none"/>
            <!-- Cabeza -->
            <ellipse cx="24" cy="17" rx="3.2" ry="3.7" fill="${colorCuerpo}" />
          </g>
        </svg>
      `;
      return mariposa;
    }
    const mariposasDiv = document.getElementById('mariposas');
    for (let m=0; m<6; m++) {
      mariposasDiv.appendChild(crearMariposa(m,
        m%2 ? 'gold' : 'var(--mariposa-ala)',
        m%2 ? 'orange' : 'var(--mariposa-cuerpo)'
      ));
    }
  </script>
</body>
</html>
