<!DOCTYPE html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Klikačka - Terče</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f4f4f4;
            cursor: crosshair; /* Nastavení kurzoru na křížek */
        }
        #gameArea {
            position: relative;
            width: 80%;
            height: 80%;
            border: 2px solid #000;
            background-image: url('https://www.w3schools.com/html/img_strelnice.jpg'); /* Pozadí střelnice */
            background-size: cover; /* Zajištění, že obrázek vyplní celou herní oblast */
            background-position: center; /* Ucentrování obrázku */
            overflow: hidden;
        }
        .target {
            position: absolute;
            width: 50px;
            height: 50px;
            border-radius: 50%; /* Zaoblení pro kruh */
            background: radial-gradient(circle, red 30%, white 30%, white 60%, red 60%); /* Červené a bílé vrstvy */
            cursor: crosshair; /* Zajištění křížového kurzoru i při kliknutí na terč */
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }
        #score {
            position: fixed;
            top: 10px;
            left: 10px;
            font-size: 24px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div id="score">Body: 0</div>
    <div id="gameArea"></div>

    <!-- Zvuk výstřelu -->
    <audio id="shootSound" src="https://www.soundjay.com/button/beep-07.wav" preload="auto"></audio>

    <script>
        let score = 0;
        const gameArea = document.getElementById('gameArea');
        const scoreDisplay = document.getElementById('score');
        const shootSound = document.getElementById('shootSound');

        // Funkce pro vytvoření nového terče
        function createTarget() {
            const target = document.createElement('div');
            target.classList.add('target');
            
            // Nastavení náhodné pozice terče
            const maxX = gameArea.offsetWidth - 50;
            const maxY = gameArea.offsetHeight - 50;
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            target.style.left = randomX + 'px';
            target.style.top = randomY + 'px';
            
            // Přidání terče do herní oblasti
            gameArea.appendChild(target);
            
            // Přidání události pro kliknutí na terč
            target.addEventListener('click', () => {
                score++;
                scoreDisplay.textContent = `Body: ${score}`;
                target.remove();  // Odstranění terče po kliknutí
                createTarget();  // Vytvoření nového terče
                
                // Přehrání zvuku výstřelu
                shootSound.play().catch(error => {
                    console.log("Zvuk nelze přehrát:", error);
                });
            });
        }

        // Inicializace hry
        createTarget();  // Vytvoření prvního terče

    </script>

</body>
</html>