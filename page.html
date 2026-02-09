<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        :root {
            color-scheme: light dark;
        }
        * {
            box-sizing: border-box;
        }
        body {
            margin: 0;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: radial-gradient(circle at top, #1f2a44, #0b1020 60%);
            font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
            color: #f5f7ff;
        }
        .game-shell {
            width: min(92vw, 520px);
            background: rgba(18, 28, 52, 0.92);
            border-radius: 18px;
            padding: 24px;
            box-shadow: 0 18px 45px rgba(6, 10, 24, 0.45);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
        }
        h1 {
            font-size: 1.6rem;
            margin: 0;
        }
        .score-board {
            display: flex;
            gap: 12px;
            font-size: 0.95rem;
            background: rgba(255, 255, 255, 0.08);
            padding: 8px 12px;
            border-radius: 999px;
        }
        canvas {
            width: 100%;
            border-radius: 14px;
            background: #0a1226;
            display: block;
            border: 2px solid rgba(255, 255, 255, 0.12);
        }
        .controls {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-top: 18px;
        }
        .controls button {
            background: rgba(255, 255, 255, 0.12);
            border: none;
            color: inherit;
            padding: 12px 0;
            border-radius: 10px;
            font-size: 1rem;
            cursor: pointer;
            transition: transform 0.1s ease, background 0.2s ease;
        }
        .controls button:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-1px);
        }
        .controls .primary {
            background: #38bdf8;
            color: #0b1020;
            font-weight: 600;
        }
        .hint {
            margin-top: 12px;
            font-size: 0.9rem;
            color: rgba(245, 247, 255, 0.75);
        }
        .footer {
            margin-top: 16px;
            font-size: 0.85rem;
            color: rgba(245, 247, 255, 0.6);
        }
    </style>
