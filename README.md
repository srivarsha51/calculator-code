# calculator-code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }

        .calculator {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            width: 300px;
            padding: 20px;
        }

        .display {
            background-color: #222;
            color: white;
            font-size: 2em;
            padding: 20px;
            border-radius: 5px;
            text-align: right;
            margin-bottom: 20px;
            height: 60px;
            overflow: hidden;
        }

        .button {
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 20px;
            font-size: 1.5em;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .button:hover {
            background-color: #45a049;
        }

        .button:active {
            background-color: #3e8e41;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .operator {
            background-color: #f39c12;
        }

        .operator:hover {
            background-color: #e67e22;
        }

        .operator:active {
            background-color: #d35400;
        }

        .clear {
            background-color: #e74c3c;
        }

        .clear:hover {
            background-color: #c0392b;
        }

        .clear:active {
            background-color: #a93226;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="grid">
            <button class="button clear" id="clear">C</button>
            <button class="button" id="seven">7</button>
            <button class="button" id="eight">8</button>
            <button class="button" id="nine">9</button>
            <button class="button operator" id="divide">/</button>
            <button class="button" id="four">4</button>
            <button class="button" id="five">5</button>
            <button class="button" id="six">6</button>
            <button class="button operator" id="multiply">*</button>
            <button class="button" id="one">1</button>
            <button class="button" id="two">2</button>
            <button class="button" id="three">3</button>
            <button class="button operator" id="subtract">-</button>
            <button class="button" id="zero">0</button>
            <button class="button operator" id="equals">=</button>
            <button class="button operator" id="add">+</button>
        </div>
    </div>

    <script>
        const display = document.getElementById('display');
        const buttons = document.querySelectorAll('.button');
        let currentInput = '';
        let operator = '';
        let previousInput = '';

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const value = button.innerText;

                if (value === 'C') {
                    clear();
                } else if (value === '=') {
                    calculate();
                } else if (['+', '-', '*', '/'].includes(value)) {
                    setOperator(value);
                } else {
                    appendNumber(value);
                }
            });
        });

        function appendNumber(number) {
            if (currentInput.length < 10) {
                currentInput += number;
                updateDisplay(currentInput);
            }
        }

        function setOperator(op) {
            if (currentInput === '') return;
            if (previousInput !== '') {
                calculate();
            }
            operator = op;
            previousInput = currentInput;
            currentInput = '';
        }

        function calculate() {
            let computation;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);

            if (isNaN(prev) || isNaN(current)) return;

            switch (operator) {
                case '+':
                    computation = prev + current;
                    break;
                case '-':
                    computation = prev - current;
                    break;
                case '*':
                    computation = prev * current;
                    break;
                case '/':
                    computation = prev / current;
                    break;
                default:
                    return;
            }

            currentInput = computation.toString();
            operator = '';
            previousInput = '';
            updateDisplay(currentInput);
        }

        function clear() {
            currentInput = '';
            operator = '';
            previousInput = '';
            updateDisplay('0');
        }

        function updateDisplay(value) {
            display.innerText = value.length > 10 ? value.slice(0, 10) : value;
        }
    </script>
</body>
</html>
