<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Инженерный Калькулятор</title>
   <style>
.calculator {
  width: 250px;
  margin: 50px auto;
  border: 2px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

#display {
  width: 25%;
  height: 50px;
  margin-bottom: 15px;
  font-size: 24px;
  padding: 5px;
  box-sizing: border-box;
  text-align: right;
  border: 2px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 5px;
}

button {
  width: 25%;
  height: 50px;
  font-size: 20px;
  background-color: #e0e0e0;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #d0d0d0;
}

button:active {
  background-color: #ccc;
}

button.operator {
  background-color: #f39c12;
  color: #fff;
}

button.operator:hover {
  background-color: #e67e22;
}

button.clear {
  background-color: #e74c3c;
  color: #fff;
}

button.clear:hover {
  background-color: #c0392b;
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
