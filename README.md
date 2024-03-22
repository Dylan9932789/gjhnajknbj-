<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Инженерный Калькулятор</title>
   <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        label {
            display: block;
            margin-bottom: 10px;
        }
        input {
            width: calc(10% - 20px);
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }
        button {
            display: inline-block;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            margin-top: 10px;
            transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out, transform 0.1s ease-in-out;
        }
        button:hover {
            background-color: #45a049;
        }
        button:active {
            transform: translateY(1px);
            box-shadow: none;
        }
        iframe {
            width: 10%;
            height: 50px;
            border: 1px solid #ccc;
            transition: height 0.5s ease-in-out;
        }
        .error {
            color: red;
            margin-top: 10px;
            font-weight: bold;
        }
        p a {
            color: #333;
            text-decoration: none;
            margin-right: 10px;
            padding: 8px 15px;
            border: 2px solid #333;
            border-radius: 5px;
            transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out;
        }
        p a:hover {
            background-color: #333;
            color: #fff;
        }
        h2 {
            font-size: 1.5em;
            margin-bottom: 10px;
            color: #333;
        }
        main {
            border-top: 1px solid #ccc;
            padding-top: 20px;
            margin-top: 20px;
        }
        footer {
            text-align: center;
            padding: 20px;
            background-color: #f4f4f4;
            color: #666;
        }
        footer .error {
            color: red;
            font-weight: bold;
        }
        .controls {
            margin-top: 10px;
        }
    </style>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }

        input {
            width: 200px;
            font-size: 18px;
            padding: 5px;
            margin-bottom: 10px;
        }

        button {
            font-size: 16px;
            padding: 10px;
            margin: 5px;
        } <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            margin: 50px;
            background-color: #f4f4f4;
        }

        input {
            width: 240px;
            font-size: 20px;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        button {
            font-size: 18px;
            padding: 15px 20px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #4caf50;
            color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        button:hover {
            background-color: #45a049;
        }

        .row {
            display: flex;
            justify-content: center;
        }

        .column {
            flex: 20%;
        }

        .calculator-container {
            max-width: 400px;
            margin: 0 auto;
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
  <script src="https://cdn.lordicon.com/lordicon.js"></script>
<lord-icon
    src="https://cdn.lordicon.com/cnpvyndp.json"
    trigger="hover"
    style="width:250px;height:250px">
</lord-icon>

<script src="https://cdn.lordicon.com/lordicon.js"></script>
<lord-icon
    src="https://cdn.lordicon.com/axteoudt.json"
    trigger="hover"
    style="width:250px;height:250px">
</lord-icon>
<li> ВНИМАНИЕ  для Работоспособность калькулятора при выполнении функции  sin cos tg  корень из числа 
 нужно  при вписании  цифры  закрыть скобку </li>
 
    <p>&copy; 2024 Разработчик  Dylan933 Все права защищены. | <span id="companyLink"></span></p>
