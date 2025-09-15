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
            color: #d32f2f;
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

        .special-event {
            margin-top: 40px;
            text-align: left;
            padding: 20px;
            max-width: 800px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            opacity: 0;
            transform: scale(0.8);
            transition: opacity 0.8s ease-in-out, transform 0.8s ease-in-out;
            display: none;
        }

        .special-event.show {
            opacity: 1;
            transform: scale(1);
            display: block;
        }

        .question-box {
            text-align: center;
            font-size: 1.4em;
            margin-bottom: 20px;
            min-height: 80px;
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

        #timerSection {
            text-align: center;
            display: none;
        }
        #timerInstructions {
            font-size: 1.8em;
            font-weight: bold;
            color: #d32f2f;
            margin-top: 20px;
            text-shadow: 1px 1px 2px #000;
        }
        #timerContinueBtn {
            background-color: #d32f2f;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1.1em;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
            margin-top: 20px;
        }
        #timerContinueBtn:hover {
            background-color: #b71c1c;
        }
        
        #finalMessage {
            text-align: center;
            font-size: 2em;
            font-weight: bold;
            color: #d32f2f;
            margin-top: 40px;
            text-shadow: 1px 1px 2px #000;
            transition: opacity 1s ease-in-out;
        }
        
        .confirmation-buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        .confirmation-buttons button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 1.2em;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        .confirmation-buttons button:hover {
            background-color: #45a049;
        }
        
        #finalProposal {
            text-align: center;
            margin-top: 40px;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        #finalProposal p {
            font-size: 3.5em;
            font-weight: bold;
            color: #d32f2f;
            text-shadow: 3px 3px 6px #000;
            margin: 0;
            line-height: 1.2;
            animation: fadeIn 2s forwards;
        }
        
        .proposal-lang {
            display: none;
            animation: pulse 1.5s infinite;
        }

        /* Efectos de decoración */
        .butterfly, .dandelion {
            position: absolute;
            font-size: 3em;
            color: #fff;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
            animation: float 20s infinite linear;
            pointer-events: none;
            opacity: 0.8;
            z-index: 1;
        }
        .butterfly-1 { top: 10%; left: 5%; animation-duration: 22s; }
        .butterfly-2 { top: 40%; right: 10%; animation-duration: 25s; }
        .butterfly-3 { top: 25%; left: 30%; animation-duration: 18s; transform: scale(0.8); }
        .butterfly-4 { bottom: 15%; right: 10%; animation-duration: 23s; transform: scale(0.9); }
        .dandelion-1 { bottom: 15%; left: 20%; animation-duration: 28s; }
        .dandelion-2 { bottom: 30%; right: 25%; animation-duration: 30s; }
        .dandelion-3 { top: 50%; left: 15%; animation-duration: 20s; transform: scale(0.7); }
        .dandelion-4 { top: 5%; right: 20%; animation-duration: 26s; transform: scale(1.1); }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 0.8; }
            50% { transform: translateY(-30px) rotate(8deg); opacity: 1; }
            100% { transform: translateY(0) rotate(0deg); opacity: 0.8; }
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
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
            #timerInstructions {
                font-size: 1.3em;
            }
            #finalProposal p {
                font-size: 2.5em;
            }
        }
    </style>
