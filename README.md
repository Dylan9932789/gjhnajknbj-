<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Инженерный Калькулятор</title>
   <style>
.calculator {
  width: 300px;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  background-color: #f9f9f9;
}

.display {
  height: 50px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
  text-align: right;
  padding: 5px;
  font-size: 20px;
}

.button {
  width: 50px;
  height: 50px;
  margin: 5px;
  background-color: #eee;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}

.button:hover {
  background-color: #ddd;
}

.operation-button {
  background-color: #f2a154;
  color: #fff;
}

.operation-button:hover {
  background-color: #d98c42;
}

.number-button {
  background-color: #4caf50;
  color: #fff;
}

.number-button:hover {
  background-color: #388e3c;
}

.equal-button {
  background-color: #2196f3;
  color: #fff;
}

.equal-button:hover {
  background-color: #1976d2;
}

.clear-button {
  background-color: #f44336;
  color: #fff;
}

.clear-button:hover {
  background-color: #d32f2f;
}
    </style>
</head>
<body>
    <input type="text" id="display" readonly>
    <br>
    <button onclick="clearDisplay()">C</button>
    <button onclick="backspace()">⌫</button>
    <button onclick="appendToDisplay('customSin(')">sin</button>
    <button onclick="appendToDisplay('customCos(')">cos</button>
    <button onclick="appendToDisplay('customTan(')">tg</button>
    <br>
    <button onclick="appendToDisplay('Math.log(')">log</button>
    <button onclick="appendToDisplay('Math.exp(')">exp</button>
    <button onclick="appendToDisplay('customSqrt(')">√</button>
    <button onclick="appendToDisplay('Math.PI')">π</button>
    <button onclick="appendToDisplay('**')">^</button>
    <br>
    <button onclick="appendToDisplay('7')">7</button>
    <button onclick="appendToDisplay('8')">8</button>
    <button onclick="appendToDisplay('9')">9</button>
    <button onclick="appendToDisplay('+')">+</button>
    <button onclick="appendToDisplay('-')">-</button>
    <br>
    <button onclick="appendToDisplay('4')">4</button>
    <button onclick="appendToDisplay('5')">5</button>
    <button onclick="appendToDisplay('6')">6</button>
    <button onclick="appendToDisplay('*')">*</button>
    <button onclick="appendToDisplay('/')">/</button>
    <br>
    <button onclick="appendToDisplay('1')">1</button>
    <button onclick="appendToDisplay('2')">2</button>
    <button onclick="appendToDisplay('3')">3</button>
    <button onclick="appendToDisplay('('">(</button>
    <button onclick="appendToDisplay(')')">)</button>
    <br>
    <button onclick="appendToDisplay('0')">0</button>
    <button onclick="appendToDisplay('.')">.</button>
    <button onclick="calculate()">=</button>
    <button onclick="appendToDisplay('Math.abs(')">|x|</button>
    <button onclick="appendToDisplay('!')">!</button>
 
    <script>
        function appendToDisplay(value) {
            document.getElementById('display').value += value;
        }

        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        function backspace() {
            var currentValue = document.getElementById('display').value;
            document.getElementById('display').value = currentValue.substring(0, currentValue.length - 1);
        }

        function calculate() {
            try {
                var expression = document.getElementById('display').value.replace(/\*\*/g, '^');
                expression = expression.replace(/(\d+)!/g, function(match, p1) {
                    return factorial(parseInt(p1));
                });

                expression = expression.replace(/Math.sin\(/g, 'customSin(');
                expression = expression.replace(/Math.cos\(/g, 'customCos(');
                expression = expression.replace(/Math.tg\(/g, 'customTan(');
                expression = expression.replace(/Math.sqrt\(/g, 'customSqrt(');

                var result = eval(expression);
                document.getElementById('display').value = result;
            } catch (error) {
                document.getElementById('display').value = 'Ошибка';
            }
        }

        function factorial(n) {
            if (n === 0 || n === 1) {
                return 1;
            }
            return n * factorial(n - 1);
        }

        function customSin(value) {
            var radians = value * Math.PI / 180;
            return Math.sin(radians);
        }

        function customCos(value) {
            var radians = value * Math.PI / 180;
            return Math.cos(radians);
        }

        function customTan(value) {
            var radians = value * Math.PI / 180;
            return Math.tan(radians);
        }

        function customSqrt(value) {
            if (value < 0) {
                return 'Ошибка: Квадратный корень из отрицательного числа';
            }
            return Math.sqrt(value);
        }

        // Keyboard input handling
        document.addEventListener('keydown', function(event) {
            // Allow numbers, operators, and some special keys
            if (/[\d\+\-\*\/\(\)\.\^]/.test(event.key)) {
                appendToDisplay(event.key);
            } else if (event.key === 'Enter') {
                calculate();
            } else if (event.key === 'Backspace') {
                backspace();
            }
        });
    </script>

<li> ВНИМАНИЕ  для Работоспособность калькулятора при выполнении 
функции  sin cos tg  корень из числа 
 нужно  при вписании  цифры  закрыть скобку </li>
 
    <p>&copy; 2024 Разработчик  Dylan933 Все права защищены. | <span id="companyLink"></span></p>
