<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мины - Простая версия</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        
        .game-container {
            max-width: 800px;
            width: 100%;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            border: 2px solid rgba(255, 255, 255, 0.2);
            text-align: center;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 10px;
            text-shadow: 3px 3px 0 rgba(0, 0, 0, 0.2);
            color: #fff;
            letter-spacing: 2px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 30px;
            color: rgba(255, 255, 255, 0.9);
        }
        
        .game-info {
            display: flex;
            justify-content: space-around;
            background: rgba(0, 0, 0, 0.3);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            border: 2px solid rgba(255, 255, 255, 0.1);
        }
        
        .info-box {
            text-align: center;
        }
        
        .info-value {
            font-size: 2.8rem;
            font-weight: bold;
            color: #ffd700;
            text-shadow: 2px 2px 0 rgba(0, 0, 0, 0.3);
        }
        
        .info-label {
            font-size: 1.1rem;
            color: rgba(255, 255, 255, 0.8);
            margin-top: 5px;
        }
        
        .level-selector {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }
        
        .level-btn {
            padding: 12px 25px;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            min-width: 120px;
        }
        
        .level-btn:hover {
            transform: translateY(-3px);
            background: rgba(255, 255, 255, 0.3);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .level-btn.active {
            background: linear-gradient(135deg, #ffd700 0%, #ff8c00 100%);
            color: #333;
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.4);
        }
        
        .score-sequence {
            background: rgba(0, 0, 0, 0.2);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            border: 1px dashed rgba(255, 255, 255, 0.3);
        }
        
        .score-sequence h3 {
            margin-bottom: 10px;
            color: #ffd700;
        }
        
        .sequence-numbers {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .sequence-number {
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 15px;
            border-radius: 5px;
            font-weight: bold;
            min-width: 60px;
            transition: all 0.3s ease;
        }
        
        .sequence-number.current {
            background: linear-gradient(135deg, #00ff88 0%, #00cc66 100%);
            color: #000;
            transform: scale(1.1);
            box-shadow: 0 0 15px rgba(0, 255, 136, 0.5);
        }
        
        .game-board {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 12px;
            margin: 30px auto;
            max-width: 500px;
        }
        
        .cell {
            aspect-ratio: 1;
            background: linear-gradient(145deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.05));
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.8rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 3px solid rgba(255, 255, 255, 0.1);
            user-select: none;
            position: relative;
            overflow: hidden;
        }
        
        .cell:before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(135deg, transparent 30%, rgba(255, 255, 255, 0.1) 50%, transparent 70%);
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .cell:hover:before {
            opacity: 1;
        }
        
        .cell:hover {
            transform: scale(1.08);
            border-color: rgba(255, 255, 255, 0.3);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .cell.revealed {
            background: linear-gradient(145deg, rgba(0, 200, 255, 0.3), rgba(0, 150, 200, 0.2));
            cursor: default;
            transform: none;
        }
        
        .cell.revealed:hover {
            transform: none;
            border-color: rgba(255, 255, 255, 0.1);
            box-shadow: none;
        }
        
        .cell.mine {
            background: linear-gradient(145deg, #ff416c, #ff4b2b);
            animation: explode 0.5s ease;
            color: white;
        }
        
        .cell.treasure {
            background: linear-gradient(145deg, #00ff88, #00cc66);
            color: #000;
            animation: bounce 0.5s ease;
        }
        
        @keyframes bounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.15); }
        }
        
        @keyframes explode {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }
        
        .control-btn {
            padding: 16px 35px;
            border: none;
            border-radius: 50px;
            font-size: 1.2rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 180px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .start-btn {
            background: linear-gradient(135deg, #00ff88 0%, #00cc66 100%);
            color: #000;
        }
        
        .start-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 255, 136, 0.4);
        }
        
        .restart-btn {
            background: linear-gradient(135deg, #ff416c 0%, #ff4b2b 100%);
            color: white;
        }
        
        .restart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(255, 65, 108, 0.4);
        }
        
        .restart-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .message-box {
            background: rgba(0, 0, 0, 0.4);
            padding: 25px;
            border-radius: 15px;
            margin-top: 30px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .message {
            font-size: 1.5rem;
            font-weight: bold;
            color: #ffd700;
        }
        
        .win-message {
            color: #00ff88 !important;
            text-shadow: 0 0 10px rgba(0, 255, 136, 0.5);
        }
        
        .lose-message {
            color: #ff416c !important;
            text-shadow: 0 0 10px rgba(255, 65, 108, 0.5);
        }
        
        .instructions {
            background: rgba(0, 0, 0, 0.2);
            padding: 20px;
            border-radius: 15px;
            margin-top: 40px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            text-align: left;
        }
        
        .instructions h3 {
            color: #ffd700;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .instructions ul {
            list-style-type: none;
            padding: 0;
        }
        
        .instructions li {
            margin-bottom: 12px;
            padding-left: 25px;
            position: relative;
            color: rgba(255, 255, 255, 0.9);
        }
        
        .instructions li:before {
            content: '►';
            color: #00ff88;
            position: absolute;
            left: 0;
        }
        
        @media (max-width: 600px) {
            .game-board {
                grid-template-columns: repeat(5, 1fr);
                gap: 8px;
            }
            
            .cell {
                font-size: 1.5rem;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            .control-btn {
                width: 100%;
                max-width: 300px;
            }
            
            .level-selector {
                flex-direction: column;
                align-items: center;
            }
            
            .level-btn {
                width: 100%;
                max-width: 250px;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>МИНЫ</h1>
        <p class="subtitle">Найди все сокровища и избегай ловушек!</p>
        
        <div class="game-info">
            <div class="info-box">
                <div class="info-value" id="score">0</div>
                <div class="info-label">СЧЕТ</div>
            </div>
            <div class="info-box">
                <div class="info-value" id="level">5</div>
                <div class="info-label">ЛОВУШЕК</div>
            </div>
            <div class="info-box">
                <div class="info-value" id="multiplier">1x</div>
                <div class="info-label">КОЭФФИЦИЕНТ</div>
            </div>
        </div>
        
        <div class="level-selector">
            <button class="level-btn" data-level="3">Легко (3 ловушки)</button>
            <button class="level-btn active" data-level="5">Средне (5 ловушек)</button>
            <button class="level-btn" data-level="10">Сложно (10 ловушек)</button>
        </div>
        
        <div class="score-sequence">
            <h3>Последовательность очков:</h3>
            <div class="sequence-numbers" id="sequenceNumbers">
                <!-- Последовательность очков будет здесь -->
            </div>
        </div>
        
        <div class="game-board" id="gameBoard">
            <!-- Игровое поле будет сгенерировано здесь -->
        </div>
        
        <div class="controls">
            <button class="control-btn start-btn" id="startBtn">НАЧАТЬ ИГРУ</button>
            <button class="control-btn restart-btn" id="restartBtn" disabled>ИГРАТЬ СНОВА</button>
        </div>
        
        <div class="message-box" id="messageBox" style="display: none;">
            <div class="message" id="message">Сообщение о результате игры</div>
        </div>
        
        <div class="instructions">
            <h3>Правила игры:</h3>
            <ul>
                <li>Выбери уровень сложности (количество ловушек)</li>
                <li>Нажми "НАЧАТЬ ИГРУ"</li>
                <li>Кликай на клетки, чтобы находить сокровища</li>
                <li>За каждое сокровище твой счет удваивается</li>
                <li>Если найдешь ловушку - игра окончена</li>
                <li>Нажми "ИГРАТЬ СНОВА" для новой попытки</li>
                <li>Цель: набрать максимальное количество очков!</li>
            </ul>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Элементы DOM
            const gameBoard = document.getElementById('gameBoard');
            const startBtn = document.getElementById('startBtn');
            const restartBtn = document.getElementById('restartBtn');
            const scoreElement = document.getElementById('score');
            const levelElement = document.getElementById('level');
            const multiplierElement = document.getElementById('multiplier');
            const messageBox = document.getElementById('messageBox');
            const messageElement = document.getElementById('message');
            const sequenceNumbersElement = document.getElementById('sequenceNumbers');
            const levelButtons = document.querySelectorAll('.level-btn');
            
            // Игровые переменные
            let score = 0;
            let currentMultiplier = 1;
            let gameActive = false;
            let mines = [];
            let revealedCells = [];
            let gameCells = [];
            let currentLevel = 5;
            let safeCellsFound = 0;
            
            // Последовательность очков: 10, 20, 40, 80, 160...
            const scoreSequence = [];
            let baseScore = 10;
            for (let i = 0; i < 25; i++) {
                scoreSequence.push(baseScore * Math.pow(2, i));
            }
            
            // Инициализация игрового поля
            function initGameBoard() {
                gameBoard.innerHTML = '';
                gameCells = [];
                
                for (let i = 0; i < 25; i++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    cell.dataset.index = i;
                    cell.textContent = '?';
                    
                    cell.addEventListener('click', () => revealCell(i));
                    
                    gameBoard.appendChild(cell);
                    gameCells.push(cell);
                }
            }
            
            // Обновление последовательности очков
            function updateScoreSequence() {
                sequenceNumbersElement.innerHTML = '';
                const maxToShow = 25 - currentLevel;
                
                for (let i = 0; i < Math.min(8, maxToShow); i++) {
                    const seqEl = document.createElement('div');
                    seqEl.className = 'sequence-number';
                    seqEl.textContent = scoreSequence[i];
                    sequenceNumbersElement.appendChild(seqEl);
                }
                
                if (maxToShow > 8) {
                    const dots = document.createElement('div');
                    dots.className = 'sequence-number';
                    dots.textContent = '...';
                    sequenceNumbersElement.appendChild(dots);
                    
                    const last = document.createElement('div');
                    last.className = 'sequence-number';
                    last.textContent = scoreSequence[maxToShow - 1];
                    sequenceNumbersElement.appendChild(last);
                }
            }
            
            // Подсветка текущего значения в последовательности
            function highlightCurrentSequence() {
                const seqNumbers = document.querySelectorAll('.sequence-number');
                seqNumbers.forEach((el, index) => {
                    el.classList.remove('current');
                    if (el.textContent !== '...' && parseInt(el.textContent) === score) {
                        el.classList.add('current');
                    }
                });
            }
            
            // Начало новой игры
            function startGame() {
                if (gameActive) return;
                
                // Сброс значений
                score = 0;
                currentMultiplier = 1;
                safeCellsFound = 0;
                revealedCells = [];
                
                // Генерация ловушек
                mines = generateMines(currentLevel);
                
                // Сброс поля
                gameCells.forEach(cell => {
                    cell.className = 'cell';
                    cell.textContent = '?';
                });
                
                // Обновление UI
                updateScoreSequence();
                updateUI();
                
                // Активация игры
                gameActive = true;
                startBtn.disabled = true;
                restartBtn.disabled = true;
                messageBox.style.display = 'none';
                
                // Подсветка последовательности
                highlightCurrentSequence();
                
                showMessage(`Игра началась! Найди все сокровища и избегай ${currentLevel} ловушек!`);
            }
            
            // Генерация позиций ловушек
            function generateMines(count) {
                const positions = new Set();
                
                while (positions.size < count) {
                    const pos = Math.floor(Math.random() * 25);
                    positions.add(pos);
                }
                
                return Array.from(positions);
            }
            
            // Открытие клетки
            function revealCell(index) {
                if (!gameActive || revealedCells.includes(index)) return;
                
                revealedCells.push(index);
                const cell = gameCells[index];
                
                if (mines.includes(index)) {
                    // Игрок попал на ловушку
                    cell.className = 'cell mine';
                    cell.textContent = '💣';
                    endGame(false);
                } else {
                    // Нашел сокровище
                    cell.className = 'cell treasure';
                    cell.textContent = '💎';
                    
                    // Увеличиваем счет
                    safeCellsFound++;
                    score = scoreSequence[safeCellsFound - 1];
                    currentMultiplier = Math.pow(2, safeCellsFound);
                    
                    updateUI();
                    highlightCurrentSequence();
                    
                    // Проверка на победу (найдены все безопасные клетки)
                    if (safeCellsFound === 25 - currentLevel) {
                        endGame(true);
                    }
                }
            }
            
            // Завершение игры
            function endGame(win) {
                gameActive = false;
                
                // Показываем все ловушки
                mines.forEach(mineIndex => {
                    if (!revealedCells.includes(mineIndex)) {
                        gameCells[mineIndex].className = 'cell mine';
                        gameCells[mineIndex].textContent = '💣';
                    }
                });
                
                // Показываем сообщение
                if (win) {
                    showMessage(`ПОБЕДА! Ты нашел все ${25 - currentLevel} сокровищ! Финальный счет: ${score}`, true);
                } else {
                    showMessage(`Игра окончена! Ловушка! Твой счет: ${score}`, false);
                }
                
                // Активируем кнопку "Играть снова"
                restartBtn.disabled = false;
                startBtn.disabled = false;
            }
            
            // Обновление интерфейса
            function updateUI() {
                scoreElement.textContent = score;
                levelElement.textContent = currentLevel;
                multiplierElement.textContent = `${currentMultiplier}x`;
            }
            
            // Показать сообщение
            function showMessage(text, isWin = null) {
                messageElement.textContent = text;
                messageBox.style.display = 'block';
                
                if (isWin === true) {
                    messageElement.className = 'message win-message';
                } else if (isWin === false) {
                    messageElement.className = 'message lose-message';
                } else {
                    messageElement.className = 'message';
                }
            }
            
            // Обработчики событий
            startBtn.addEventListener('click', startGame);
            
            restartBtn.addEventListener('click', () => {
                startGame();
            });
            
            // Выбор уровня сложности
            levelButtons.forEach(btn => {
                btn.addEventListener('click', () => {
                    // Удаляем активный класс у всех кнопок
                    levelButtons.forEach(b => b.classList.remove('active'));
                    // Добавляем активный класс текущей кнопке
                    btn.classList.add('active');
                    // Обновляем текущий уровень
                    currentLevel = parseInt(btn.dataset.level);
                    levelElement.textContent = currentLevel;
                    // Обновляем последовательность очков
                    updateScoreSequence();
                });
            });
            
            // Инициализация
            initGameBoard();
            updateUI();
            updateScoreSequence();
            
            // Показываем начальное сообщение
            showMessage('Выбери уровень сложности и нажми "НАЧАТЬ ИГРУ"!');
        });
    </script>
</body>
</html>