</head>
<body>
    <div class="butterfly butterfly-1">🦋</div>
    <div class="butterfly butterfly-2">🦋</div>
    <div class="butterfly butterfly-3">🦋</div>
    <div class="butterfly butterfly-4">🦋</div>

    
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
            <h2 id="questionTitle" style="text-align: center; color: #d32f2f;">Desafío de las 36 Preguntas</h2>
            <p id="questionIntro" style="text-align: center;">¡Felicidades! Como parte de nuestra aventura, hoy nos sumergiremos en este desafío para conocernos aún mejor. Tomen su tiempo para responder cada pregunta con honestidad. ¡Adelante!</p>
            <div id="questionBox" class="question-box"></div>
            <div class="controls">
                <button id="nextBtn">Comenzar</button>
            </div>
        </div>
        <div id="timerSection" style="display: none; text-align: center;">
            <p id="timerInstructions">Ahora, mirense a los ojos por 4 minutos. Por favor, usen un temporizador aparte. ¡Este es su momento!</p>
            <button id="timerContinueBtn">Listo, ¡Continuar!</button>
        </div>
        <div id="final-sequence" style="display: none;">
            <p id="finalMessage"></p>
            <div id="confirmation" style="display: none;">
                <div class="confirmation-buttons">
                    <button id="confirmYes">Sí</button>
                </div>
            </div>
            <div id="finalProposal" style="display: none;">
                <p id="proposalText"></p>
            </div>
        </div>
    </div>

    <script>
        const cards = document.querySelectorAll('.scratch-card:not(.disabled)');
        const disabledCard = document.getElementById('card3');
        const winnerMsg = document.getElementById('winnerMsg');
        const specialEvent = document.getElementById('specialEvent');
        const questionContainer = document.getElementById('questionContainer');
        const questionBox = document.getElementById('questionBox');
        const nextBtn = document.getElementById('nextBtn');
        const timerSection = document.getElementById('timerSection');
        const timerInstructions = document.getElementById('timerInstructions');
        const timerContinueBtn = document.getElementById('timerContinueBtn');
        const finalSequence = document.getElementById('final-sequence');
        const finalMessage = document.getElementById('finalMessage');
        const confirmation = document.getElementById('confirmation');
        const confirmYesBtn = document.getElementById('confirmYes');
        const finalProposal = document.getElementById('finalProposal');
        const proposalText = document.getElementById('proposalText');

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
        let confirmationStep = 0;

        const proposalLanguages = [
            '¿Quieres ser mi novia?',
            'Will you be my girlfriend?',
            'Veux-tu être ma petite amie?',
            'Vuoi essere la mia ragazza?',
            'Möchtest du meine Freundin sein?',
            'Você quer ser minha namorada?',
            '你愿意做我的女朋友吗？'
        ];
        let langIndex = 0;
        let langInterval;

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
                        specialEvent.style.display = 'block';
                        setTimeout(() => {
                            specialEvent.classList.add('show');
                            questionBox.textContent = `¡Están listos! Presionen "Comenzar" para iniciar el desafío.`;
                        }, 50);
                    }, 1000);
                }
            });
        });

        nextBtn.addEventListener('click', () => {
            if (currentQuestion < questions.length) {
                questionBox.innerHTML = `<span>${currentQuestion + 1}.</span> ${questions[currentQuestion]}`;
                currentQuestion++;
                nextBtn.textContent = 'Siguiente';
                if (currentQuestion === questions.length) {
                    nextBtn.textContent = '¡Mirada de 4 minutos!';
                }
            } else {
                startTimerInstructions();
            }
        });

        disabledCard.addEventListener('click', () => {
            alert('¡Ups! Ya hemos ido a esta aventura. Por favor, elige otra tarjeta.');
        });
        
        timerContinueBtn.addEventListener('click', () => {
            startFinalSequence();
        });

        confirmYesBtn.addEventListener('click', () => {
            confirmationStep++;
            if (confirmationStep === 1) {
                finalMessage.textContent = '¿Quieres abrirla?';
            } else if (confirmationStep === 2) {
                finalMessage.textContent = 'Segura que la quieres abrir';
            } else if (confirmationStep === 3) {
                finalMessage.textContent = '¿Estás muy segura que la quieres abrir?';
                confirmYesBtn.textContent = 'Sí, muy segura';
            } else if (confirmationStep === 4) {
                confirmation.style.display = 'none';
                finalMessage.style.display = 'none';
                setTimeout(() => {
                    startLanguageProposal();
                }, 1000);
            }
        });

        function startTimerInstructions() {
            questionContainer.style.display = 'none';
            timerSection.style.display = 'block';
            timerInstructions.style.display = 'block';
            timerContinueBtn.style.display = 'block';
        }

        function startFinalSequence() {
            timerSection.style.display = 'none';
            finalSequence.style.display = 'block';
            finalMessage.style.display = 'block';
            finalMessage.textContent = 'Ahora tienes que abrir esta nota.';
            confirmation.style.display = 'block';
            confirmYesBtn.textContent = 'Sí';
            confirmationStep = 0; // Reiniciar el contador para la nueva secuencia
        }

        function startLanguageProposal() {
            finalProposal.style.display = 'block';
            
            langInterval = setInterval(() => {
                proposalText.textContent = proposalLanguages[langIndex];
                langIndex = (langIndex + 1) % proposalLanguages.length;
            }, 1500);
        }
    </script>
</body>
</html>
