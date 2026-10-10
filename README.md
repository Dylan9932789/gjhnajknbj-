html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Инженерный калькулятор — Дилан</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            padding: 25px 12px;
            font-family: Arial, sans-serif;
            background: #e9edf5;
            color: #172033;
        }

        .calculator {
            width: 100%;
            max-width: 460px;
            margin: 0 auto;
            padding: 20px;
            background: #ffffff;
            border-radius: 20px;
            box-shadow: 0 8px 30px #00000018;
        }

        h1 {
            margin: 0 0 18px;
            text-align: center;
            font-size: 25px;
            color: #191970;
        }

        .mode-row {
            display: flex;
            gap: 8px;
            margin-bottom: 12px;
        }

        .mode-row button {
            flex: 1;
            padding: 11px 5px;
            background: #e5e7eb;
            color: #172033;
        }

        .mode-row button.active {
            background: #191970;
            color: white;
        }

        #display {
            width: 100%;
            height: 65px;
            margin-bottom: 8px;
            padding: 12px;
            border: 2px solid #d5dbea;
            border-radius: 10px;
            background: #f8faff;
            color: #172033;
            text-align: right;
            font-size: 25px;
            outline: none;
        }

        #display:focus {
            border-color: #191970;
        }

        #message {
            min-height: 20px;
            margin-bottom: 10px;
            color: #c0392b;
            font-size: 13px;
            text-align: right;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(5, minmax(0, 1fr));
            gap: 8px;
        }

        button {
            min-width: 0;
            min-height: 48px;
            padding: 8px 3px;
            border: none;
            border-radius: 9px;
            background: #eef1f8;
            color: #172033;
            font-size: 17px;
            cursor: pointer;
            transition: background 0.15s, transform 0.1s;
            touch-action: manipulation;
        }

        button:hover {
            background: #dce4f5;
        }

        button:active {
            transform: scale(0.96);
        }

        button.function {
            background: #dfe6fa;
            color: #191970;
        }

        button.operator {
            background: #d8e4ff;
            color: #191970;
            font-weight: bold;
        }

        button.clear {
            background: #ffe2e2;
            color: #a51f1f;
        }

        button.equal {
            background: #191970;
            color: white;
            font-size: 23px;
        }

        button.equal:hover {
            background: #3030a0;
        }

        .history-title {
            margin-top: 22px;
            margin-bottom: 8px;
            font-weight: bold;
            color: #191970;
        }

        #history {
            max-height: 130px;
            overflow-y: auto;
            font-size: 14px;
            color: #515b70;
        }

        .history-item {
            padding: 7px 3px;
            border-bottom: 1px solid #edf0f5;
            overflow-wrap: anywhere;
            cursor: pointer;
        }

        .history-item:hover {
            background: #f2f5fb;
        }

        .footer {
            margin-top: 20px;
            text-align: center;
            color: #687386;
            font-size: 12px;
        }

        @media (max-width: 380px) {
            body {
                padding: 10px 6px;
            }

            .calculator {
                padding: 12px;
                border-radius: 14px;
            }

            .buttons {
                gap: 5px;
            }

            button {
                min-height: 44px;
                font-size: 15px;
            }

            #display {
                font-size: 21px;
            }

            h1 {
                font-size: 21px;
            }
        }
    </style>
</head>

<body>

<div class="calculator">
    <h1>Инженерный калькулятор</h1>

    <div class="mode-row">
        <button id="degButton" class="active"
                onclick="setAngleMode('DEG')">Градусы</button>
        <button id="radButton"
                onclick="setAngleMode('RAD')">Радианы</button>
    </div>

    <input id="display" type="text"
           placeholder="Введите выражение"
           autocomplete="off"
           spellcheck="false">

    <div id="message"></div>

    <div class="buttons">
        <button class="clear" onclick="clearDisplay()">C</button>
        <button class="clear" onclick="backspace()">⌫</button>
        <button class="function" onclick="append('(')">(</button>
        <button class="function" onclick="append(')')">)</button>
        <button class="operator" onclick="append('/')">÷</button>

        <button class="function" onclick="append('sin(')">sin</button>
        <button class="function" onclick="append('cos(')">cos</button>
        <button class="function" onclick="append('tg(')">tg</button>
        <button class="function" onclick="append('sqrt(')">√</button>
        <button class="operator" onclick="append('*')">×</button>

        <button class="function" onclick="append('ln(')">ln</button>
        <button class="function" onclick="append('log10(')">log₁₀</button>
        <button class="function" onclick="append('exp(')">exp</button>
        <button class="function" onclick="append('abs(')">|x|</button>
        <button class="operator" onclick="append('-')">−</button>

        <button onclick="append('7')">7</button>
        <button onclick="append('8')">8</button>
        <button onclick="append('9')">9</button>
        <button class="operator" onclick="append('^')">xʸ</button>
        <button class="operator" onclick="append('+')">+</button>

        <button onclick="append('4')">4</button>
        <button onclick="append('5')">5</button>
        <button onclick="append('6')">6</button>
        <button class="function" onclick="append('!')">n!</button>
        <button class="function" onclick="append('%')">%</button>

        <button onclick="append('1')">1</button>
        <button onclick="append('2')">2</button>
        <button onclick="append('3')">3</button>
        <button class="function" onclick="append('^2')">x²</button>
        <button class="function" onclick="append('pi')">π</button>

        <button onclick="append('0')">0</button>
        <button onclick="append('.')">.</button>
        <button class="function" onclick="append('e')">e</button>
        <button class="function" onclick="append('ans')">Ans</button>
        <button class="equal" onclick="calculate()">=</button>
    </div>

    <div class="history-title">История вычислений</div>
    <div id="history"></div>

    <div class="footer">
        © 2026 Дилан. Инженерный калькулятор.
    </div>
