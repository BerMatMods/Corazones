
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Yape</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css " rel="stylesheet">
  <style>
    /* ===== VARIABLES GLOBALES ===== */
    :root {
      --yape-green: #00c853;
      --yape-purple: #7b1fa2;
      --yape-blue: #29b6f6;
      --white: #ffffff;
      --text: #333333;
      --text-secondary: #666666;
      --border: #e0e0e0;
      --shadow: 0 4px 12px rgba(0,0,0,0.1);
      --card-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', -apple-system, sans-serif;
    }

    body {
      background-color: var(--yape-purple);
      color: var(--text);
      -webkit-font-smoothing: antialiased;
      overflow-x: hidden;
    }

    .container {
      max-width: 414px;
      margin: 0 auto;
      min-height: 100vh;
      position: relative;
    }

    /* ===== HEADER ===== */
    .top-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 20px 16px;
      color: white;
    }

    .top-bar h1 {
      font-size: 1.5em;
      margin: 0;
    }

    .top-bar .status {
      font-size: 0.8em;
      background: #fbbd00;
      color: black;
      padding: 4px 8px;
      border-radius: 12px;
      font-weight: bold;
    }

    .top-bar .icons {
      display: flex;
      gap: 20px;
    }

    .top-bar .icons i {
      font-size: 1.5em;
      color: white;
    }

    /* ===== OCULTAR HEADER Y MENÚ EN RECIBO ===== */
    #confirmContainer .top-bar,
    #confirmContainer .menu-toggle {
      display: none !important;
    }

    /* ===== MENÚ HAMBURGUESA ===== */
    .menu-toggle {
      position: absolute;
      top: 20px;
      left: 16px;
      font-size: 1.5em;
      color: white;
      cursor: pointer;
      z-index: 100;
    }

    .menu-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 99;
      display: none;
    }

    .menu-sidebar {
      position: fixed;
      top: 0;
      left: 0;
      width: 280px;
      height: 100%;
      background: var(--white);
      z-index: 100;
      transform: translateX(-100%);
      transition: transform 0.3s ease;
      padding: 80px 16px 20px;
      overflow-y: auto;
    }

    .menu-sidebar.active {
      transform: translateX(0);
    }

    .menu-header {
      text-align: center;
      margin-bottom: 20px;
      padding-bottom: 15px;
      border-bottom: 1px solid var(--border);
    }

    .menu-header img {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      margin: 0 auto 10px;
      border: 3px solid var(--yape-purple);
    }

    .menu-header h3 {
      color: var(--yape-purple);
      font-size: 1.2em;
    }

    .menu-item {
      padding: 16px;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 12px;
      color: var(--text);
      cursor: pointer;
      transition: background 0.3s;
    }

    .menu-item:hover {
      background: #f5f5f5;
    }

    .menu-item i {
      color: var(--yape-purple);
      font-size: 1.3em;
    }

    .menu-item .label {
      font-weight: 500;
    }

    .menu-item .desc {
      font-size: 0.8em;
      color: #888;
    }

    /* ===== BANNER PROMOCIONAL (arriba del saldo) ===== */
    .promo-banner-top {
      margin: 20px 20px 0;
      background: var(--white);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: var(--shadow);
    }

    .promo-banner-top img {
      width: 100%;
      height: auto;
      border-radius: 20px;
      display: block;
    }

    /* ===== BANNER EN CONFIRMACIÓN (abajo del recibo) ===== */
    .promo-banner-bottom {
      margin: 20px 20px 15px;
      background: var(--white);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: var(--shadow);
    }

    .promo-banner-bottom img {
      width: 100%;
      height: auto;
      border-radius: 20px;
      display: block;
    }

    /* ===== SERVICIOS ===== */
    .services-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 16px;
      padding: 20px;
    }

    .service-item {
      text-align: center;
      color: white;
      font-size: 0.85em;
    }

    .service-icon {
      width: 70px;
      height: 70px;
      background: white;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: transform 0.2s;
      overflow: hidden;
    }

    .service-icon:hover {
      transform: scale(1.05);
    }

    .service-icon img {
      width: 60%;
      height: 60%;
      object-fit: contain;
    }

    /* ===== SALDO ===== */
    .balance-card {
      background: var(--white);
      border-radius: 20px;
      margin: 15px 20px;
      padding: 20px;
      box-shadow: var(--shadow);
    }

    .balance-toggle {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 16px;
      background: var(--yape-purple);
      border-radius: 12px;
      margin-bottom: 12px;
      cursor: pointer;
    }

    .balance-toggle span {
      color: white;
      font-weight: 600;
    }

    .balance-amount {
      font-size: 2.2em;
      font-weight: bold;
      margin: 10px 0;
    }

    /* ===== MOVIMIENTOS ===== */
    .movements-toggle {
      background: var(--white);
      border-radius: 12px;
      padding: 16px;
      margin: 10px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      cursor: pointer;
      box-shadow: var(--shadow);
    }

    .movements-toggle span {
      color: var(--yape-purple);
      font-weight: 600;
    }

    .movements-toggle i {
      color: var(--yape-purple);
    }

    /* ===== LISTA DE MOVIMIENTOS ===== */
    .movements-list {
      background: var(--white);
      border-radius: 20px;
      margin: 15px 20px;
      padding: 10px 0;
      box-shadow: var(--shadow);
      max-height: 300px;
      overflow-y: auto;
    }

    .movement-item {
      padding: 14px 16px;
      display: flex;
      align-items: center;
      border-bottom: 1px solid #f0f0f0;
    }

    .movement-icon {
      width: 50px;
      height: 50px;
      background: #f0f0f0;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 12px;
    }

    .movement-icon i {
      color: var(--yape-green);
      font-size: 1.3em;
    }

    .movement-info {
      flex: 1;
    }

    .movement-name {
      font-weight: 600;
      color: var(--text);
      margin-bottom: 4px;
    }

    .movement-date {
      font-size: 0.85em;
      color: var(--text-secondary);
    }

    .movement-amount {
      font-weight: bold;
      color: var(--yape-green);
    }

    /* ===== BOTONES GRANDES (en fila horizontal, tamaño original) ===== */
    .buttons-row {
      display: flex;
      gap: 16px;
      padding: 0 20px;
      margin: 20px 0;
    }

    .big-button {
      flex: 1;
      background: var(--yape-blue);
      color: white;
      border: none;
      padding: 14px;
      border-radius: 12px;
      font-size: 1.1em;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 6px;
      box-shadow: 0 4px 12px rgba(41, 182, 246, 0.3);
    }

    .big-button.yapear {
      background: var(--yape-green);
      box-shadow: 0 4px 12px rgba(0, 200, 83, 0.3);
    }

    .big-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(41, 182, 246, 0.4);
    }

    .big-button.yapear:hover {
      box-shadow: 0 6px 16px rgba(0, 200, 83, 0.4);
    }

    .big-button i {
      font-size: 1.2em;
    }

    .big-button span {
      font-size: 0.9em;
      margin-top: 4px;
    }

    /* ===== PANTALLA: INGRESAR NÚMERO Y MONTO ===== */
    .send-screen {
      background: var(--white);
      border-radius: 20px;
      margin: 20px 20px 15px;
      padding: 20px;
      box-shadow: var(--shadow);
      display: none;
    }

    .send-title {
      font-size: 1.4em;
      color: var(--yape-purple);
      margin-bottom: 16px;
    }

    .send-input {
      width: 100%;
      padding: 12px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 1em;
      margin: 10px 0;
    }

    .send-amount {
      font-size: 2.5em;
      font-weight: bold;
      margin: 15px 0;
      text-align: center;
    }

    .send-buttons {
      display: flex;
      gap: 10px;
      margin-top: 15px;
    }

    .send-btn {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 8px;
      font-size: 1em;
      cursor: pointer;
    }

    .send-btn.cancel {
      background: #f5f5f5;
      color: var(--text);
    }

    .send-btn.send {
      background: var(--yape-green);
      color: white;
    }

    /* ===== PANTALLA DE CONFIRMACIÓN (¡Yapeaste!) ===== */
    .confirm-container {
      display: none;
      margin: 20px 20px 15px;
      position: relative;
    }

    /* ✅ ICONO X (cerrar) - más arriba, en la esquina superior derecha de la pantalla */
    .global-close {
      position: absolute;
      top: 15px;
      right: 16px;
      color: white;
      font-size: 1.5em;
      background: rgba(0,0,0,0.3);
      width: 36px;
      height: 36px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      z-index: 10;
    }

    /* ✅ RECIBO BLANCO - con datos reales */
    .confirm-screen {
      background: var(--white);
      border-radius: 20px;
      padding: 16px;
      box-shadow: var(--shadow);
      font-family: 'Segoe UI', sans-serif;
      margin-top: 60px; /* Espacio para el X arriba */
    }

    .confirm-title {
      font-size: 1.3em;
      color: var(--yape-purple);
      font-weight: bold;
      margin: 0;
    }

    .confirm-amount {
      font-size: 2.8em;
      font-weight: bold;
      margin: 10px 0;
      text-align: center;
      color: var(--text);
    }

    .confirm-name {
      font-size: 1.2em;
      font-weight: bold;
      margin: 10px 0;
      text-align: center;
      color: var(--text);
    }

    .confirm-date {
      font-size: 0.9em;
      color: var(--text-secondary);
      margin-bottom: 20px;
      text-align: center;
    }

    .security-code {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin: 15px 0;
      padding-bottom: 15px;
      border-bottom: 1px solid var(--border);
    }

    .security-code span {
      font-size: 0.9em;
      color: var(--text-secondary);
      font-weight: bold;
    }

    .security-code i {
      color: var(--yape-green);
      font-size: 1.2em;
    }

    .security-digits {
      display: flex;
      gap: 10px;
    }

    .digit {
      width: 40px;
      height: 40px;
      background: #f0f0f0;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      color: var(--text);
    }

    .confirm-details {
      margin-top: 20px;
      font-size: 0.95em;
      color: var(--text-secondary);
      text-align: left;
    }

    .detail-row {
      display: flex;
      justify-content: space-between;
      margin: 10px 0;
      font-weight: bold;
    }

    /* ✅ BOTÓN COMPARTIR - en la esquina superior derecha del recibo */
    .share-inside {
      position: absolute;
      top: 16px;
      right: 16px;
      background: #f0f0f0;
      border: none;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--yape-purple);
      font-size: 1.2em;
      cursor: pointer;
    }

    /* ===== ESCANEO QR ===== */
    .scan-screen {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #000;
      z-index: 1000;
      justify-content: center;
      align-items: center;
    }

    .scan-overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
    }

    .scan-frame {
      width: 290px;
      height: 290px;
      border: 3px solid #00ff00;
      border-radius: 18px;
      position: relative;
      z-index: 2;
      overflow: hidden;
      box-shadow: 0 0 25px rgba(0,255,0,0.5);
    }

    .scan-line {
      width: 100%;
      height: 5px;
      background: #00ff00;
      position: absolute;
      top: 0;
      animation: scanLine 1.6s ease-in-out infinite;
      box-shadow: 0 0 15px #00ff00;
    }

    @keyframes scanLine {
      0% { top: 0; }
      100% { top: 285px; }
    }

    .scan-close {
      position: absolute;
      top: 20px;
      right: 20px;
      background: white;
      color: black;
      width: 44px;
      height: 44px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 3;
      cursor: pointer;
    }

    /* ===== CHISPAS ===== */
    .sparkles {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1001;
      display: none;
    }

    .spark {
      position: absolute;
      width: 10px;
      height: 10px;
      background: #fff;
      border-radius: 50%;
      opacity: 0.8;
      animation: fall linear forwards;
    }

    @keyframes fall {
      0% { transform: translateY(-20px); opacity: 1; }
      100% { transform: translateY(100vh); opacity: 0; }
    }

    /* ===== PANTALLAS ===== */
    .screen {
      display: none;
    }

    .screen.active {
      display: block;
    }

    /* ===== FOOTER ===== */
    .footer {
      text-align: center;
      padding: 20px 0;
      color: #aaa;
      font-size: 0.8em;
    }

    /* ===== PANTALLA: INFORMACIÓN DE LA APP ===== */
    .info-screen {
      display: none;
      background: var(--white);
      border-radius: 20px;
      margin: 30px 20px;
      padding: 25px 20px;
      box-shadow: var(--shadow);
      text-align: center;
      max-width: 370px;
      font-family: 'Segoe UI', sans-serif;
    }

    .info-screen h2 {
      color: var(--yape-purple);
      font-size: 1.5em;
      margin-bottom: 8px;
    }

    .info-screen p {
      color: var(--text);
      font-size: 1em;
      margin: 8px 0;
    }

    .info-screen .dev-name {
      font-weight: 600;
      color: var(--yape-green);
      font-size: 1.1em;
    }

    .info-screen .github-link {
      margin-top: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      color: var(--yape-purple);
      text-decoration: none;
      font-weight: 600;
      font-size: 0.95em;
    }

    .info-screen .github-link img {
      width: 24px;
      height: 24px;
      vertical-align: middle;
    }

    .info-screen .footer-text {
      color: #888;
      font-size: 0.85em;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <div class="container">

    <!-- Menú hamburguesa -->
    <div class="menu-toggle" onclick="toggleMenu()">
      <i class="fas fa-bars"></i>
    </div>

    <div class="menu-overlay" id="menuOverlay" onclick="toggleMenu()"></div>

    <div class="menu-sidebar" id="menuSidebar">
      <div class="menu-header">
        <img src="https://ui-avatars.com/api/?name=AnthZz+Berrocal&background=7b1fa2&color=fff" alt="Perfil" id="menuProfilePic">
        <h3 id="menuName">AnthZz Berrocal</h3>
        <p>_BerMat_Mods</p>
      </div>

      <div class="menu-item" onclick="showScreen('profile')">
        <i class="fas fa-user"></i>
        <div>
          <div class="label">Perfil</div>
          <div class="desc">Editar información</div>
        </div>
      </div>

      <div class="menu-item" onclick="showScreen('editBalance')">
        <i class="fas fa-wallet"></i>
        <div>
          <div class="label">Editar Saldo</div>
          <div class="desc">S/ <span id="menuBalance">27.00</span></div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Créditos')">
        <i class="fas fa-hand-holding-usd"></i>
        <div>
          <div class="label">Créditos</div>
          <div class="desc">S/ 8000 disponibles</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Promociones')">
        <i class="fas fa-percent"></i>
        <div>
          <div class="label">Promociones</div>
          <div class="desc">Ofertas exclusivas</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Notificaciones')">
        <i class="fas fa-bell"></i>
        <div>
          <div class="label">Notificaciones</div>
          <div class="desc">Activadas</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Seguridad')">
        <i class="fas fa-shield-alt"></i>
        <div>
          <div class="label">Seguridad</div>
          <div class="desc">PIN, huella, facial</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Soporte')">
        <i class="fas fa-headset"></i>
        <div>
          <div class="label">Soporte</div>
          <div class="desc">Chatea con nosotros</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Ayuda')">
        <i class="fas fa-question-circle"></i>
        <div>
          <div class="label">Ayuda</div>
          <div class="desc">Centro de ayuda</div>
        </div>
      </div>

      <!-- NUEVO: Información de la app -->
      <div class="menu-item" onclick="showScreen('infoScreen')">
        <i class="fas fa-info-circle"></i>
        <div>
          <div class="label">Información de la app</div>
          <div class="desc">Detalles del desarrollo</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Términos')">
        <i class="fas fa-file-alt"></i>
        <div>
          <div class="label">Términos y condiciones</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Privacidad')">
        <i class="fas fa-lock"></i>
        <div>
          <div class="label">Privacidad</div>
        </div>
      </div>

      <div class="menu-item" onclick="alert('Cerrar sesión')">
        <i class="fas fa-sign-out-alt"></i>
        <div>
          <div class="label">Cerrar sesión</div>
        </div>
      </div>
    </div>

    <!-- Header -->
    <div class="top-bar">
      <i class="fas fa-user"></i>
      <h1 id="greeting">Hola, AnthZz</h1>
      <span class="status">Gratis</span>
      <div class="icons">
        <i class="fas fa-headset"></i>
        <i class="fas fa-bell"></i>
      </div>
    </div>

    <!-- Pantalla: Inicio -->
    <div id="home" class="screen active">
      <div class="services-grid">
        <!-- Recargar celular -->
        <div class="service-item" onclick="startScan()">
          <div class="service-icon">
            <img src=" https://i.postimg.cc/9FzMzGFm/Screenshot-20250823-104637.jpg " alt="Recargar celular">
          </div>
          <div>Recargar celular</div>
        </div>

        <!-- Yapear servicios -->
        <div class="service-item" onclick="alert('Yapear servicios')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/QCvrFK0C/Screenshot-20250823-104730.jpg " alt="Yapear servicios">
          </div>
          <div>Yapear servicios</div>
        </div>

        <!-- Promos -->
        <div class="service-item" onclick="alert('Promos')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/DwrKzZsf/Screenshot-20250823-104820.jpg " alt="Promos">
          </div>
          <div>Promos</div>
        </div>

        <!-- Aprobar compras -->
        <div class="service-item" onclick="alert('Aprobar compras')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/Y9y5PmcR/Screenshot-20250823-104906.jpg " alt="Aprobar compras">
          </div>
          <div>Aprobar compras</div>
        </div>

        <!-- Créditos -->
        <div class="service-item" onclick="alert('Créditos')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/xTHdK9Hh/Screenshot-20250823-104933.jpg " alt="Créditos">
          </div>
          <div>Créditos</div>
        </div>

        <!-- Tienda -->
        <div class="service-item" onclick="alert('Tienda')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/pT42FSdP/Screenshot-20250823-105003.jpg " alt="Tienda">
          </div>
          <div>Tienda</div>
        </div>

        <!-- Dólares -->
        <div class="service-item" onclick="alert('Dólares')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/jjB9QYy3/Screenshot-20250823-105020.jpg " alt="Dólares">
          </div>
          <div>Dólares</div>
        </div>

        <!-- Remesas -->
        <div class="service-item" onclick="alert('Remesas')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/wvJrw4Vq/Screenshot-20250823-105050.jpg " alt="Remesas">
          </div>
          <div>Remesas</div>
        </div>

        <!-- SOAT -->
        <div class="service-item" onclick="alert('SOAT')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/RZFbkZRb/Screenshot-20250823-105128.jpg " alt="SOAT">
          </div>
          <div>SOAT</div>
        </div>

        <!-- Viajar en bus -->
        <div class="service-item" onclick="alert('Viajar en bus')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/63sj4LND/Screenshot-20250823-105147.jpg " alt="Viajar en bus">
          </div>
          <div>Viajar en bus</div>
        </div>

        <!-- Biométrica -->
        <div class="service-item" onclick="alert('Biométrica')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/qq41jJqw/Screenshot-20250823-105211.jpg " alt="Biométrica">
          </div>
          <div>Biométrica</div>
        </div>

        <!-- Ver todo -->
        <div class="service-item" onclick="alert('Ver todo')">
          <div class="service-icon">
            <img src="https://i.postimg.cc/RVPgLzB1/Screenshot-20250823-105316.jpg " alt="Ver todo">
          </div>
          <div>Ver todo</div>
        </div>
      </div>

      <!-- Imagen 1: arriba del saldo -->
      <div class="promo-banner-top">
        <img src="https://i.postimg.cc/85Mf0TWF/1755961504718.jpg " alt="Promoción">
      </div>

      <div class="balance-card">
        <div class="balance-toggle" onclick="toggleBalance()">
          <span>Ocultar saldo</span>
          <span id="balanceAmount">S/ 2866</span>
        </div>
      </div>

      <!-- Movimientos: Mostrar lista -->
      <div class="movements-toggle" onclick="showScreen('movementsList')">
        <span>Mostrar movimientos</span>
        <i class="fas fa-chevron-down"></i>
      </div>

      <!-- Lista de movimientos -->
      <div id="movementsList" class="screen movements-list" style="display:none;">
        <!-- Se llena con JavaScript -->
      </div>

      <!-- Botones en fila horizontal -->
      <div class="buttons-row">
        <button class="big-button" onclick="startScan()">
          <i class="fas fa-qrcode"></i>
          <span>ESCANEAR QR</span>
        </button>
        <button class="big-button yapear" onclick="showSendScreen()">
          <i class="fas fa-paper-plane"></i>
          <span>YAPEAR</span>
        </button>
      </div>
    </div>

    <!-- Pantalla: Ingresar número y monto -->
    <div id="sendScreen" class="screen send-screen">
      <div class="send-title">¿A quién vas a yapear?</div>
      <input type="tel" id="sendPhone" placeholder="987 654 321" class="send-input">
      <div class="send-title">Nombre del destinatario</div>
      <input type="text" id="sendName" placeholder="AnthZz Berrocal" value="AnthZz Berrocal" class="send-input">
      <div class="send-title">¿Cuánto?</div>
      <div class="send-amount">S/ <span id="sendAmount">0.00</span></div>
      <input type="number" id="amountInput" placeholder="0.00" class="send-input" oninput="updateAmount(this.value)">
      <div class="send-buttons">
        <button class="send-btn cancel" onclick="goBack()">Cancelar</button>
        <button class="send-btn send" onclick="confirmSend()">Yapear</button>
      </div>
    </div>

    <!-- Contenido: Recibo + Anuncio -->
    <div id="confirmContainer" class="screen confirm-container">
      <!-- ✅ X (cerrar) - más arriba, en la esquina superior derecha de la pantalla -->
      <div class="global-close" onclick="goBack()">
        <i class="fas fa-times"></i>
      </div>

      <!-- Recibo de pago -->
      <div class="confirm-screen">
        <!-- ✅ Botón de compartir DENTRO del recibo -->
        <button class="share-inside" onclick="alert('Compartir recibo')">
          <i class="fas fa-share-alt"></i>
        </button>

        <div class="confirm-title">¡Yapeaste!</div>
        <div class="confirm-amount">S/ <span id="confirmAmount">1</span></div>
        <div class="confirm-name"><span id="confirmName">AnthZz Berrocal</span></div>
        <div class="confirm-date">
          <i class="fas fa-calendar"></i> <span id="confirmDate">22 ago. 2025</span> | <i class="fas fa-clock"></i> <span id="confirmTime">10:35 p.m.</span>
        </div>

        <div class="security-code">
          <span>CÓDIGO DE SEGURIDAD</span>
          <i class="fas fa-info-circle"></i>
          <div class="security-digits">
            <div class="digit" id="code1">4</div>
            <div class="digit" id="code2">6</div>
            <div class="digit" id="code3">4</div>
          </div>
        </div>

        <div class="confirm-details">
          <div class="detail-row">
            <span>Nro. de celular</span>
            <span id="confirmPhone">*** *** 777</span>
          </div>
          <div class="detail-row">
            <span>Destino</span>
            <span>Yape</span>
          </div>
          <div class="detail-row">
            <span>Nro. de operación</span>
            <span id="confirmOp">25422464</span>
          </div>
        </div>
      </div>

      <!-- Imagen 2: anuncio del iPhone -->
      <div class="promo-banner-bottom">
        <img src="https://i.postimg.cc/FRNhhv8k/1755961471955.jpg " alt="iPhone 16e">
      </div>
    </div>

    <!-- Pantalla: Perfil -->
    <div id="profile" class="screen" style="display:none; padding:20px;">
      <h2 style="color:var(--yape-purple); margin:20px 0;">Editar Perfil</h2>
      <img src="https://ui-avatars.com/api/?name=AnthZz+Berrocal&background=7b1fa2&color=fff" alt="Foto" class="profile-pic" id="profilePic" onclick="changePhoto()" style="width:80px; height:80px; border-radius:50%; margin:20px auto; display:block; border:3px solid var(--yape-purple);">
      <div style="margin:15px 0;">
        <label style="display:block; margin-bottom:8px; color:#333;">Nombre completo</label>
        <input type="text" id="editName" value="AnthZz Berrocal" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
      </div>
      <div style="margin:15px 0;">
        <label style="display:block; margin-bottom:8px; color:#333;">Apodo</label>
        <input type="text" id="editNickname" value="_BerMat_Mods" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
      </div>
      <div style="margin:15px 0;">
        <label style="display:block; margin-bottom:8px; color:#333;">Email</label>
        <input type="email" id="editEmail" value="anthzz@bermatmods.dev" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
      </div>
      <div style="margin:15px 0;">
        <label style="display:block; margin-bottom:8px; color:#333;">Teléfono</label>
        <input type="tel" id="editPhone" value="+51 999 888 777" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
      </div>
      <button class="big-button" onclick="saveProfile()">Guardar Cambios</button>
      <button class="big-button secondary" style="margin-top:10px;" onclick="goBack()">← Volver</button>
    </div>

    <!-- Pantalla: Editar Saldo -->
    <div id="editBalance" class="screen" style="display:none; padding:20px;">
      <h2 style="color:var(--yape-purple); margin:20px 0;">Editar Saldo</h2>
      <div style="margin:15px 0;">
        <label style="display:block; margin-bottom:8px; color:#333;">Saldo actual (S/)</label>
        <input type="number" id="editBalanceInput" value="27.00" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
      </div>
      <button class="big-button" onclick="saveBalance()">Guardar Saldo</button>
      <button class="big-button secondary" style="margin-top:10px;" onclick="goBack()">← Volver</button>
    </div>

    <!-- Pantalla: Información de la app -->
    <div id="infoScreen" class="info-screen">
      <h2>Yape Fake v2.5</h2>
      <p>Desarrollado por</p>
      <p class="dev-name">AnthZz Berrocal _BerMat_Mods</p>
      <p>Versión más reciente lanzada por BerMatMods</p>
      <hr style="border:1px solid #e0e0e0; margin:20px 0;">
      <a href=" https://github.com/BerMatMods " target="_blank" class="github-link">
        <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png " alt="GitHub">
        Ver más en GitHub
      </a>
      <p class="footer-text">Somos legión no olvides,Esperanos</p>
      <button class="big-button secondary" style="margin-top:20px; width:100%;" onclick="goBack()">
        <i class="fas fa-arrow-left"></i> Volver
      </button>
    </div>

    <!-- Escaneo QR -->
    <div id="scanScreen" class="scan-screen">
      <div class="scan-overlay"></div>
      <div class="scan-frame">
        <div class="scan-line"></div>
      </div>
      <div class="scan-close" onclick="closeScan()">
        <i class="fas fa-times"></i>
      </div>
    </div>

    <!-- Chispas -->
    <div class="sparkles" id="sparkles"></div>

    <!-- Footer -->
    <div class="footer">
      <strong>by AnthZz Berrocal _BerMat_Mods</strong>
    </div>

  </div>

  <script>
    let balance = 27.00;
    let balanceVisible = false;
    let userName = "AnthZz";
    let userProfile = {
      name: "AnthZz Berrocal",
      nickname: "_BerMat_Mods",
      email: "anthzz@bermatmods.dev",
      phone: "+51 999 888 777",
      photo: "https://ui-avatars.com/api/?name=AnthZz+Berrocal&background=7b1fa2&color=fff"
    };

    // Historial de movimientos
    let movements = JSON.parse(localStorage.getItem('yape_movements')) || [];

    function toggleMenu() {
      const sidebar = document.getElementById('menuSidebar');
      const overlay = document.getElementById('menuOverlay');
      sidebar.classList.toggle('active');
      overlay.style.display = sidebar.classList.contains('active') ? 'block' : 'none';
    }

    function toggleBalance() {
      const elem = document.getElementById('balanceAmount');
      if (balanceVisible) {
        elem.textContent = `S/ ${balance.toFixed(2)}`;
        document.querySelector('.balance-toggle span:nth-child(1)').textContent = 'Ocultar saldo';
        balanceVisible = false;
      } else {
        elem.textContent = '●●●●●●';
        document.querySelector('.balance-toggle span:nth-child(1)').textContent = 'Mostrar saldo';
        balanceVisible = true;
      }
    }

    function startScan() {
      document.getElementById('scanScreen').style.display = 'flex';
      setTimeout(() => {
        closeScan();
        const amount = (Math.random() * 60 + 10).toFixed(2);
        showSparkles();
        setTimeout(() => {
          alert(`✅ Pago realizado\nMonto: S/ ${amount}`);
          balance -= parseFloat(amount);
          document.getElementById('balanceAmount').textContent = `S/ ${balance.toFixed(2)}`;
          document.getElementById('menuBalance').textContent = balance.toFixed(2);
          addMovement('Pago realizado', '*** *** 777', amount);
        }, 500);
      }, 2500);
    }

    function closeScan() {
      document.getElementById('scanScreen').style.display = 'none';
    }

    function showSendScreen() {
      document.getElementById('sendPhone').value = '';
      document.getElementById('sendName').value = 'AnthZz Berrocal';
      document.getElementById('amountInput').value = '';
      document.getElementById('sendAmount').textContent = '0.00';
      showScreen('sendScreen');
    }

    function updateAmount(value) {
      document.getElementById('sendAmount').textContent = value || '0.00';
    }

    function confirmSend() {
      const phone = document.getElementById('sendPhone').value;
      const name = document.getElementById('sendName').value;
      const amount = document.getElementById('sendAmount').textContent;
      if (!phone || phone.length < 9) {
        alert("Número inválido");
        return;
      }
      if (!amount || amount === '0.00') {
        alert("Ingresa un monto válido");
        return;
      }
      showConfirm(phone, name, amount);
    }

    function showConfirm(phone, name, amount) {
      showScreen('confirmContainer');
      document.getElementById('confirmAmount').textContent = amount;
      document.getElementById('confirmName').textContent = name;
      const now = new Date();
      const months = ['ene', 'feb', 'mar', 'abr', 'may', 'jun', 'jul', 'ago', 'sep', 'oct', 'nov', 'dic'];
      const month = months[now.getMonth()];
      const day = now.getDate();
      const year = now.getFullYear();
      const hour = now.getHours();
      const minutes = now.getMinutes().toString().padStart(2, '0');
      const ampm = hour >= 12 ? 'p.m.' : 'a.m.';
      const hour12 = hour % 12 || 12;
      document.getElementById('confirmDate').textContent = `${day} ${month}. ${year}`;
      document.getElementById('confirmTime').textContent = `${hour12}:${minutes} ${ampm}`;
      document.getElementById('code1').textContent = Math.floor(Math.random() * 10);
      document.getElementById('code2').textContent = Math.floor(Math.random() * 10);
      document.getElementById('code3').textContent = Math.floor(Math.random() * 10);
      document.getElementById('confirmPhone').textContent = `*** *** ${phone.slice(-3)}`;
      document.getElementById('confirmOp').textContent = Math.floor(Math.random() * 90000000 + 10000000);
      showSparkles();

      // Registrar movimiento completo
      addMovement(name, phone, amount);
    }

    function addMovement(name, phone, amount) {
      const now = new Date();
      const date = now.toLocaleDateString('es-PE', { day: '2-digit', month: 'short', year: 'numeric' }).replace('.', '');
      const time = now.toLocaleTimeString('es-PE', { hour: '2-digit', minute: '2-digit', hour12: true });
      const operation = Math.floor(Math.random() * 90000000 + 10000000);

      const movement = {
        name: name,
        phone: `*** *** ${phone.slice(-3)}`,
        amount: amount,
        date: `${date} ${time}`,
        operation: operation
      };

      movements.unshift(movement);
      localStorage.setItem('yape_movements', JSON.stringify(movements));
      renderMovements();
    }

    function renderMovements() {
      const container = document.getElementById('movementsList');
      container.innerHTML = '';

      if (movements.length === 0) {
        container.innerHTML = '<div style="text-align:center; color:#888; padding:20px;">No tienes movimientos aún</div>';
        return;
      }

      movements.forEach(mov => {
        const item = document.createElement('div');
        item.className = 'movement-item';
        item.innerHTML = `
          <div class="movement-icon">
            <i class="fas fa-paper-plane"></i>
          </div>
          <div class="movement-info">
            <div class="movement-name">${mov.name}</div>
            <div class="movement-date">${mov.date}</div>
          </div>
          <div class="movement-amount">S/ ${mov.amount}</div>
        `;
        container.appendChild(item);
      });
    }

    function goBack() {
      showScreen('home');
    }

    function showScreen(id) {
      document.querySelectorAll('.screen').forEach(s => s.style.display = 'none');
      document.getElementById(id).style.display = 'block';
      if (id === 'movementsList') {
        renderMovements();
      }
    }

    function changePhoto() {
      const url = prompt('Ingresa URL de foto (o deja vacío para avatar)', '');
      if (url && url.trim() !== '') {
        userProfile.photo = url.trim();
      } else {
        const name = document.getElementById('editName').value || 'AnthZz Berrocal';
        userProfile.photo = ` https://ui-avatars.com/api/?name=${encodeURIComponent(name)}&background=7b1fa2&color=fff`;
      }
      document.getElementById('profilePic').src = userProfile.photo;
      document.getElementById('menuProfilePic').src = userProfile.photo;
    }

    function saveProfile() {
      const name = document.getElementById('editName').value;
      const nickname = document.getElementById('editNickname').value;
      const email = document.getElementById('editEmail').value;
      const phone = document.getElementById('editPhone').value;
      if (!name || !email || !phone) {
        alert('Completa todos los campos');
        return;
      }
      userProfile.name = name;
      userProfile.nickname = nickname;
      userProfile.email = email;
      userProfile.phone = phone;
      userName = name.split(' ')[0];
      document.getElementById('greeting').textContent = `Hola, ${userName}`;
      document.getElementById('menuName').textContent = name;
      alert('✅ Perfil actualizado');
      goBack();
    }

    function saveBalance() {
      const newBalance = parseFloat(document.getElementById('editBalanceInput').value);
      if (isNaN(newBalance) || newBalance < 0) {
        alert('Ingresa un saldo válido');
        return;
      }
      balance = newBalance;
      document.getElementById('balanceAmount').textContent = `S/ ${balance.toFixed(2)}`;
      document.getElementById('menuBalance').textContent = balance.toFixed(2);
      alert('✅ Saldo actualizado');
      goBack();
    }

    function showSparkles() {
      const container = document.getElementById('sparkles');
      container.style.display = 'block';
      for (let i = 0; i < 30; i++) {
        setTimeout(() => {
          const spark = document.createElement('div');
          spark.classList.add('spark');
          spark.style.left = Math.random() * 100 + 'vw';
          spark.style.opacity = Math.random();
          spark.style.width = spark.style.height = (Math.random() * 10 + 5) + 'px';
          spark.style.animationDuration = (Math.random() * 2 + 1) + 's';
          container.appendChild(spark);
          setTimeout(() => spark.remove(), 3000);
        }, i * 50);
      }
      setTimeout(() => container.style.display = 'none', 3000);
    }

    window.addEventListener('load', () => {
      showScreen('home');
      renderMovements();
    });
  </script>

  <!-- ===== AÑADIDO: RECIBO "TE YAPEARON" EDITABLE DESDE EL MENÚ ===== -->
  <script>
    // Añadir opción "Editar Te yapearon" al menú sin tocar HTML original
    const menuItems = document.querySelector('.menu-sidebar');
    const newItem = document.createElement('div');
    newItem.className = 'menu-item';
    newItem.onclick = () => showScreen('editReceive');
    newItem.innerHTML = `
      <i class="fas fa-exchange-alt"></i>
      <div>
        <div class="label">Editar "Te yapearon"</div>
        <div class="desc">Personaliza el recibo</div>
      </div>
    `;
    menuItems.appendChild(newItem);
  </script>

  <!-- RECIBO: Te yapearon -->
  <div id="receiveContainer" class="screen" style="display:none; position:relative;">
    <div class="global-close" onclick="goBack()">
      <i class="fas fa-times"></i>
    </div>
    <div class="confirm-screen">
      <button class="share-inside" onclick="alert('Compartir recibo')">
        <i class="fas fa-share-alt"></i>
      </button>
      <div class="confirm-title">¡Te yapearon!</div>
      <div class="confirm-amount">S/ <span id="receiveAmount">100.00</span></div>
      <div class="confirm-name"><span id="receiveName">Luis Gómez</span></div>
      <div class="confirm-date">
        <i class="fas fa-calendar"></i> <span id="receiveDate">23 ago. 2025</span> | 
        <i class="fas fa-clock"></i> <span id="receiveTime">09:15 a.m.</span>
      </div>
      <div class="security-code">
        <span>CÓDIGO DE SEGURIDAD</span>
        <i class="fas fa-info-circle"></i>
        <div class="security-digits">
          <div class="digit" id="rcvCode1">3</div>
          <div class="digit" id="rcvCode2">7</div>
          <div class="digit" id="rcvCode3">1</div>
        </div>
      </div>
      <div class="confirm-details">
        <div class="detail-row">
          <span>Nro. de celular</span>
          <span id="receivePhone">*** *** 456</span>
        </div>
        <div class="detail-row">
          <span>Origen</span>
          <span>Yape</span>
        </div>
        <div class="detail-row">
          <span>Nro. de operación</span>
          <span id="receiveOp">87654321</span>
        </div>
      </div>
    </div>
    <div class="promo-banner-bottom">
      <img src="https://i.postimg.cc/FRNhhv8k/1755961471955.jpg" alt="iPhone 16e">
    </div>
  </div>

  <!-- PANTALLA: Editar "Te yapearon" -->
  <div id="editReceive" class="screen" style="display:none; padding:20px; background:white; border-radius:20px; margin:20px;">
    <h2 style="color:var(--yape-purple); margin:20px 0;">Editar "Te yapearon"</h2>
    <div style="margin:15px 0;">
      <label style="display:block; margin-bottom:8px; color:#333;">Nombre del que te yapeó</label>
      <input type="text" id="editReceiveName" value="Luis Gómez" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
    </div>
    <div style="margin:15px 0;">
      <label style="display:block; margin-bottom:8px; color:#333;">Monto (S/)</label>
      <input type="number" step="0.01" id="editReceiveAmount" value="100.00" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
    </div>
    <div style="margin:15px 0;">
      <label style="display:block; margin-bottom:8px; color:#333;">Últimos 3 dígitos del número</label>
      <input type="text" id="editReceivePhone" value="456" maxlength="3" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
    </div>
    <div style="margin:15px 0;">
      <label style="display:block; margin-bottom:8px; color:#333;">Código de seguridad</label>
      <div style="display:flex; gap:10px;">
        <input type="text" id="editRcvCode1" value="3" maxlength="1" style="width:50px; text-align:center; font-size:1.2em; font-weight:bold;">
        <input type="text" id="editRcvCode2" value="7" maxlength="1" style="width:50px; text-align:center; font-size:1.2em; font-weight:bold;">
        <input type="text" id="editRcvCode3" value="1" maxlength="1" style="width:50px; text-align:center; font-size:1.2em; font-weight:bold;">
      </div>
    </div>
    <div style="margin:15px 0;">
      <label style="display:block; margin-bottom:8px; color:#333;">Número de operación</label>
      <input type="text" id="editReceiveOp" value="87654321" style="width:100%; padding:12px; border-radius:8px; border:1px solid #e0e0e0; font-size:1em;">
    </div>
    <button class="big-button" onclick="saveReceiveData()">Guardar Cambios</button>
    <button class="big-button secondary" style="margin-top:10px;" onclick="goBack()">← Volver</button>
  </div>

  <!-- SCRIPT: Funcionalidad "Te yapearon" -->
  <script>
    let receiveData = JSON.parse(localStorage.getItem('yape_receive_data')) || {
      name: 'Luis Gómez',
      amount: '100.00',
      phone: '456',
      code: ['3','7','1'],
      operation: '87654321',
      date: '23 ago. 2025',
      time: '09:15 a.m.'
    };

    function loadReceiveData() {
      document.getElementById('receiveAmount').textContent = receiveData.amount;
      document.getElementById('receiveName').textContent = receiveData.name;
      document.getElementById('receivePhone').textContent = `*** *** ${receiveData.phone}`;
      document.getElementById('rcvCode1').textContent = receiveData.code[0];
      document.getElementById('rcvCode2').textContent = receiveData.code[1];
      document.getElementById('rcvCode3').textContent = receiveData.code[2];
      document.getElementById('receiveOp').textContent = receiveData.operation;
      document.getElementById('receiveDate').textContent = receiveData.date;
      document.getElementById('receiveTime').textContent = receiveData.time;

      if (document.getElementById('editReceiveName')) {
        document.getElementById('editReceiveName').value = receiveData.name;
        document.getElementById('editReceiveAmount').value = receiveData.amount;
        document.getElementById('editReceivePhone').value = receiveData.phone;
        document.getElementById('editRcvCode1').value = receiveData.code[0];
        document.getElementById('editRcvCode2').value = receiveData.code[1];
        document.getElementById('editRcvCode3').value = receiveData.code[2];
        document.getElementById('editReceiveOp').value = receiveData.operation;
      }
    }

    function saveReceiveData() {
      const name = document.getElementById('editReceiveName').value.trim();
      const amount = document.getElementById('editReceiveAmount').value;
      const phone = document.getElementById('editReceivePhone').value.trim();
      const code1 = document.getElementById('editRcvCode1').value.trim();
      const code2 = document.getElementById('editRcvCode2').value.trim();
      const code3 = document.getElementById('editRcvCode3').value.trim();
      const operation = document.getElementById('editReceiveOp').value.trim();

      if (!name || !amount || !phone || !code1 || !code2 || !code3 || !operation) {
        alert("Completa todos los campos");
        return;
      }

      receiveData = { name, amount, phone, code: [code1, code2, code3], operation };
      localStorage.setItem('yape_receive_data', JSON.stringify(receiveData));
      loadReceiveData();
      alert('✅ Recibo "Te yapearon" actualizado');
      goBack();
    }

    function showReceive() {
      loadReceiveData();
      showScreen('receiveContainer');
      showSparkles();
    }

    window.addEventListener('load', () => {
      setTimeout(loadReceiveData, 500);
    });
  </script>
</body>
</html>
