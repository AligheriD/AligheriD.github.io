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
            color: #f0f0f0;
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

        /* --- ESTILOS PARA EL MODAL --- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease-in-out;
        }

        .modal-overlay.show {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-content {
            background: white;
            padding: 40px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transform: scale(0.8);
            transition: transform 0.4s ease-in-out;
            max-width: 500px;
            color: #333;
        }
        
        .modal-overlay.show .modal-content {
            transform: scale(1);
        }

        .modal-content h2 {
            color: #4CAF50;
            font-size: 2em;
            margin-top: 0;
        }

        .modal-content p {
            font-size: 1.2em;
            line-height: 1.6;
        }

        .modal-content img {
            max-width: 100px; /* Tamaño del perrito */
            height: auto;
            margin-top: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        /* --- FIN DE ESTILOS PARA EL MODAL --- */
        
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

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-30px) rotate(8deg); }
            100% { transform: translateY(0) rotate(0deg); }
        }
    </style>
</head>
<body>
    <div class="butterfly butterfly-1">🦋</div>
    <div class="butterfly butterfly-2">🦋</div>
    
    <h1>¿A Dónde Vamos Hoy?</h1>
    <p class="instructions">¡Haga clic, señorita Mairyn, en la tarjeta restante!</p>

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

    <div id="finalModal" class="modal-overlay">
        <div class="modal-content">
            <h2>¡Felicidades! 🥳</h2>
            <p>Has completado todas las aventuras disponibles hasta ahora.</p>
            <p><strong>Estamos construyendo nuevas sorpresas para ti. ¡Mantente al tanto!</strong></p>
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWH_7B0xO5ZgdvJSlsSN0-va01kYZglZYZ1w&s" alt="Perrito tierno">
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const selectableCards = document.querySelectorAll('.scratch-card:not(.disabled)');
            const allCards = document.querySelectorAll('.scratch-card');
            const winnerMsg = document.getElementById('winnerMsg');
            const finalModal = document.getElementById('finalModal');
            let completedCards = 0;

            function showFinalPopup() {
                // Asegurarse de que todas las tarjetas se vean completadas
                allCards.forEach(c => {
                    if (!c.classList.contains('disabled')) {
                        c.classList.add('disabled');
                    }
                    if (!c.querySelector('.check-icon')) {
                         const checkIcon = document.createElement('i');
                         checkIcon.className = 'fas fa-check-circle check-icon';
                         c.appendChild(checkIcon);
                    }
                });
                winnerMsg.classList.remove('show'); // Ocultar mensaje intermedio
                finalModal.classList.add('show'); // Mostrar el modal
            }
            
            // Revisar localStorage al cargar la página
            if (localStorage.getItem('allAdventuresCompleted') === 'true') {
                showFinalPopup();
            }

            selectableCards.forEach(card => {
                card.addEventListener('click', () => {
                    if (card.classList.contains('revealed')) return;

                    card.classList.add('revealed');
                    
                    const optionChosen = card.querySelector('.option-text').textContent;
                    winnerMsg.textContent = `¡Excelente elección! Hoy iremos a: ${optionChosen}`;
                    winnerMsg.classList.add('show');
                    
                    card.classList.add('disabled');
                    card.style.pointerEvents = 'none';
                    const checkIcon = document.createElement('i');
                    checkIcon.className = 'fas fa-check-circle check-icon';
                    card.appendChild(checkIcon);
                    
                    completedCards++;

                    // Si ya se completaron todas las tarjetas seleccionables
                    if (completedCards === selectableCards.length) {
                         setTimeout(() => {
                            localStorage.setItem('allAdventuresCompleted', 'true');
                            showFinalPopup();
                        }, 4000); // <-- TIEMPO CAMBIADO AQUÍ a 4 segundos
                    }
                });
            });
        });
    </script>
</body>
</html>