</div>

<script>
    const display = document.getElementById("display");
    const message = document.getElementById("message");
    const historyBox = document.getElementById("history");

    let angleMode = "DEG";
    let lastAnswer = 0;
    let history = [];

    function setAngleMode(mode) {
        angleMode = mode;

        document.getElementById("degButton")
            .classList.toggle("active", mode === "DEG");

        document.getElementById("radButton")
            .classList.toggle("active", mode === "RAD");

        message.textContent =
            mode === "DEG" ? "Режим: градусы" : "Режим: радианы";
    }

    function append(value) {
        const start = display.selectionStart;
        const end = display.selectionEnd;
        const text = display.value;

        display.value =
            text.slice(0, start) + value + text.slice(end);

        const position = start + value.length;
        display.setSelectionRange(position, position);
        display.focus();
        message.textContent = "";
    }

    function clearDisplay() {
        display.value = "";
        message.textContent = "";
        display.focus();
    }

    function backspace() {
        const start = display.selectionStart;
        const end = display.selectionEnd;
        const text = display.value;

        if (start !== end) {
            display.value = text.slice(0, start) + text.slice(end);
            display.setSelectionRange(start, start);
        } else if (start > 0) {
            display.value =
                text.slice(0, start - 1) + text.slice(end);

            display.setSelectionRange(start - 1, start - 1);
        }

        display.focus();
    }

    // Разбиваем выражение на числа, функции и операторы.
    function tokenize(input) {
        input = input
            .replace(/,/g, ".")
            .replace(/π/g, "pi")
            .replace(/√/g, "sqrt");

        const tokens = [];
        let i = 0;

        while (i < input.length) {
            if (/\s/.test(input[i])) {
                i++;
                continue;
            }

            const rest = input.slice(i);

            const number = rest.match(
                /^(?:\d+(?:\.\d*)?|\.\d+)(?:e[+-]?\d+)?/i
            );

            if (number) {
                tokens.push({
                    type: "number",
                    value: Number(number[0])
                });

                i += number[0].length;
                continue;
            }

            const word = rest.match(/^[a-z]+/i);

            if (word) {
                const name = word[0].toLowerCase();

                if (![
                    "sin", "cos", "tg", "tan",
                    "sqrt", "ln", "log", "log10",
                    "exp", "abs", "pi", "e", "ans"
                ].includes(name)) {
                    throw new Error("Неизвестная функция: " + name);
                }

                tokens.push({
                    type: "word",
                    value: name
                });

                i += word[0].length;
                continue;
            }

            if ("+-*/^!%()".includes(input[i])) {
                tokens.push({
                    type: "operator",
                    value: input[i]
                });

                i++;
                continue;
            }

            throw new Error("Недопустимый символ: " + input[i]);
        }

        return tokens;
    }

    function factorial(n) {
        if (!Number.isInteger(n) || n < 0) {
            throw new Error("Факториал определён для целых n ≥ 0");
        }

        if (n > 170) {
            throw new Error("Слишком большое значение факториала");
        }

        let result = 1;

        for (let i = 2; i <= n; i++) {
            result *= i;
        }

        return result;
    }

    // Рекурсивный разбор выражения с учётом приоритета операций.
    function evaluate(input) {
        const tokens = tokenize(input);
        let pos = 0;

        function peek() {
            return tokens[pos];
        }

        function take(value) {
            if (peek() && peek().value === value) {
                pos++;
                return true;
            }

            return false;
        }

        function expression() {
            let value = term();

            while (peek() &&
                   (peek().value === "+" || peek().value === "-")) {
                const op = tokens[pos++].value;
                const right = term();

                value = op === "+" ? value + right : value - right;
            }

            return value;
        }

        function term() {
            let value = unary();

            while (peek() &&
                   (peek().value === "*" || peek().value === "/")) {
                const op = tokens[pos++].value;
                const right = unary();

                if (op === "/" && right === 0) {
                    throw new Error("Деление на ноль");
                }

                value = op === "*" ? value * right : value / right;
            }

            return value;
        }

        function unary() {
            if (take("+")) return unary();
            if (take("-")) return -unary();

            return power();
        }

        function power() {
            let value = postfix();

            if (take("^")) {
                value = Math.pow(value, unary());
            }

            return value;
        }

        function postfix() {
            let value = primary();

            while (peek() &&
                   (peek().value === "!" || peek().value === "%")) {
                const op = tokens[pos++].value;

                if (op === "!") {
                    value = factorial(value);
                } else {
                    value = value / 100;
                }
            }

            return value;
        }

        function primary() {
            const token = peek();

            if (!token) {
                throw new Error("Введите число или выражение");
            }

            if (take("(")) {
                const value = expression();

                if (!take(")")) {
                    throw new Error("Не хватает закрывающей скобки");
                }

                return value;
            }

            if (token.type === "number") {
                pos++;
                return token.value;
            }

            if (token.type === "word") {
                pos++;
                const name = token.value;

                if (name === "pi") return Math.PI;
                if (name === "e") return Math.E;
                if (name === "ans") return lastAnswer;

                if (!take("(")) {
                    throw new Error("После " + name + " поставьте скобку");
                }

                const x = expression();

                if (!take(")")) {
                    throw new Error("Не хватает закрывающей скобки");
                }

                let result;

                switch (name) {
                    case "sin":
                        result = Math.sin(
                            angleMode === "DEG" ? x * Math.PI / 180 : x
                        );
                        break;

                    case "cos":
                        result = Math.cos(
                            angleMode === "DEG" ? x * Math.PI / 180 : x
                        );
                        break;

                    case "tg":
                    case "tan": {
                        const radians =
                            angleMode === "DEG" ? x * Math.PI / 180 : x;

                        if (Math.abs(Math.cos(radians)) < 1e-12) {
                            throw new Error("Тангенс не определён");
                        }

                        result = Math.tan(radians);
                        break;
                    }

                    case "sqrt":
                        if (x < 0) {
                            throw new Error("Корень из отрицательного числа");
                        }
                        result = Math.sqrt(x);
                        break;

                    case "ln":
                        if (x <= 0) {
                            throw new Error("Для ln число должно быть > 0");
                        }
                        result = Math.log(x);
                        break;

                    case "log":
                    case "log10":
                        if (x <= 0) {
                            throw new Error("Для log число должно быть > 0");
                        }
                        result = Math.log10(x);
                        break;

                    case "exp":
                        result = Math.exp(x);
                        break;

                    case "abs":
                        result = Math.abs(x);
                        break;

                    default:
                        throw new Error("Неизвестная функция");
                }

                return result;
            }

            throw new Error("Проверьте выражение");
        }

        if (tokens.length === 0) {
            throw new Error("Введите выражение");
        }

        const result = expression();

        if (pos !== tokens.length) {
            throw new Error("Проверьте расположение операторов и скобок");
        }

        if (!Number.isFinite(result)) {
            throw new Error("Результат выходит за допустимые пределы");
        }

        return result;
    }

    function calculate() {
        try {
            const input = display.value;
            const result = evaluate(input);

            lastAnswer = result;

            // Убираем лишние знаки после запятой.
            const formatted = Number(result.toPrecision(12));

            display.value = String(formatted);
            message.textContent = "";

            history.unshift({
                expression: input,
                result: formatted
            });

            history = history.slice(0, 10);
            renderHistory();

        } catch (error) {
            message.textContent = error.message;
        }
    }

    function renderHistory() {
        historyBox.replaceChildren();

        history.forEach(item => {
            const row = document.createElement("div");
            row.className = "history-item";
            row.textContent = item.expression + " = " + item.result;

            row.addEventListener("click", () => {
                display.value = String(item.result);
                message.textContent = "";
            });

            historyBox.appendChild(row);
        });
    }

    // Управление с клавиатуры.
    display.addEventListener("keydown", function(event) {
        if (event.key === "Enter" || event.key === "=") {
            event.preventDefault();
            calculate();
        }

        if (event.key === "Escape") {
            clearDisplay();
        }
    });
</script>

</body>
</html>
