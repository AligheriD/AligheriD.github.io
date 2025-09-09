










<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿A Dónde Vamos Hoy? </title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            text-align: center;
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2.5em;
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
            background-color: #ccc; /* Color base de la tarjeta */
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
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            transition: transform 0.2s ease-in-out;
        }

        .scratch-card:hover {
            transform: translateY(-5px);
        }

        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #4CAF50; /* Color "raspa y gana" verde */
            background-image: linear-gradient(45deg, #4CAF50 25%, #8BC34A 25%, #8BC34A 50%, #4CAF50 50%, #4CAF50 75%, #8BC34A 75%, #8BC34A);
            background-size: 20px 20px;
            border-radius: 10px; /* Borde interno para el overlay */
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 1.5em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            transition: opacity 0.5s ease-in-out;
        }

        .scratch-card.revealed .overlay {
            opacity: 0;
            pointer-events: none; /* Desactiva eventos de ratón en el overlay oculto */
        }

        .option-text {
            color: #333;
            font-size: 1.5em;
            padding: 10px;
            text-align: center;
        }

        .instructions {
            margin-top: 20px;
            font-size: 1.1em;
            color: #666;
        }

        .winner-message {
            margin-top: 30px;
            font-size: 2em;
            color: #d32f2f; /* Un rojo vibrante para el mensaje final */
            font-weight: bold;
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }

        .winner-message.show {
            opacity: 1;
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
    <h1>¿A Dónde Vamos Hoy? ¡Raspa una Tarjeta!</h1>
    <p class="instructions">¡Haga clic, señorita Mayrin, en una de las tarjetas para descubrir nuestra aventura de hoy!</p>

    <div class="game-container">
        <div class="scratch-card" id="card1">
            <div class="overlay">RASPA AQUÍ</div>
            <div class="option-text"> Sodas y juegos de mesa 🧿 </div>
        </div>

        <div class="scratch-card" id="card2">
            <div class="overlay">RASPA AQUÍ</div>
            <div class="option-text"> Cafeteria con muchos libros 📖 </div>
        </div>

        <div class="scratch-card" id="card3">
            <div class="overlay">RASPA AQUÍ</div>
            <div class="option-text"> Senderimo por calvario de metepec 🗺️</div>
        </div>
    </div>

    <p class="winner-message" id="winnerMsg"></p>

    <script>
        const cards = document.querySelectorAll('.scratch-card');
        const winnerMsg = document.getElementById('winnerMsg');
        let revealedCount = 0;

        cards.forEach(card => {
            card.addEventListener('click', () => {
                if (!card.classList.contains('revealed')) {
                    card.classList.add('revealed');
                    revealedCount++;
                    // Mostrar el mensaje final si ya se reveló la tarjeta ganadora o si es la última
                    if (revealedCount === 1) { // Solo si es la primera tarjeta que se raspa
                        const optionChosen = card.querySelector('.option-text').textContent;
                        winnerMsg.textContent = `¡Felicidades! Hoy iremos a: ${optionChosen}`;
                        winnerMsg.classList.add('show');
                        disableOtherCards(card.id);
                    }
                }
            });
        });

        function disableOtherCards(chosenCardId) {
            cards.forEach(card => {
                if (card.id !== chosenCardId) {
                    card.style.pointerEvents = 'none'; // Deshabilita el clic en las otras tarjetas
                    // Opcionalmente, puedes "raspar" las otras automáticamente
                    // card.classList.add('revealed');
                }
            });
        }
    </script>
</body>
</html>
