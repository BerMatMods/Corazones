<!--
Yape Fake v2.5 - Mejorado (Pantalla login, efectos serpentinas, recibo personalizable, botones estilo yape, etc)
Desarrollado por AnthZz Berrocal _BerMat_Mods
-->
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Yape Fake v2.5</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
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
    /* ... [TUS ESTILOS ORIGINALES AQUÍ, NO SE MODIFICAN] ... */

    /* LOGIN SCREEN */
    #loginScreen {
      background:var(--yape-purple); min-height:100vh; display:flex;align-items:center;justify-content:center;flex-direction:column;
      z-index: 9999; position:fixed; top:0; left:0; width:100vw; height:100vh;
    }
    #loginScreen img { width:90px; margin-bottom:18px;}
    #loginScreen h2 {color:white; margin-bottom:12px;}
    #loginScreen input { padding:14px;width:220px;border-radius:8px;border:none;font-size:1.1em;text-align:center; }
    #loginScreen .big-button { margin-top:18px; width:220px;}
    #loginScreen #loginError { color:#ff5252; margin-top:8px; font-weight:600; display:none; }
    /* BOTONES QR/YAPEAR ESTILO YAPE */
    .big-button {
      flex: 1;
      background: var(--yape-green);
      color: white;
      border: none;
      padding: 18px 0;
      border-radius: 25px;
      font-size: 1.2em;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 6px;
      box-shadow: 0 8px 24px rgba(0,200,83,0.20);
    }
    .big-button.yapear { background: var(--yape-green); }
    .big-button.qr { background: var(--yape-green); }
    .big-button:hover { transform: translateY(-2px); box-shadow: 0 12px 30px rgba(0,200,83,0.3);}
    .big-button span { font-size: 0.9em; margin-top: 4px; }
    /* SERPENTINAS/ANIMACIÓN */
    .sparkles { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1001; display: none; }
    .serpentina {
      position: absolute;
      width: 8px;
      height: 44px;
      border-radius: 12px;
      background: linear-gradient(90deg,#00d664,#fff200,#ff2e72,#7b1fa2);
      animation: serpentinas 2.5s cubic-bezier(.31,.79,.72,.98) forwards;
      opacity: 0.9;
    }
    @keyframes serpentinas {
      0% { transform:rotate(0) scaleY(0.5) translateY(-30px); opacity:1;}
      80% { transform:rotate(360deg) scaleY(1.2) translateY(80vh); opacity:0.8;}
      100% { opacity:0; }
    }
    /* RECIBO: PERSONALIZABLE */
    #confirmType { margin:12px 0; width:100%; padding:8px; border-radius:8px; border:1px solid var(--border); font-size:1em;}
    /* ... [TUS ESTILOS ORIGINALES SIGUEN AQUÍ] ... */
  </style>
</head>
<body>
  <div class="container">
    <!-- LOGIN SCREEN -->
    <div id="loginScreen" class="screen active">
      <img src="https://seeklogo.com/images/Y/yape-logo-6A0A8BFD2B-seeklogo.com.png" alt="Yape">
      <h2>Bienvenido a Yape Fake</h2>
      <input type="password" id="loginCode" maxlength="6" placeholder="Clave de acceso">
      <button class="big-button yapear" onclick="checkLogin()">Ingresar</button>
      <div id="loginError">Clave incorrecta, consulta con el creador</div>
    </div>
    <!-- ... [TU CÓDIGO ORIGINAL SIGUE AQUÍ: MENÚ, HEADER, HOME, SERVICIOS, ETC] ... -->
    <!-- Botones QR/Yapear estilo Yape -->
    <div class="buttons-row">
      <button class="big-button qr" onclick="startScan()">
        <i class="fas fa-qrcode"></i>
        <span>ESCANEAR QR</span>
      </button>
      <button class="big-button yapear" onclick="showSendScreen()">
        <i class="fas fa-paper-plane"></i>
        <span>YAPEAR</span>
      </button>
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
      <div class="send-title">Tipo de recibo</div>
      <select id="confirmType" onchange="changeConfirmType()">
        <option value="¡Yapeaste!">¡Yapeaste!</option>
        <option value="¡Te yapearon!">¡Te yapearon!</option>
      </select>
      <div class="send-buttons">
        <button class="send-btn cancel" onclick="goBack()">Cancelar</button>
        <button class="send-btn send" onclick="confirmSend()">Yapear</button>
      </div>
    </div>
    <!-- Recibo -->
    <div id="confirmContainer" class="screen confirm-container">
      <div class="global-close" onclick="goBack()"><i class="fas fa-times"></i></div>
      <div class="confirm-screen">
        <button class="share-inside" onclick="alert('Compartir recibo')">
          <i class="fas fa-share-alt"></i>
        </button>
        <div class="confirm-title" id="confirmTitle">¡Yapeaste!</div>
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
      <!-- ... resto igual ... -->
    </div>
    <div class="sparkles" id="sparkles"></div>
    <div class="footer"><strong>by AnthZz Berrocal _BerMat_Mods</strong></div>
  </div>
  <script>
    /* === CÓDIGO ORIGINAL Y MEJORAS === */
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
    let movements = JSON.parse(localStorage.getItem('yape_movements')) || [];
    // LOGIN
    function checkLogin() {
      const code = document.getElementById('loginCode').value;
      if (code === "020807") {
        document.getElementById('loginScreen').style.display = 'none';
        showScreen('home');
      } else {
        document.getElementById('loginError').style.display = 'block';
      }
    }
    // ... [TUS FUNCIONES ORIGINALES AQUÍ] ...
    function toggleMenu() { const sidebar = document.getElementById('menuSidebar'); const overlay = document.getElementById('menuOverlay'); sidebar.classList.toggle('active'); overlay.style.display = sidebar.classList.contains('active') ? 'block' : 'none'; }
    function toggleBalance() { const elem = document.getElementById('balanceAmount'); if (balanceVisible) { elem.textContent = `S/ ${balance.toFixed(2)}`; document.querySelector('.balance-toggle span:nth-child(1)').textContent = 'Ocultar saldo'; balanceVisible = false; } else { elem.textContent = '●●●●●●'; document.querySelector('.balance-toggle span:nth-child(1)').textContent = 'Mostrar saldo'; balanceVisible = true; } }
    function startScan() {
      showSerpentinas();
      setTimeout(() => {
        const amount = (Math.random() * 60 + 10).toFixed(2);
        alert(`✅ Pago realizado\nMonto: S/ ${amount}`);
        balance -= parseFloat(amount);
        document.getElementById('balanceAmount').textContent = `S/ ${balance.toFixed(2)}`;
        document.getElementById('menuBalance').textContent = balance.toFixed(2);
        addMovement('Pago realizado', '*** *** 777', amount);
      }, 2000);
    }
    function showSendScreen() {
      document.getElementById('sendPhone').value = '';
      document.getElementById('sendName').value = userProfile.name;
      document.getElementById('amountInput').value = '';
      document.getElementById('sendAmount').textContent = '0.00';
      document.getElementById('confirmType').value = '¡Yapeaste!';
      showScreen('sendScreen');
    }
    function updateAmount(value) { document.getElementById('sendAmount').textContent = value || '0.00'; }
    function changeConfirmType() { document.getElementById('confirmTitle').textContent = document.getElementById('confirmType').value; }
    function confirmSend() {
      const phone = document.getElementById('sendPhone').value;
      const name = document.getElementById('sendName').value;
      const amount = document.getElementById('sendAmount').textContent;
      const type = document.getElementById('confirmType').value;
      if (!phone || phone.length < 9) { alert("Número inválido"); return; }
      if (!amount || amount === '0.00') { alert("Ingresa un monto válido"); return; }
      showConfirm(phone, name, amount, type);
    }
    function showConfirm(phone, name, amount, type) {
      showScreen('confirmContainer');
      document.getElementById('confirmAmount').textContent = amount;
      document.getElementById('confirmName').textContent = name;
      document.getElementById('confirmTitle').textContent = type;
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
      showSerpentinas();
      addMovement(name, phone, amount);
    }
    function addMovement(name, phone, amount) {
      const now = new Date();
      const date = now.toLocaleDateString('es-PE', { day: '2-digit', month: 'short', year: 'numeric' }).replace('.', '');
      const time = now.toLocaleTimeString('es-PE', { hour: '2-digit', minute: '2-digit', hour12: true });
      const operation = Math.floor(Math.random() * 90000000 + 10000000);
      const movement = { name: name, phone: `*** *** ${phone.slice(-3)}`, amount: amount, date: `${date} ${time}`, operation: operation };
      movements.unshift(movement);
      localStorage.setItem('yape_movements', JSON.stringify(movements));
      renderMovements();
    }
    function renderMovements() {
      const container = document.getElementById('movementsList');
      container.innerHTML = '';
      if (movements.length === 0) { container.innerHTML = '<div style="text-align:center; color:#888; padding:20px;">No tienes movimientos aún</div>'; return; }
      movements.forEach(mov => {
        const item = document.createElement('div');
        item.className = 'movement-item';
        item.innerHTML = `<div class="movement-icon"><i class="fas fa-paper-plane"></i></div>
          <div class="movement-info"><div class="movement-name">${mov.name}</div><div class="movement-date">${mov.date}</div></div>
          <div class="movement-amount">S/ ${mov.amount}</div>`;
        container.appendChild(item);
      });
    }
    function goBack() { showScreen('home'); }
    function showScreen(id) {
      document.querySelectorAll('.screen').forEach(s => s.style.display = 'none');
      document.getElementById(id).style.display = 'block';
      if (id === 'movementsList') { renderMovements(); }
    }
    // Animación serpentinas tipo Yape
    function showSerpentinas() {
      const container = document.getElementById('sparkles');
      container.style.display = 'block';
      for (let i = 0; i < 26; i++) {
        setTimeout(() => {
          const serp = document.createElement('div');
          serp.classList.add('serpentina');
          serp.style.left = Math.random()*100 + 'vw';
          // Colores aleatorios tipo Yape
          serp.style.background = `linear-gradient(90deg,${randomColor()},${randomColor()},${randomColor()})`;
          container.appendChild(serp);
          setTimeout(() => serp.remove(), 3000);
        }, i*60);
      }
      setTimeout(() => container.style.display='none',3000);
    }
    function randomColor() {
      const c = ['#00d664','#fff200','#ff2e72','#7b1fa2','#29b6f6','#fae100'];
      return c[Math.floor(Math.random()*c.length)];
    }
    window.addEventListener('load', () => {
      showScreen('loginScreen');
      renderMovements();
    });
    /* ... [TUS FUNCIONES ORIGINALES SIGUEN ...] ... */
  </script>
</body>
</html>
