
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>Yape Replica Educativa</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:400,700&amp;display=swap">
  <style>
    body {
      font-family: 'Roboto', Arial, sans-serif;
      background: #f2f3f7;
      margin: 0;
      padding: 0;
      color: #333;
    }
    .container {
      max-width: 400px;
      background: #fff;
      margin: 32px auto;
      border-radius: 18px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.06);
      overflow: hidden;
      border: 1px solid #e6e6e6;
    }
    .header {
      background: linear-gradient(90deg,#30e57a 0%, #0ac96b 100%);
      color: #fff;
      padding: 32px 24px 20px 24px;
      text-align: left;
      position: relative;
    }
    .profile {
      display: flex;
      align-items: center;
      margin-bottom: 12px;
    }
    .avatar {
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background: #fff;
      border: 2px solid #fff;
      object-fit: cover;
      margin-right: 14px;
    }
    .profile-name {
      font-size: 1.3em;
      font-weight: 700;
      margin: 0;
      display: flex;
      align-items: center;
    }
    .edit-btn {
      background: none;
      border: none;
      color: #fff;
      font-size: 1em;
      margin-left: 8px;
      cursor: pointer;
      outline: none;
      transition: opacity .1s;
      opacity: 0.7;
    }
    .edit-btn:hover { opacity: 1; }
    .balance {
      font-size: 2em;
      font-weight: 700;
      margin: 12px 0 0 0;
      letter-spacing: 1px;
    }
    .label {
      font-size: 1em;
      opacity: 0.85;
    }
    .actions {
      display: flex;
      justify-content: space-around;
      background: #fff;
      padding: 18px 0;
      border-bottom: 1px solid #f2f3f7;
    }
    .action-btn {
      background: linear-gradient(90deg,#30e57a 0%, #15e1b7 100%);
      color: #fff;
      border: none;
      border-radius: 12px;
      font-size: 1em;
      font-weight: 700;
      padding: 13px 24px;
      cursor: pointer;
      box-shadow: 0 1px 6px rgba(44,199,120,0.10);
      transition: background .2s;
    }
    .action-btn:active {
      background: linear-gradient(90deg,#15e1b7 0%, #30e57a 100%);
    }
    .historial-title {
      font-size: 1.1em;
      font-weight: 700;
      margin: 16px 0 6px 24px;
    }
    .historial {
      padding: 0 24px 24px 24px;
      background: #fff;
    }
    .historial-list {
      list-style: none;
      margin: 0;
      padding: 0;
    }
    .historial-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 0;
      border-bottom: 1px solid #f2f3f7;
    }
    .historial-item:last-child { border-bottom: none; }
    .historial-detail {
      flex: 1;
    }
    .historial-date {
      font-size: 0.93em;
      color: #888;
    }
    .historial-amount {
      font-weight: 700;
      font-size: 1em;
      color: #0ac96b;
      min-width: 70px;
      text-align: right;
    }
    /* Modal */
    .modal-bg {
      position: fixed;
      top:0;left:0;right:0;bottom:0;
      background: rgba(0,0,0,0.24);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 100;
    }
    .modal {
      background: #fff;
      padding: 28px 18px 18px 18px;
      border-radius: 18px;
      max-width: 340px;
      box-shadow: 0 4px 16px rgba(0,0,0,0.18);
      text-align: center;
      position: relative;
    }
    .modal input[type="text"], .modal input[type="number"] {
      padding: 8px 12px;
      margin: 12px 0 20px 0;
      border-radius: 8px;
      border: 1px solid #aaa;
      width: 90%;
      font-size: 1em;
      font-family: inherit;
    }
    .modal .modal-btn {
      background: linear-gradient(90deg,#30e57a 0%, #15e1b7 100%);
      color: #fff;
      border: none;
      border-radius: 8px;
      font-size: 1em;
      font-weight: 700;
      padding: 8px 22px;
      cursor: pointer;
      margin: 0 2px;
      box-shadow: 0 1px 6px rgba(44,199,120,0.13);
    }
    .modal-close {
      position: absolute;
      top:12px;right:12px;
      background:none;
      border:none;
      font-size:1.3em;
      color:#888;
      cursor:pointer;
    }
    @media (max-width:480px) {
      .container { max-width: 98vw; }
      .header { padding: 24px 12px 12px 12px; }
      .historial { padding: 0 12px 20px 12px; }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- HEADER -->
    <div class="header">
      <div class="profile">
        <img src="https://ui-avatars.com/api/?background=0ac96b&color=fff&name=Y" alt="Avatar" class="avatar" id="avatar">
        <span class="profile-name" id="profileName">
          Usuario Yape
          <button class="edit-btn" title="Editar nombre" id="editNameBtn">&#9998;</button>
        </span>
      </div>
      <div class="label">Saldo disponible</div>
      <div class="balance" id="balance">S/ 220.00</div>
    </div>
    <!-- ACCIONES -->
    <div class="actions">
      <button class="action-btn" id="sendBtn">Enviar</button>
      <button class="action-btn" id="receiveBtn">Recibir</button>
    </div>
    <!-- HISTORIAL -->
    <div>
      <div class="historial-title">Historial</div>
      <div class="historial">
        <ul class="historial-list" id="historialList">
          <!-- Items generados por JS -->
        </ul>
      </div>
    </div>
  </div>

  <!-- MODAL EDITAR NOMBRE -->
  <div class="modal-bg" id="editModalBg">
    <div class="modal">
      <button class="modal-close" id="closeEditModal">&times;</button>
      <h3>Editar nombre</h3>
      <input type="text" id="editNameInput" maxlength="30" />
      <br>
      <button class="modal-btn" id="saveNameBtn">Guardar</button>
    </div>
  </div>

  <!-- MODAL ENVIAR DINERO -->
  <div class="modal-bg" id="sendModalBg">
    <div class="modal">
      <button class="modal-close" id="closeSendModal">&times;</button>
      <h3>Enviar dinero</h3>
      <input type="text" id="sendToInput" placeholder="Nombre destinatario" maxlength="30" />
      <input type="number" id="sendAmountInput" min="1" step="0.01" placeholder="Monto S/" />
      <br>
      <button class="modal-btn" id="confirmSendBtn">Confirmar</button>
    </div>
  </div>

  <!-- MODAL RECIBIR DINERO -->
  <div class="modal-bg" id="receiveModalBg">
    <div class="modal">
      <button class="modal-close" id="closeReceiveModal">&times;</button>
      <h3>Recibir dinero</h3>
      <input type="text" id="receiveFromInput" placeholder="Nombre remitente" maxlength="30" />
      <input type="number" id="receiveAmountInput" min="1" step="0.01" placeholder="Monto S/" />
      <br>
      <button class="modal-btn" id="confirmReceiveBtn">Confirmar</button>
    </div>
  </div>

  <script>
    // --- Datos iniciales
    let userName = localStorage.getItem('yape_user_name') || "Usuario Yape";
    let balance = parseFloat(localStorage.getItem('yape_balance')) || 220.00;
    let historial = JSON.parse(localStorage.getItem('yape_historial') || "[]");

    // --- Elementos
    const profileNameEl = document.getElementById('profileName');
    const balanceEl = document.getElementById('balance');
    const historialListEl = document.getElementById('historialList');
    const avatarEl = document.getElementById('avatar');

    // --- Renderizar nombre y balance
    function renderProfile() {
      profileNameEl.childNodes[0].nodeValue = userName;
      avatarEl.src = `https://ui-avatars.com/api/?background=0ac96b&color=fff&name=${encodeURIComponent(userName[0] || "Y")}`;
    }
    function renderBalance() {
      balanceEl.textContent = `S/ ${balance.toFixed(2)}`;
    }
    function renderHistorial() {
      historialListEl.innerHTML = "";
      if (historial.length === 0) {
        historialListEl.innerHTML = `<li style="color:#999;font-size:1em;">Sin movimientos aún</li>`;
        return;
      }
      historial.slice().reverse().forEach(item => {
        const li = document.createElement('li');
        li.className = "historial-item";
        li.innerHTML = `
          <div class="historial-detail">
            ${item.type === 'send' ? 'Enviaste a' : 'Recibiste de'}
            <b>${item.name}</b>
            <div class="historial-date">${item.date}</div>
          </div>
          <div class="historial-amount" style="color:${item.type === 'send' ? '#f44' : '#0ac96b'};">
            ${item.type === 'send' ? '-' : '+'} S/ ${item.amount.toFixed(2)}
          </div>
        `;
        historialListEl.appendChild(li);
      });
    }

    // --- Guardar datos
    function saveData() {
      localStorage.setItem('yape_user_name', userName);
      localStorage.setItem('yape_balance', balance);
      localStorage.setItem('yape_historial', JSON.stringify(historial));
    }

    // --- Modal helpers
    function openModal(id) {
      document.getElementById(id).style.display = "flex";
    }
    function closeModal(id) {
      document.getElementById(id).style.display = "none";
    }

    // --- Editar nombre
    document.getElementById('editNameBtn').onclick = () => {
      document.getElementById('editNameInput').value = userName;
      openModal('editModalBg');
      setTimeout(() => document.getElementById('editNameInput').focus(), 100);
    };
    document.getElementById('closeEditModal').onclick = () => closeModal('editModalBg');
    document.getElementById('saveNameBtn').onclick = () => {
      const newName = document.getElementById('editNameInput').value.trim();
      if (newName.length >= 2) {
        userName = newName;
        renderProfile();
        saveData();
        closeModal('editModalBg');
      }
    };

    // --- Enviar dinero
    document.getElementById('sendBtn').onclick = () => {
      document.getElementById('sendToInput').value = "";
      document.getElementById('sendAmountInput').value = "";
      openModal('sendModalBg');
      setTimeout(() => document.getElementById('sendToInput').focus(), 100);
    };
    document.getElementById('closeSendModal').onclick = () => closeModal('sendModalBg');
    document.getElementById('confirmSendBtn').onclick = () => {
      const to = document.getElementById('sendToInput').value.trim();
      const amount = parseFloat(document.getElementById('sendAmountInput').value);
      if (to.length >= 2 && amount > 0 && amount <= balance) {
        balance -= amount;
        historial.push({
          type: 'send',
          name: to,
          amount: amount,
          date: new Date().toLocaleString('es-PE', { day:'2-digit', month:'2-digit', year:'2-digit', hour:'2-digit', minute:'2-digit' }),
        });
        renderBalance();
        renderHistorial();
        saveData();
        closeModal('sendModalBg');
      } else {
        alert("Revisa los datos. El monto no puede ser mayor al saldo.");
      }
    };

    // --- Recibir dinero
    document.getElementById('receiveBtn').onclick = () => {
      document.getElementById('receiveFromInput').value = "";
      document.getElementById('receiveAmountInput').value = "";
      openModal('receiveModalBg');
      setTimeout(() => document.getElementById('receiveFromInput').focus(), 100);
    };
    document.getElementById('closeReceiveModal').onclick = () => closeModal('receiveModalBg');
    document.getElementById('confirmReceiveBtn').onclick = () => {
      const from = document.getElementById('receiveFromInput').value.trim();
      const amount = parseFloat(document.getElementById('receiveAmountInput').value);
      if (from.length >= 2 && amount > 0) {
        balance += amount;
        historial.push({
          type: 'receive',
          name: from,
          amount: amount,
          date: new Date().toLocaleString('es-PE', { day:'2-digit', month:'2-digit', year:'2-digit', hour:'2-digit', minute:'2-digit' }),
        });
        renderBalance();
        renderHistorial();
        saveData();
        closeModal('receiveModalBg');
      } else {
        alert("Revisa los datos.");
      }
    };

    // --- Inicialización
    renderProfile();
    renderBalance();
    renderHistorial();
  </script>
</body>
</html>
