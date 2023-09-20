---
toc: false
comments: false
layout: post
title: My Calculator
description: A test calculator. Changed button sizes and fonts. 9/20 - Changed the color of the buttons, added a hover button color change, changed the calculator layout into a table,  added some scientific calculator buttons (trig, exponents, sqrt, logs)
type: plans
courses: {compsci: {week: 0} }
categories: [C1.4]
---

[Back to Main Home Page](http://0.0.0.0:4200/student/)

<html>
<head>
<style>
/* Style for the calculator buttons */
.button {
  padding: 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 2px;
  cursor: pointer;
  border-radius: 5px;
  width: 50px;
  transition: background-color 0.2s, transform 0.1s;
}

/* Black number buttons */
.number-button {
  background-color: black;
  border: none;
  color: white;
}

/* Arithmetic operation buttons in green */
.operation-button {
  background-color: #27ae60;
  border: none;
  color: white;
}

/* Other buttons in red */
.other-button {
  background-color: #e74c3c;
  border: none;
  color: white;
}

/* Hover effect */
.button:hover {
  background-color: #2980b9;
}

/* Click effect */
.button:active {
  background-color: #1f6da6;
  transform: scale(0.95);
}

/* Style for the calculator table */
table {
  border-collapse: collapse;
  margin: 0 auto;
}

/* Style for the calculator display */
#display {
  width: 200px;
  font-size: 20px;
  padding: 10px;
}
</style>
</head>
<body>

<!-- Calculator display -->
<input type="text" id="display" readonly><br>

<!-- Calculator buttons -->
<table>
  <tr>
    <td><button class="button number-button" onclick="appendToDisplay('7')">7</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('8')">8</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('9')">9</button></td>
    <td><button class="button operation-button" onclick="appendToDisplay('+')">+</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('sqrt(')">√</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('**')">^</button></td>
  </tr>
  <tr>
    <td><button class="button number-button" onclick="appendToDisplay('4')">4</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('5')">5</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('6')">6</button></td>
    <td><button class="button operation-button" onclick="appendToDisplay('-')">-</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('sin(')">sin</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('cos(')">cos</button></td>
  </tr>
  <tr>
    <td><button class="button number-button" onclick="appendToDisplay('1')">1</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('2')">2</button></td>
    <td><button class="button number-button" onclick="appendToDisplay('3')">3</button></td>
    <td><button class="button operation-button" onclick="appendToDisplay('*')">*</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('tan(')">tan</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('log(')">log</button></td>
  </tr>
  <tr>
    <td><button class="button number-button" onclick="appendToDisplay('0')">0</button></td>
    <td><button class="button other-button" onclick="clearDisplay()">C</button></td>
    <td><button class="button other-button" onclick="calculate()">=</button></td>
    <td><button class="button operation-button" onclick="appendToDisplay('/')">/</button></td>
    <td><button class="button other-button" onclick="appendToDisplay('('">(</button></td>
    <td><button class="button other-button" onclick="appendToDisplay(')')">)</button></td>
  </tr>
</table>

<script>
// Function to append clicked button value to the display
function appendToDisplay(value) {
  document.getElementById('display').value += value;
}

// Function to clear the display
function clearDisplay() {
  document.getElementById('display').value = '';
}

// Function to calculate the result
function calculate() {
  try {
    const result = eval(document.getElementById('display').value);
    document.getElementById('display').value = result;
  } catch (error) {
    document.getElementById('display').value = 'Error';
  }
}
</script>

</body>
</html>
