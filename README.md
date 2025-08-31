<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lluvia de Te Amo</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #111;
            touch-action: manipulation;
            font-family: 'Arial', sans-serif;
            cursor: pointer;
            height: 100vh;
            width: 100vw;
        }

        .love-word {
            position: absolute;
            color: #ff0000;
            font-size: 24px;
            user-select: none;
            pointer-events: none;
            text-shadow: 0 0 8px rgba(255, 0, 0, 0.7);
            opacity: 0.9;
            animation: fall linear infinite;
            font-weight: bold;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh);
            }
        }

        .explosion {
            position: absolute;
            font-size: 20px;
            user-select: none;
            pointer-events: none;
            animation: explode 1.8s ease-out forwards;
            opacity: 0;
            font-weight: bold;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.7);
        }

        @keyframes explode {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(var(--tx), var(--ty)) scale(0);
                opacity: 0;
            }
        }

        /* Ocultar controles de audio pero mantener funcionalidad */
        #bg-music {
            position: absolute;
            opacity: 0;
            width: 1px;
            height: 1px;
        }
    </style>
</head>
<body>
    <audio id="bg-music" loop autoplay>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3" type="audio/mpeg">
        Tu navegador no soporta el elemento de audio.
    </audio>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const body = document.body;
            const audio = document.getElementById('bg-music');
            
            // Configurar audio
            audio.volume = 0.4;
            audio.play().catch(e => console.log("La reproducción automática no está permitida"));
            
            // Colores rojos para las palabras que caen
            const redColors = [
                '#ff0000', // Rojo vivo
                '#ff6b6b', // Rojo claro
                '#ff9999', // Rojo bebé
                '#cc0000', // Rojo oscuro
                '#ff3333', // Rojo brillante
                '#ff8080', // Rosa rojizo
                '#e60000', // Rojo intenso
                '#ff4d4d'  // Rojo coral
            ];
            
            // Colores pastel para las explosiones
            const explosionColors = [
                '#FFB6C1', // LightPink
                '#FFD700', // Light yellow
                '#98FB98', // PaleGreen
                '#ADD8E6', // LightBlue
                '#E6E6FA', // Lavender
                '#FFA07A', // LightSalmon
                '#87CEFA', // LightSkyBlue
                '#FFDEAD', // NavajoWhite
                '#F0E68C', // Khaki
                '#DDA0DD'  // Plum
            ];
            
            // Crear palabras "Te Amo" que caen (más tupido)
            function createFallingWord() {
                const word = document.createElement('div');
                word.className = 'love-word';
                word.textContent = Math.random() > 0.3 ? 'Te Quiero mi chiquita' : '❤️';
                word.style.left = Math.random() * 100 + 'vw';
                word.style.animationDuration = (Math.random() * 3 + 2) + 's'; // Más rápido
                word.style.color = redColors[Math.floor(Math.random() * redColors.length)];
                word.style.fontSize = (Math.random() * 15 + 20) + 'px';
                word.style.opacity = Math.random() * 0.7 + 0.3;
                
                body.appendChild(word);
                
                // Eliminar la palabra cuando salga de la pantalla
                setTimeout(() => {
                    word.remove();
                }, parseFloat(word.style.animationDuration) * 1000);
            }
            
            // Crear múltiples palabras que caen (más tupido)
            for (let i = 0; i < 80; i++) {
                setTimeout(createFallingWord, Math.random() * 2000);
            }
            
            // Crear nuevas palabras continuamente (más frecuente)
            setInterval(createFallingWord, 200);
            
            // Crear explosión al hacer clic/tocar
            body.addEventListener('click', createExplosion);
            body.addEventListener('touchstart', createExplosion);
            
            function createExplosion(e) {
                const x = e.clientX || (e.touches && e.touches[0].clientX);
                const y = e.clientY || (e.touches && e.touches[0].clientY);
                
                if (x === undefined || y === undefined) return;
                
                // Crear múltiples partículas para la explosión
                for (let i = 0; i < 40; i++) { // Más partículas
                    const particle = document.createElement('div');
                    particle.className = 'explosion';
                    particle.textContent = Math.random() > 0.3 ? 'Te Quiero mi chiquita' : '❤️';
                    particle.style.left = x + 'px';
                    particle.style.top = y + 'px';
                    particle.style.color = explosionColors[Math.floor(Math.random() * explosionColors.length)];
                    
                    // Direcciones aleatorias para la explosión
                    const angle = Math.random() * Math.PI * 2;
                    const distance = Math.random() * 150 + 80; // Más lejos
                    const tx = Math.cos(angle) * distance;
                    const ty = Math.sin(angle) * distance;
                    
                    particle.style.setProperty('--tx', tx + 'px');
                    particle.style.setProperty('--ty', ty + 'px');
                    particle.style.fontSize = (Math.random() * 15 + 18) + 'px';
                    particle.style.animationDuration = (Math.random() * 0.5 + 1.5) + 's'; // Más lento
                    
                    body.appendChild(particle);
                    
                    // Eliminar la partícula después de la animación
                    setTimeout(() => {
                        particle.remove();
                    }, 1800);
                }
            }
            
            // Permitir que el audio se reproduzca después de una interacción
            document.addEventListener('click', function() {
                audio.play().catch(e => console.log("Audio no pudo reproducirse"));
            }, { once: true });
        });
    </script>
</body>
</html>
