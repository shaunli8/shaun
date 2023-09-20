---
toc: false
comments: false
layout: post
title: Partner Calculator Review
description: My partner's calculator for the calculator review
type: plans
courses: {compsci: {week: 0} }
categories: [C1.4]
---

[Back to Main Home Page](http://0.0.0.0:4200/student/)

<head>
    <title>Calculator with Vanta Fog Animation</title>
    <style type="text/css">
        * {
            margin: 0;
            padding: 0;
        }
        body {
            overflow: hidden;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #fff;
        }
        #vanta-canvas {
            position: absolute;
            width: 30.5%;
            height: 53%;
            z-index: -1;
        }
        .calculator-output {
            grid-column: span 4;
            grid-row: span 1;
            padding: 0.25em;
            font-size: 20px;
            border: 2px solid black;
            display: flex;
            align-items: center;
            background-color: white;
            z-index: 1;
        }

        .calculator-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            max-width: 400px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 10px;
            position: relative;
        }
        .calculator-button {
            padding: 10px;
            font-size: 18px;
            text-align: center;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="vanta-canvas"></div>
    <div class="calculator-container">
        <!-- Calculator display -->
        <div class="calculator-output" id="output">0</div>
        <!-- Calculator buttons -->
        <div class="calculator-button" onclick="clearCalc()">AC</div>
        <div class="calculator-button" onclick="toggleSign()">+/-</div>
        <div class="calculator-button" onclick="percentage()">%</div>
        <div class="calculator-button" onclick="operation('/')">÷</div>
        <div class="calculator-button" onclick="number(7)">7</div>
        <div class="calculator-button" onclick="number(8)">8</div>
        <div class="calculator-button" onclick="number(9)">9</div>
        <div class="calculator-button" onclick="operation('*')">*</div>
        <div class="calculator-button" onclick="number(4)">4</div>
        <div class="calculator-button" onclick="number(5)">5</div>
        <div class="calculator-button" onclick="number(6)">6</div>
        <div class="calculator-button" onclick="operation('-')">-</div>
        <div class="calculator-button" onclick="number(1)">1</div>
        <div class="calculator-button" onclick="number(2)">2</div>
        <div class="calculator-button" onclick="number(3)">3</div>
        <div class="calculator-button" onclick="operation('+')">+</div>
        <div class="calculator-button" onclick="number(0)">0</div>
        <div class="calculator-button" onclick="squareRoot()">√</div>
        <div class="calculator-button" onclick="number('.')">.</div>
        <div class="calculator-button" onclick="equal()">=</div>
    </div>

    <!-- JavaScript (JS) implementation of the calculator. -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vanta@latest/dist/vanta.fog.min.js"></script>
    <script type="text/javascript">
        // Initialize Vanta.Fog
        VANTA.FOG({
            el: "#vanta-canvas",
            mouseControls: true,
            touchControls: true,
            gyroControls: false,
            minHeight: 200.00,
            minWidth: 200.00,
            zoom: 0.80
        });

        // Calculator logic
        var firstNumber = null;
        var operator = null;
        var nextReady = true;
        var output = document.getElementById("output");

        // Function to handle keyboard input
        document.addEventListener("keydown", function (event) {
            const key = event.key;
            if (!isNaN(key) || key === ".") {
                number(key);
            } else if (key === "+" || key === "-" || key === "*" || key === "/") {
                operation(key);
            } else if (key === "Enter") {
                equal();
            } else if (key === "Escape") {
                clearCalc();
            }
        });

        function number(value) {
            // Handle keyboard input for numbers
            if (!isNaN(value) || value === ".") {
                if (nextReady) {
                    output.innerHTML = value;
                    if (value !== "0") {
                        nextReady = false;
                    }
                } else {
                    output.innerHTML += value;
                }
            }
        }

        function operation(choice) {
            // Handle keyboard input for operators
            if (firstNumber === null) {
                firstNumber = parseFloat(output.innerHTML);
                nextReady = true;
                operator = choice;
                return;
            }

            firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
            operator = choice;
            output.innerHTML = firstNumber.toString();
            nextReady = true;
        }

        function calculate(first, second) {
            let result = 0;
            switch (operator) {
                case "+":
                    result = first + second;
                    break;
                case "-":
                    result = first - second;
                    break;
                case "*":
                    result = first * second;
                    break;
                case "/":
                    result = first / second;
                    break;
                default:
                    break;
            }
            return result;
        }

        function equal() {
            firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
            output.innerHTML = firstNumber.toString();
            nextReady = true;
        }

        function clearCalc() {
            firstNumber = null;
            output.innerHTML = "0";
            nextReady = true;
        }

        function toggleSign() {
            output.innerHTML = (parseFloat(output.innerHTML) * -1).toString();
        }

        function percentage() {
            output.innerHTML = (parseFloat(output.innerHTML) / 100).toString();
        }

        function clearInput() {
            output.innerHTML = "0";
        }

        function squareRoot() {
            const currentValue = parseFloat(output.innerHTML);
            if (currentValue >= 0) {
                output.innerHTML = Math.sqrt(currentValue).toString();
        } else {
            // Handle the case where the input is negative (optional)
            output.innerHTML = "Invalid Input";
        }
        nextReady = true;
        }
    </script>
</body>
