<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿A Dónde Vamos Hoy?</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            text-align: center;
            background: #f0f0f0;
            background-image: url('https://static.videezy.com/system/resources/thumbnails/000/039/986/original/17_024_03.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            position: relative;
        }

        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: -1;
        }

        h1 {
            color: #fff;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
        }

        .instructions {
            color: #fff;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
        }

        .game-container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
            max-width: 900px;
        }

        .scratch-card {
            width: 250px;
            height: 150px;
            background-color: #ccc;
            border: 5px solid #a0a0a0;
            border-radius: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.2em;
            font-weight: bold;
            color: #555;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            transition: transform 0.2s ease-in-out;
        }

        .scratch-card:hover:not(.disabled) {
            transform: translateY(-5px);
        }

        .scratch-card.disabled {
            cursor: not-allowed;
            opacity: 0.6;
            background-color: #e0e0e0;
        }

        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #4CAF50;
            background-image: linear-gradient(45deg, #4CAF50 25%, #8BC34A 25%, #8BC34A 50%, #4CAF50 50%, #4CAF50 75%, #8BC34A 75%, #8BC34A);
            background-size: 20px 20px;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 1.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            transition: opacity 0.5s ease-in-out;
        }

        .scratch-card.revealed .overlay {
            opacity: 0;
            pointer-events: none;
        }

        .option-text {
            color: #333;
            font-size: 1.5em;
            padding: 10px;
            text-align: center;
        }

        .winner-message {
            margin-top: 30px;
            font-size: 2em;
            color: #4CAF50; /* Cambiado a un color más festivo */
            font-weight: bold;
            opacity: 0;
            transition: opacity 1s ease-in-out;
            text-shadow: 1px 1px 2px #000;
        }

        .winner-message.show {
            opacity: 1;
        }

        .check-icon {
            color: #4CAF50;
            font-size: 3em;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
        }

        /* Efectos de decoración */
        .butterfly {
            position: absolute;
            font-size: 3em;
            color: #fff;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
            animation: float 20s infinite linear;
            pointer-events: none;
            opacity: 0.8;
            z-index: 1;
        }
        .butterfly-1 { top: 5%; left: 5%; animation-duration: 22s; }
        .butterfly-2 { top: 5%; right: 5%; animation-duration: 25s; }
        .butterfly-3 { bottom: 5%; left: 5%; animation-duration: 18s; transform: scale(0.8); }
        .butterfly-4 { bottom: 5%; right: 5%; animation-duration: 23s; transform: scale(0.9); }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 0.8; }
            50% { transform: translateY(-30px) rotate(8deg); opacity: 1; }
            100% { transform: translateY(0) rotate(0deg); opacity: 0.8; }
        }
        
        @media (max-width: 600px) {
            h1 {
                font-size: 1.8em;
            }
            .scratch-card {
                width: 200px;
                height: 120px;
            }
            .option-text {
                font-size: 1.2em;
            }
            .overlay {
                font-size: 1.2em;
            }
            .winner-message {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="butterfly butterfly-1">🦋</div>
    <div class="butterfly butterfly-2">🦋</div>
    <div class="butterfly butterfly-3">🦋</div>
    <div class="butterfly butterfly-4">🦋</div>
    
    <h1>¿A Dónde Vamos Hoy?</h1>
    <p class="instructions">¡Haga clic, señorita Mairyn, en la tarjeta restante para descubrir nuestra aventura de hoy!</p>

    <div class="game-container">
        <div class="scratch-card disabled" id="card1">
            <div class="option-text"> Sodas y juegos de mesa 🧿 </div>
            <i class="fas fa-check-circle check-icon"></i>
        </div>

        <div class="scratch-card" id="card2">
            <div class="overlay">RASPA AQUÍ</div>
            <div class="option-text"> Cafeteria con muchos libros 📖 </div>
        </div>
        
        <div class="scratch-card disabled" id="card3">
            <div class="option-text"> Senderismo por calvario de metepec 🗺️</div>
            <i class="fas fa-check-circle check-icon"></i>
        </div>
    </div>

    <p class="winner-message" id="winnerMsg"></p>

    <script>
        const cards = document.querySelectorAll('.scratch-card:not(.disabled)');
        const winnerMsg = document.getElementById('winnerMsg');
        let completedCards = 0;

        cards.forEach(card => {
            card.addEventListener('click', () => {
                // Si la tarjeta ya fue revelada, no hagas nada
                if (card.classList.contains('revealed')) {
                    return;
                }

                // Revelar la tarjeta
                card.classList.add('revealed');
                
                const optionChosen = card.querySelector('.option-text').textContent;
                
                // Mostrar mensaje de la opción elegida
                winnerMsg.textContent = `¡Excelente elección! Hoy iremos a: ${optionChosen}`;
                winnerMsg.classList.add('show');
                
                // Deshabilitar la tarjeta y agregar la palomita
                card.classList.add('disabled');
                card.style.pointerEvents = 'none';
                const checkIcon = document.createElement('i');
                checkIcon.className = 'fas fa-check-circle check-icon';
                card.appendChild(checkIcon);
                
                completedCards++;

                // Verificar si ya se completaron todas las tarjetas
                if (completedCards === cards.length) {
                    setTimeout(() => {
                        // Mensaje final y más bonito :)
                        winnerMsg.textContent = "¡Felicidades por completar todas las aventuras! 🥳 Estamos preparando nuevas sorpresas para ti. ¡Mantente al tanto!";
                    }, 2500); // Muestra el mensaje final después de 2.5 segundos
                }
            });
        });
        
        // Mensaje para las tarjetas ya deshabilitadas
        document.querySelectorAll('.scratch-card.disabled').forEach(disabledCard => {
            disabledCard.addEventListener('click', () => {
                alert('¡Ups! Ya hemos ido a esta aventura. Por favor, elige otra tarjeta.');
            });
        });

    </script>
</body>
</html>
