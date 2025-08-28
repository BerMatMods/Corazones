
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Rompecabezas del Amor 💖</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #ffafbd, #ffc3a0);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      color: #fff;
      text-align: center;
    }

    .container {
      background: rgba(255, 255, 255, 0.2);
      padding: 30px;
      border-radius: 20px;
      backdrop-filter: blur(10px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      max-width: 500px;
      width: 90%;
    }

    .title {
      font-size: 2rem;
      margin-bottom: 10px;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
      animation: fadeIn 1s ease;
    }

    .subtitle {
      font-size: 1.1rem;
      margin-bottom: 20px;
      opacity: 0.9;
      animation: slideUp 1.2s ease;
    }

    .puzzle-container {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 2px;
      margin: 20px auto;
      width: 306px;
      height: 306px;
      background: #fff;
      border: 4px solid #fff;
      border-radius: 12px;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
      overflow: hidden;
    }

    .piece {
      width: 100px;
      height: 100px;
      background-image: url('https://i.postimg.cc/KvZxhqQM/1742316301125-2.jpg');
      background-size: 300px 300px;
      border: 1px solid #ddd;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.3s ease;
      border-radius: 6px;
      user-select: none;
    }

    .piece:hover {
      transform: scale(1.05);
      z-index: 10;
      box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    }

    .btn {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1rem;
      background: #ff6b9d;
      color: white;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    .btn:hover {
      background: #e55a8a;
      transform: translateY(-2px);
    }

    .message {
      margin-top: 15px;
      font-size: 1.3rem;
      font-weight: bold;
      color: #fff;
      text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
      min-height: 30px;
      line-height: 1.4;
    }

    .hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: -1;
    }

    .heart {
      position: absolute;
      font-size: 1.5rem;
      animation: float 6s infinite ease-in-out;
      opacity: 0.7;
    }

    @keyframes float {
      0% {
        transform: translateY(0) rotate(0deg);
        opacity: 0;
      }
      50% {
        opacity: 0.8;
      }
      100% {
        transform: translateY(-100vh) rotate(360deg);
        opacity: 0;
      }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes slideUp {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .victory-message {
      animation: pulse 0.7s ease infinite alternate;
    }

    @keyframes pulse {
      from { transform: scale(1); }
      to { transform: scale(1.08); }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1 class="title">Arma nuestro recuerdo juntos 💕</h1>
    <p class="subtitle">Haz clic en una pieza al lado del espacio vacío para moverla.</p>

    <div class="puzzle-container" id="puzzle"></div>

    <button id="shuffleBtn" class="btn">Mezclar de nuevo</button>
    <div id="message" class="message"></div>
  </div>

  <div class="hearts">
    <span class="heart">❤️</span>
    <span class="heart">💖</span>
    <span class="heart">💕</span>
    <span class="heart">💘</span>
    <span class="heart">💓</span>
  </div>

  <script>
    document.addEventListener("DOMContentLoaded", () => {
      const puzzleContainer = document.getElementById("puzzle");
      const shuffleBtn = document.getElementById("shuffleBtn");
      const message = document.getElementById("message");

      const rows = 3;
      const cols = 3;
      const totalPieces = rows * cols;
      let pieces = [];
      let emptyIndex = totalPieces - 1;

      function getBackgroundPosition(row, col) {
        return `-${col * 100}px -${row * 100}px`;
      }

      function createPieces() {
        puzzleContainer.innerHTML = "";
        pieces = [];

        for (let row = 0; row < rows; row++) {
          for (let col = 0; col < cols; col++) {
            const pieceIndex = row * cols + col;
            const piece = document.createElement("div");
            piece.classList.add("piece");

            if (pieceIndex !== emptyIndex) {
              piece.style.backgroundPosition = getBackgroundPosition(row, col);
              piece.dataset.index = pieceIndex;
            } else {
              piece.style.backgroundColor = "#f0f0f0";
              piece.style.border = "1px dashed #ccc";
            }

            piece.dataset.row = row;
            piece.dataset.col = col;

            piece.addEventListener("click", () => {
              if (isAdjacentToEmpty(pieceIndex)) {
                swapPieces(pieceIndex, emptyIndex);
              }
            });

            puzzleContainer.appendChild(piece);
            pieces.push(piece);
          }
        }
      }

      function isAdjacentToEmpty(index) {
        const idx = parseInt(index);
        const row = Math.floor(idx / cols);
        const col = idx % cols;
        const emptyRow = Math.floor(emptyIndex / cols);
        const emptyCol = emptyIndex % cols;

        return (
          (Math.abs(row - emptyRow) === 1 && col === emptyCol) ||
          (Math.abs(col - emptyCol) === 1 && row === emptyRow)
        );
      }

      function swapPieces(index1, index2) {
        const tempBg = pieces[index1].style.backgroundPosition;
        const tempDataset = pieces[index1].dataset.index;

        pieces[index1].style.backgroundPosition = pieces[index2].style.backgroundPosition;
        pieces[index2].style.backgroundPosition = tempBg;

        pieces[index1].dataset.index = pieces[index2].dataset.index;
        pieces[index2].dataset.index = tempDataset;

        emptyIndex = index2;

        checkWin();
      }

      function checkWin() {
        let correct = 0;
        for (let i = 0; i < totalPieces - 1; i++) {
          if (pieces[i].dataset.index == i) correct++;
        }

        if (correct === totalPieces - 1) {
          message.innerHTML = "¡LO LOGRASTE MI AMOOOOOOR!<br>TE AMO MUCHÍSIMO 💖";
          message.classList.add("victory-message");
          confetti();
        } else {
          message.textContent = "";
          message.classList.remove("victory-message");
        }
      }

      function shufflePieces() {
        for (let i = 0; i < 300; i++) {
          const neighbors = [];
          const row = Math.floor(emptyIndex / cols);
          const col = emptyIndex % cols;

          if (row > 0) neighbors.push(emptyIndex - cols);
          if (row < rows - 1) neighbors.push(emptyIndex + cols);
          if (col > 0) neighbors.push(emptyIndex - 1);
          if (col < cols - 1) neighbors.push(emptyIndex + 1);

          const randomNeighbor = neighbors[Math.floor(Math.random() * neighbors.length)];
          swapPieces(randomNeighbor, emptyIndex);
        }
        message.textContent = "";
      }

      function confetti() {
        for (let i = 0; i < 60; i++) {
          const heart = document.createElement("div");
          heart.textContent = ["💖", "💕", "💓", "💘", "💗", "💞"][Math.floor(Math.random() * 6)];
          heart.style.position = "fixed";
          heart.style.fontSize = Math.random() * 25 + 15 + "px";
          heart.style.left = Math.random() * 100 + "vw";
          heart.style.top = "0";
          heart.style.color = "#ff69b4";
          heart.style.pointerEvents = "none";
          heart.style.zIndex = "1000";
          heart.style.userSelect = "none";
          heart.style.opacity = Math.random();
          heart.style.transform = `rotate(${Math.random() * 360}deg)`;

          document.body.appendChild(heart);

          const animation = heart.animate(
            [
              { transform: `translateY(0) rotate(0deg)`, opacity: 1 },
              { transform: `translateY(${window.innerHeight}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
            ],
            {
              duration: Math.random() * 3000 + 2500,
              easing: "cubic-bezier(0.2, 0.8, 0.8, 0.2)"
            }
          );

          animation.onfinish = () => heart.remove();
        }
      }

      shuffleBtn.addEventListener("click", () => {
        shufflePieces();
        message.textContent = "";
        message.classList.remove("victory-message");
      });

      // Iniciar
      createPieces();
      shufflePieces();
    });
  </script>
</body>
</html>
