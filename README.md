<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿A Dónde Vamos Hoy? ¡Raspa y Gana!</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
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
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
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
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
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

        .instructions {
            margin-top: 20px;
            font-size: 1.1em;
            color: #666;
        }

        .winner-message {
            margin-top: 30px;
            font-size: 2em;
            color: #d32f2f;
            font-weight: bold;
            opacity: 0;
            transition: opacity 1s ease-in-out;
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

        .special-event {
            margin-top: 40px;
            text-align: left;
            padding: 20px;
            max-width: 800px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            display: none;
        }
        
        .special-event.show {
            display: block;
        }

        .question-box {
            text-align: center;
            font-size: 1.4em;
            margin-bottom: 20px;
            min-height: 80px; /* Para evitar que la caja salte al cambiar de pregunta */
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 10px;
        }

        .controls {
            margin-top: 20px;
        }

        .controls button {
            background-color: #d32f2f;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        .controls button:hover {
            background-color: #b71c1c;
        }

        #timerDisplay {
            font-size: 3em;
            font-weight: bold;
            color: #d32f2f;
            margin-top: 20px;
            display: none;
        }
    </style>
</head>
<body>
    <h1>¿A Dónde Vamos Hoy? ¡Raspa una Tarjeta!</h1>
    <p class="instructions">¡Haga clic, señorita Mairyn, en una de las tarjetas para descubrir nuestra aventura de hoy!</p>

    <div class="game-container">
        <div class="scratch-card" id="card1">
            <div class="overlay">RASPA AQUÍ</div>
            <div class="option-text"> Sodas y juegos de mesa 🧿 </div>
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

    <div class="special-event" id="specialEvent">
        <div id="questionContainer">
            <h2 id="questionTitle">Desafío de las 36 Preguntas</h2>
            <div id="questionBox" class="question-box"></div>
            <div class="controls">
                <button id="nextBtn">Comenzar</button>
            </div>
        </div>
        <div id="timerDisplay"></div>
        <p id="finalMessage" style="display: none; font-size: 2.5em; font-weight: bold; color: #d32f2f; margin-top: 40px;"></p>
    </div>

    <script>
        const cards = document.querySelectorAll('.scratch-card:not(.disabled)');
        const disabledCard = document.getElementById('card3');
        const winnerMsg = document.getElementById('winnerMsg');
        const specialEvent = document.getElementById('specialEvent');
        const questionBox = document.getElementById('questionBox');
        const nextBtn = document.getElementById('nextBtn');
        const timerDisplay = document.getElementById('timerDisplay');
        const finalMessage = document.getElementById('finalMessage');

        const questions = [
            'Suponiendo que pudiera elegir a cualquier persona del mundo, ¿a quién le gustaría invitar a cenar?',
            '¿Le gustaría ser famoso? ¿En qué sentido?',
            '¿Algunas vez practica lo que va decir antes de llamar por teléfono? ¿Por qué?',
            '¿Qué constituye para usted un “día perfecto”?',
            '¿Cuándo fue la última vez que cantó a solas? ¿Con otra persona?',
            'Si pudiera vivir hasta los 90 años de edad conservando durante los últimos 60 años la mente o el cuerpo de una persona de 30 años, ¿qué preferiría?',
            '¿Tiene una corazonada secreta sobre la forma en que va a morir?',
            'Nombre tres cosas que usted y su pareja parezcan tener en común.',
            '¿De qué se siente más agradecido en la vida?',
            'Si pudiera cambiar cualquier cosa de la forma en que fue criado, ¿cuál sería?',
            'Cuéntele a su pareja la historia de su vida en cuatro minutos pero con tanto detalle como sea posible.',
            'Si pudiera despertarse mañana habiendo adquirido una cualidad o una habilidad, ¿cuál sería?',
            'Si una bola de cristal pudiera decirle la verdad sobre usted, su vida, su futuro o cualquier otra cosa, ¿qué le gustaría saber?',
            '¿Hay algo que haya soñado hacer desde hace mucho tiempo? ¿Por qué no lo ha hecho?',
            '¿Cuál es el mayor logro de su vida?',
            '¿Qué es lo que más valora en una amistad?',
            '¿Cuál es su recuerdo más preciado?',
            '¿Cuál es su recuerdo más terrible?',
            'Si supiera que dentro de un año va a morir súbitamente, ¿cambiaría en algo la forma en que vive ahora? ¿Por qué?',
            '¿Qué significa la amistad para usted?',
            '¿Qué papel desempeñan en su vida el amor y el afecto?',
            'Alternadamente, diga algo que considere una característica positiva de su pareja. Mencione un total de cinco características.',
            '¿Qué tan cercana y cálida es su familia? ¿Siente que su infancia fue más feliz que la de la mayoría?',
            '¿Cómo se siente en su relación con su madre?',
            'Cada uno haga tres declaraciones verdaderas usando “nosotros”. Por ejemplo: “Los dos estamos en esta sala sintiendo…”',
            'Complete esta frase: “Quisiera tener a alguien con quien compartir…”',
            'Si llegara a ser amigo íntimo de su pareja, diga qué sería importante que ella supiera.',
            'Dígale a su pareja qué le gusta a usted de ella; sea muy honesto esta vez y diga cosas que posiblemente no le diría a alguien que acababa de conocer.',
            'Cuéntele a su pareja un momento bochornoso de su vida.',
            '¿Cuándo fue la última vez que lloró con otra persona? ¿A solas?',
            'Dígale a su pareja algo que ya le guste a usted de ella.',
            '¿Qué es algo demasiado serio para bromear al respecto?',
            'Si fuera a morir esta noche, sin poder comunicarse con nadie, ¿qué sería lo que más lamentaría no haberle dicho a alguien? ¿Por qué no se lo ha dicho?',
            'Su casa, que contiene todo lo que usted posee en la vida, arde en un incendio. Después de salvar a sus seres queridos y sus mascotas, tiene tiempo de una carrera final para rescatar algún objeto. ¿Cuál sería y por qué?',
            '¿Qué muerte de algún familiar sería para usted la más perturbadora? ¿Por qué?',
            'Exponga un problema personal y pregúntele a su pareja cómo lo manejaría ella. Asimismo, pídale a su pareja que le diga cómo parece que usted se siente respecto del problema que eligió.'
        ];
        let currentQuestion = 0;

        cards.forEach(card => {
            card.addEventListener('click', () => {
                if (!card.classList.contains('revealed')) {
                    card.classList.add('revealed');
                    
                    const optionChosen = card.querySelector('.option-text').textContent;
                    winnerMsg.textContent = `¡Felicidades! Hoy iremos a: ${optionChosen}`;
                    winnerMsg.classList.add('show');
                    
                    cards.forEach(otherCard => {
                        if (otherCard.id !== card.id) {
                            otherCard.style.display = 'none';
                        }
                    });

                    card.style.pointerEvents = 'none';
                    
                    setTimeout(() => {
                        specialEvent.classList.add('show');
                        questionBox.textContent = `¡Están listos! Presionen "Comenzar" para iniciar el desafío.`;
                    }, 1000);
                }
            });
        });

        nextBtn.addEventListener('click', () => {
            if (currentQuestion < questions.length) {
                questionBox.textContent = `${currentQuestion + 1}. ${questions[currentQuestion]}`;
                currentQuestion++;
                nextBtn.textContent = 'Siguiente';
                if (currentQuestion === questions.length) {
                    nextBtn.textContent = '¡Mirada de 4 minutos!';
                }
            } else {
                startFinalTimer();
            }
        });

        disabledCard.addEventListener('click', () => {
            alert('¡Ups! Ya hemos ido a esta aventura. Por favor, elige otra tarjeta.');
        });

        function startFinalTimer() {
            document.getElementById('questionContainer').style.display = 'none';
            timerDisplay.style.display = 'block';
            timerDisplay.textContent = 'Ahora, mirense a los ojos por 4 minutos.';

            let timeInSeconds = 4 * 60;
            const timerInterval = setInterval(() => {
                const minutes = Math.floor(timeInSeconds / 60);
                const seconds = timeInSeconds % 60;
                timerDisplay.textContent = `Tiempo restante: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;

                if (timeInSeconds <= 0) {
                    clearInterval(timerInterval);
                    timerDisplay.style.display = 'none';
                    showProposal();
                }
                timeInSeconds--;
            }, 1000);
        }

        function showProposal() {
            finalMessage.style.display = 'block';
            finalMessage.textContent = '¿Quieres ser mi novia?';
        }
    </script>
</body>
</html>
