<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }
        .calculator {
            width: 220px;
            background: #4285f4;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .screen {
            width: 100%;
            height: 50px;
            background: #000;
            color: #fff;
            text-align: right;
            font-size: 24px;
            border-radius: 5px;
            padding: 5px 10px;
            box-sizing: border-box;
            margin-bottom: 10px;
            overflow: hidden;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        .button {
            width: 100%;
            height: 50px;
            background: #e0e0e0;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .button:active {
            background: #d0d0d0;
        }
        .button.clear {
            grid-column: span 2;
            background: #ff5c5c;
            color: white;
        }
        .button.equals {
            grid-column: span 2;
            background: #4caf50;
            color: white;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="screen" id="screen">0</div>
        <div class="buttons">
            <button class="button">7</button>
            <button class="button">8</button>
            <button class="button">9</button>
            <button class="button">/</button>
            <button class="button">4</button>
            <button class="button">5</button>
            <button class="button">6</button>
            <button class="button">*</button>
            <button class="button">1</button>
            <button class="button">2</button>
            <button class="button">3</button>
            <button class="button">-</button>
            <button class="button">0</button>
            <button class="button">.</button>
            <button class="button equals">=</button>
            <button class="button">+</button>
            <button class="button clear">C</button>
        </div>
    </div>

    <script>
        const screen = document.getElementById('screen');
        const buttons = document.querySelectorAll('.button');

        let currentInput = '';

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const value = button.textContent;

                if (value === 'C') {
                    currentInput = '';
                    screen.textContent = '0';
                } else if (value === '=') {
                    try {
                        currentInput = eval(currentInput).toString();
                        screen.textContent = currentInput;
                    } catch {
                        screen.textContent = 'Error';
                        currentInput = '';
                    }
                } else {
                    if (currentInput === '0' && value !== '.') {
                        currentInput = value;
                    } else {
                        currentInput += value;
                    }
                    screen.textContent = currentInput;
                }
            });
        });
    </script>
</body>
</html>