</head>
<body>
    <div class="game-shell">
        <header>
            <h1>Snake Rush</h1>
            <div class="score-board">
                <span>Score: <strong id="score">0</strong></span>
                <span>Best: <strong id="best">0</strong></span>
            </div>
        </header>
        <canvas id="board" width="420" height="420" aria-label="Snake game board"></canvas>
        <div class="controls">
            <button data-direction="ArrowUp">⬆️</button>
            <button class="primary" id="start">Start / Pause</button>
            <button data-direction="ArrowRight">➡️</button>
            <button data-direction="ArrowLeft">⬅️</button>
            <button id="reset">Reset</button>
            <button data-direction="ArrowDown">⬇️</button>
        </div>
        <p class="hint">Use arrow keys or buttons. Eat the glowing orb to grow longer.</p>
        <div class="footer">Speed increases every 5 points. Pause anytime with spacebar.</div>
    </div>

    <script>
        const canvas = document.getElementById("board");
        const ctx = canvas.getContext("2d");
        const scoreEl = document.getElementById("score");
        const bestEl = document.getElementById("best");
        const startButton = document.getElementById("start");
        const resetButton = document.getElementById("reset");
        const controlButtons = document.querySelectorAll("[data-direction]");

        const gridSize = 20;
        const tileCount = canvas.width / gridSize;

        let snake = [
            { x: 10, y: 11 },
            { x: 9, y: 11 },
            { x: 8, y: 11 }
        ];
        let direction = { x: 1, y: 0 };
        let pendingDirection = direction;
        let food = { x: 15, y: 10 };
        let score = 0;
        let bestScore = Number(localStorage.getItem("snake-best")) || 0;
        let running = false;
        let speed = 140;
        let loopId = null;

        bestEl.textContent = bestScore;

        const drawBackground = () => {
            ctx.fillStyle = "#0a1226";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.strokeStyle = "rgba(255, 255, 255, 0.06)";
            for (let i = 0; i <= tileCount; i += 1) {
                const pos = i * gridSize;
                ctx.beginPath();
                ctx.moveTo(pos, 0);
                ctx.lineTo(pos, canvas.height);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(0, pos);
                ctx.lineTo(canvas.width, pos);
                ctx.stroke();
            }
        };

        const drawSnake = () => {
            snake.forEach((segment, index) => {
                const gradient = ctx.createLinearGradient(
                    segment.x * gridSize,
                    segment.y * gridSize,
                    (segment.x + 1) * gridSize,
                    (segment.y + 1) * gridSize
                );
                gradient.addColorStop(0, index === 0 ? "#38bdf8" : "#4ade80");
                gradient.addColorStop(1, "#22d3ee");
                ctx.fillStyle = gradient;
                ctx.fillRect(
                    segment.x * gridSize + 2,
                    segment.y * gridSize + 2,
                    gridSize - 4,
                    gridSize - 4
                );
            });
        };

        const drawFood = () => {
            const centerX = food.x * gridSize + gridSize / 2;
            const centerY = food.y * gridSize + gridSize / 2;
            const radius = gridSize / 2.5;
            const gradient = ctx.createRadialGradient(
                centerX,
                centerY,
                2,
                centerX,
                centerY,
                radius
            );
            gradient.addColorStop(0, "#facc15");
            gradient.addColorStop(1, "#f97316");
            ctx.fillStyle = gradient;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
            ctx.fill();
        };

        const placeFood = () => {
            let newFood = null;
            do {
                newFood = {
                    x: Math.floor(Math.random() * tileCount),
                    y: Math.floor(Math.random() * tileCount)
                };
            } while (snake.some(segment => segment.x === newFood.x && segment.y === newFood.y));
            food = newFood;
        };

        const updateScore = () => {
            scoreEl.textContent = score;
            if (score > bestScore) {
                bestScore = score;
                bestEl.textContent = bestScore;
                localStorage.setItem("snake-best", bestScore);
            }
        };

        const resetGame = () => {
            snake = [
                { x: 10, y: 11 },
                { x: 9, y: 11 },
                { x: 8, y: 11 }
            ];
            direction = { x: 1, y: 0 };
            pendingDirection = direction;
            score = 0;
            speed = 140;
            updateScore();
            placeFood();
            draw();
        };

        const checkCollision = head => {
            if (head.x < 0 || head.x >= tileCount || head.y < 0 || head.y >= tileCount) {
                return true;
            }
            return snake.some((segment, index) => index !== 0 && segment.x === head.x && segment.y === head.y);
        };

        const step = () => {
            direction = pendingDirection;
            const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };

            if (checkCollision(head)) {
                running = false;
                startButton.textContent = "Start";
                clearTimeout(loopId);
                return;
            }

            snake.unshift(head);

            if (head.x === food.x && head.y === food.y) {
                score += 1;
                if (score % 5 === 0 && speed > 70) {
                    speed -= 10;
                }
                updateScore();
                placeFood();
            } else {
                snake.pop();
            }

            draw();
            if (running) {
                loopId = setTimeout(step, speed);
            }
        };

        const draw = () => {
            drawBackground();
            drawFood();
            drawSnake();
        };

        const setDirection = newDirection => {
            const opposite = newDirection.x === -direction.x && newDirection.y === -direction.y;
            if (!opposite) {
                pendingDirection = newDirection;
            }
        };

        const handleKey = event => {
            const mapping = {
                ArrowUp: { x: 0, y: -1 },
                ArrowDown: { x: 0, y: 1 },
                ArrowLeft: { x: -1, y: 0 },
                ArrowRight: { x: 1, y: 0 }
            };
            if (event.code === "Space") {
                toggleGame();
                return;
            }
            const next = mapping[event.key];
            if (next) {
                setDirection(next);
            }
        };

        const toggleGame = () => {
            running = !running;
            startButton.textContent = running ? "Pause" : "Start";
            if (running) {
                step();
            } else {
                clearTimeout(loopId);
            }
        };

        document.addEventListener("keydown", handleKey);

        controlButtons.forEach(button => {
            button.addEventListener("click", () => {
                const key = button.dataset.direction;
                const mapping = {
                    ArrowUp: { x: 0, y: -1 },
                    ArrowDown: { x: 0, y: 1 },
                    ArrowLeft: { x: -1, y: 0 },
                    ArrowRight: { x: 1, y: 0 }
                };
                setDirection(mapping[key]);
            });
        });

        startButton.addEventListener("click", toggleGame);
        resetButton.addEventListener("click", () => {
            running = false;
            startButton.textContent = "Start";
            clearTimeout(loopId);
            resetGame();
        });

        resetGame();
    </script>
</body>
</html>
