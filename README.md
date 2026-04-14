# How-much-How-many-games
Countable and Uncountable
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>How Much vs How Many Challenge</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&display=swap" rel="stylesheet">
    <style>
        :root {
            --team-a-color: #ff6b6b;
            --team-b-color: #4ecdc4;
            --bg-color: #f7f7f7;
        }

        * {
            box-sizing: border-box;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: 'Fredoka One', cursive;
            background: var(--bg-color);
        }

        /* Start Screen */
        #overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.85);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 100;
            color: white;
            text-align: center;
        }

        button.start-btn {
            background: #ff9f43;
            border: none;
            padding: 20px 50px;
            font-size: 3rem;
            color: white;
            border-radius: 15px;
            cursor: pointer;
            font-family: 'Fredoka One', cursive;
            box-shadow: 0 8px 0 #d35400;
            transition: transform 0.1s;
        }

        button.start-btn:active {
            transform: translateY(4px);
            box-shadow: 0 4px 0 #d35400;
        }

        /* Game Layout */
        .game-container {
            display: flex;
            width: 100vw;
            height: 100vh;
        }

        .side {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-evenly;
            padding: 20px;
            position: relative;
            transition: background 0.3s;
        }

        .side-a { background-color: var(--team-a-color); border-right: 5px solid #333; }
        .side-b { background-color: var(--team-b-color); }

        /* Timer and Score */
        .header {
            position: absolute;
            top: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .score-box {
            font-size: 3rem;
            color: white;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.2);
        }

        #timer-display {
            position: absolute;
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            background: #333;
            color: white;
            padding: 10px 30px;
            border-radius: 30px;
            font-size: 2rem;
            z-index: 10;
        }

        /* Image Display */
        .image-container {
            width: 80%;
            height: 40%;
            background: white;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            overflow: hidden;
            padding: 10px;
        }

        .target-img {
            max-width: 100%;
            max-height: 80%;
            object-fit: contain;
        }

        .item-label {
            font-size: 2rem;
            margin-top: 10px;
            color: #333;
            text-transform: capitalize;
        }

        /* Buttons */
        .btn-group {
            width: 90%;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .game-btn {
            width: 100%;
            padding: 30px 0;
            font-size: 2.5rem;
            border: none;
            border-radius: 20px;
            font-family: 'Fredoka One', cursive;
            cursor: pointer;
            box-shadow: 0 8px 0 rgba(0,0,0,0.2);
            color: white;
        }

        .much-btn { background-color: #9b59b6; }
        .many-btn { background-color: #2ecc71; }

        .game-btn:active {
            transform: translateY(4px);
            box-shadow: 0 4px 0 rgba(0,0,0,0.2);
        }

        /* Feedback Effects */
        .correct { background-color: #27ae60 !important; }
        .wrong { background-color: #c0392b !important; }

        @media (max-width: 600px) {
            .game-btn { font-size: 1.5rem; padding: 15px 0; }
            .item-label { font-size: 1.2rem; }
            .score-box { font-size: 2rem; }
        }
    </style>
</head>
<body>

    <div id="overlay">
        <h1>HOW MUCH vs HOW MANY</h1>
        <p>Team A (Left) vs Team B (Right)</p>
        <button class="start-btn" onclick="startGame()">START!</button>
    </div>

    <div id="timer-display">60</div>

    <div class="game-container">
        <div class="side side-a" id="side-a">
            <div class="header">
                <div class="score-box">TEAM A: <span id="score-a">0</span></div>
            </div>
            <div class="image-container">
                <img src="" class="target-img" id="img-a">
                <div class="item-label" id="label-a">...</div>
            </div>
            <div class="btn-group">
                <button class="game-btn much-btn" ontouchstart="handleAnswer('A', 'much')" mousedown="handleAnswer('A', 'much')">HOW MUCH</button>
                <button class="game-btn many-btn" ontouchstart="handleAnswer('A', 'many')" mousedown="handleAnswer('A', 'many')">HOW MANY</button>
            </div>
        </div>

        <div class="side side-b" id="side-b">
            <div class="header">
                <div class="score-box">TEAM B: <span id="score-b">0</span></div>
            </div>
            <div class="image-container">
                <img src="" class="target-img" id="img-b">
                <div class="item-label" id="label-b">...</div>
            </div>
            <div class="btn-group">
                <button class="game-btn much-btn" ontouchstart="handleAnswer('B', 'much')" mousedown="handleAnswer('B', 'much')">HOW MUCH</button>
                <button class="game-btn many-btn" ontouchstart="handleAnswer('B', 'many')" mousedown="handleAnswer('B', 'many')">HOW MANY</button>
            </div>
        </div>
    </div>

    <script>
        const gameData = [
            { item: "Apples", type: "many", img: "🍎" },
            { item: "Water", type: "much", img: "💧" },
            { item: "Milk", type: "much", img: "🥛" },
            { item: "Books", type: "many", img: "📚" },
            { item: "Rice", type: "much", img: "🍚" },
            { item: "Chairs", type: "many", img: "🪑" },
            { item: "Money", type: "much", img: "💰" },
            { item: "Friends", type: "many", img: "👫" },
            { item: "Sugar", type: "much", img: "🍬" },
            { item: "Trees", type: "many", img: "🌳" },
            { item: "Rain", type: "much", img: "🌧️" },
            { item: "Cars", type: "many", img: "🚗" },
            { item: "Snow", type: "much", img: "❄️" },
            { item: "Pencils", type: "many", img: "✏️" }
        ];

        let scoreA = 0;
        let scoreB = 0;
        let timeLeft = 60;
        let currentItem = null;
        let timerId = null;
        let canAnswerA = true;
        let canAnswerB = true;

        // Prevent double-triggering with touch/mouse
        function handleAnswer(team, choice) {
            if (team === 'A' && !canAnswerA) return;
            if (team === 'B' && !canAnswerB) return;

            const isCorrect = choice === currentItem.type;
            const sideEl = document.getElementById(`side-${team.toLowerCase()}`);
            
            if (isCorrect) {
                if (team === 'A') { scoreA++; document.getElementById('score-a').innerText = scoreA; }
                else { scoreB++; document.getElementById('score-b').innerText = scoreB; }
                
                flashSide(sideEl, 'correct');
            } else {
                flashSide(sideEl, 'wrong');
            }

            // Lock team from answering until next item
            if (team === 'A') canAnswerA = false;
            if (team === 'B') canAnswerB = false;

            // If both answered, or after a short delay, next item
            if (!canAnswerA && !canAnswerB) {
                setTimeout(nextRound, 600);
            }
        }

        function flashSide(element, status) {
            const originalColor = element.classList.contains('side-a') ? 'var(--team-a-color)' : 'var(--team-b-color)';
            element.style.backgroundColor = status === 'correct' ? '#2ecc71' : '#e74c3c';
            setTimeout(() => {
                element.style.backgroundColor = originalColor;
            }, 500);
        }

        function nextRound() {
            canAnswerA = true;
            canAnswerB = true;
            currentItem = gameData[Math.floor(Math.random() * gameData.length)];
            
            // Update UI - Using Text for Emojis as Images for demo simplicity
            // You can replace .innerText with .src if using real image URLs
            document.getElementById('label-a').innerText = currentItem.item;
            document.getElementById('label-b').innerText = currentItem.item;
            
            // Simulating image with a large emoji
            document.getElementById('img-a').style.display = "none"; 
            document.getElementById('img-b').style.display = "none";
            document.getElementById('label-a').innerHTML = `<span style="font-size:5rem">${currentItem.img}</span><br>${currentItem.item}`;
            document.getElementById('label-b').innerHTML = `<span style="font-size:5rem">${currentItem.img}</span><br>${currentItem.item}`;
        }

        function startGame() {
            scoreA = 0;
            scoreB = 0;
            timeLeft = 60;
            document.getElementById('score-a').innerText = "0";
            document.getElementById('score-b').innerText = "0";
            document.getElementById('overlay').style.display = "none";
            
            nextRound();
            
            timerId = setInterval(() => {
                timeLeft--;
                document.getElementById('timer-display').innerText = timeLeft;
                if (timeLeft <= 0) endGame();
            }, 1000);
        }

        function endGame() {
            clearInterval(timerId);
            let resultText = "";
            if (scoreA > scoreB) resultText = "TEAM A WINS! 🏆";
            else if (scoreB > scoreA) resultText = "TEAM B WINS! 🏆";
            else resultText = "IT'S A DRAW! 🤝";

            document.getElementById('overlay').innerHTML = `
                <h1>GAME OVER</h1>
                <h2 style="font-size:3rem">${resultText}</h2>
                <p>Score A: ${scoreA} | Score B: ${scoreB}</p>
                <button class="start-btn" onclick="location.reload()">PLAY AGAIN</button>
            `;
            document.getElementById('overlay').style.display = "flex";
        }

        // Prevent zoom on double tap for iOS
        document.addEventListener('touchstart', (e) => {
            if (e.touches.length > 1) e.preventDefault();
        }, { passive: false });
    </script>
</body>
</html>
