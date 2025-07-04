# shK2701.github.io
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Космический Кликер | Яндекс Игры</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: #0f0c29;
            color: white;
            user-select: none;
        }
        #game {
            margin: 0 auto;
            width: 300px;
        }
        #planet {
            width: 200px;
            height: 200px;
            background: url('https://cdn-icons-png.flaticon.com/512/4149/4149666.png') no-repeat center;
            background-size: cover;
            margin: 20px auto;
            cursor: pointer;
            transition: transform 0.1s;
        }
        #planet:active {
            transform: scale(0.95);
        }
        #score {
            font-size: 24px;
            margin: 10px;
        }
        button {
            background: #4CAF50;
            border: none;
            color: white;
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
        }
        #shop {
            margin-top: 20px;
            border-top: 1px solid #444;
            padding-top: 10px;
        }
    </style>
</head>
<body>
    <div id="game">
        <h1>Космический Кликер</h1>
        <div id="score">Очки: <span id="points">0</span></div>
        <div id="planet" onclick="clickPlanet()"></div>
        <div id="shop">
            <h3>Улучшения</h3>
            <button onclick="buyUpgrade('autoClick')">Автоклик (10 очков)</button>
            <button onclick="buyUpgrade('doubleClick')">Двойной клик (30 очков)</button>
        </div>
    </div>

    <script>
        let points = 0;
        let upgrades = {
            autoClick: false,
            doubleClick: false
        };

        // Клик по планете
        function clickPlanet() {
            points += upgrades.doubleClick ? 2 : 1;
            updateScore();
        }

        // Покупка улучшений
        function buyUpgrade(type) {
            const cost = { autoClick: 10, doubleClick: 30 }[type];
            if (points >= cost && !upgrades[type]) {
                points -= cost;
                upgrades[type] = true;
                alert(`Улучшение "${type}" куплено!`);
                updateScore();
                
                if (type === 'autoClick') {
                    setInterval(() => { points++; updateScore(); }, 1000);
                }
            } else if (points < cost) {
                alert("Недостаточно очков!");
            }
        }

        // Обновление счета
        function updateScore() {
            document.getElementById("points").textContent = points;
        }
    </script>
</body>
</html>
