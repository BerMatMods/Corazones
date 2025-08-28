
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>⚡ Calculadora Neon - BerMatMods ⚡</title>
  <style>
    body {
      background: #0a0a0a;
      font-family: 'Poppins', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      color: #fff;
      flex-direction: column;
      overflow: hidden;
    }h1 {
  font-size: 2rem;
  color: #0ff;
  text-shadow: 0 0 10px #0ff, 0 0 20px #0ff;
  margin-bottom: 20px;
  animation: glow 2s infinite alternate;
}

@keyframes glow {
  from { text-shadow: 0 0 5px #0ff, 0 0 15px #0ff; }
  to { text-shadow: 0 0 20px #f0f, 0 0 30px #f0f; }
}

.calculadora {
  background: rgba(20,20,20,0.95);
  padding: 20px;
  border-radius: 20px;
  box-shadow: 0 0 20px #0ff, 0 0 40px #f0f;
  display: grid;
  grid-template-columns: repeat(4, 80px);
  grid-gap: 15px;
  justify-content: center;
}

input[type="text"] {
  grid-column: span 4;
  height: 60px;
  font-size: 1.5rem;
  text-align: right;
  padding: 10px;
  border: none;
  border-radius: 10px;
  background: #111;
  color: #0ff;
  box-shadow: inset 0 0 10px #0ff;
  outline: none;
}

button {
  height: 60px;
  font-size: 1.2rem;
  border: none;
  border-radius: 10px;
  background: #111;
  color: #fff;
  box-shadow: 0 0 10px #0ff, inset 0 0 5px #0ff;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  box-shadow: 0 0 20px #f0f, 0 0 30px #0ff;
  transform: scale(1.1);
}

.btn-igual {
  grid-row: span 2;
  background:#0ff;
  color:#111;
  font-weight:bold;
  box-shadow: 0 0 20px #0ff, inset 0 0 5px #111;
}

.btn-igual:hover {
  box-shadow: 0 0 30px #f0f, 0 0 40px #0ff;
}

footer {
  margin-top: 25px;
  font-size: 0.9rem;
  color: #0ff;
  text-align: center;
  text-shadow: 0 0 10px #0ff;
  animation: neon 3s infinite alternate;
}

@keyframes neon {
  from { color: #0ff; text-shadow: 0 0 10px #0ff; }
  to { color: #f0f; text-shadow: 0 0 20px #f0f; }
}

  </style>
</head>
<body>
  <h1>⚡ Calculadora Neon - BerMatMods ⚡</h1>  <div class="calculadora">
    <input type="text" id="pantalla" disabled>
    <button onclick="borrar()">C</button>
    <button onclick="insertar('/')">÷</button>
    <button onclick="insertar('*')">×</button>
    <button onclick="retroceder()">⌫</button><button onclick="insertar('7')">7</button>
<button onclick="insertar('8')">8</button>
<button onclick="insertar('9')">9</button>
<button onclick="insertar('-')">−</button>

<button onclick="insertar('4')">4</button>
<button onclick="insertar('5')">5</button>
<button onclick="insertar('6')">6</button>
<button onclick="insertar('+')">+</button>

<button onclick="insertar('1')">1</button>
<button onclick="insertar('2')">2</button>
<button onclick="insertar('3')">3</button>
<button class="btn-igual" onclick="calcular()">=</button>

<button onclick="insertar('0')" style="grid-column: span 2;">0</button>
<button onclick="insertar('.')">.</button>

  </div>  <footer>
    <p>👨‍💻 Creado por <strong>Anth'Zz Berrocal - BerMatMods</strong></p>
    <p>🚀 Proyecto para GitHub Pages | Andahuaylas - Perú</p>
  </footer>  <script>
    const pantalla = document.getElementById("pantalla");

    function insertar(num) {
      if (pantalla.value === "Error") pantalla.value = "";
      pantalla.value += num;
    }

    function borrar() {
      pantalla.value = "";
    }

    function retroceder() {
      if (pantalla.value === "Error") pantalla.value = "";
      else pantalla.value = pantalla.value.slice(0, -1);
    }

    function calcular() {
      try {
        if (pantalla.value.trim() === "") return;
        pantalla.value = eval(pantalla.value);
      } catch {
        pantalla.value = "Error";
      }
    }

    document.addEventListener("keydown", (e) => {
      const teclasValidas = "0123456789+-*/.";
      if (teclasValidas.includes(e.key)) {
        insertar(e.key);
      } else if (e.key === "Enter") {
        calcular();
      } else if (e.key === "Backspace") {
        retroceder();
      } else if (e.key === "Escape") {
        borrar();
      }
    });
  </script></body>
</html>
