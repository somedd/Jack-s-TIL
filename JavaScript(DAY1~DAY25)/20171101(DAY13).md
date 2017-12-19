# DAY13
## 2017/11/01
# My Coding
## Making a calculator
### My Solution
- html

  ```html
  <!DOCTYPE html>
  <html lang = "jack">
  <head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="./cs-style.css">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>
  <body>
    <h1 id = 'h1'>head</h1>
  <p id = 'p'>title</p>
    <div>
      <div id = 'display' class = 'display'>display</div>
      <button id = 'clear' onclick = 'clearNum()'>C</button><br>

      <button id = 'btn7' onclick="pushNum(7)" value = '7'>7</button>
      <button id = 'btn8' onclick="pushNum(8)" value = '8'>8</button>
      <button id = 'btn9' onclick="pushNum(9)" value = '9'>9</button>
      <button id = 'opt1' onclick="pushOpt(1)" value = '+'>+</button><br>

      <button id = 'btn4' onclick="pushNum(4)" value = '4'>4</button>
      <button id = 'btn5' onclick="pushNum(5)" value = '5'>5</button>
      <button id = 'btn6' onclick="pushNum(6)" value = '6'>6</button>
      <button id = 'opt2' onclick="pushOpt(2)" value = '-'>-</button><br>

      <button id = 'btn1' onclick="pushNum(1)" value = '1'>1</button>
      <button id = 'btn2' onclick="pushNum(2)" value = '2'>2</button>
      <button id = 'btn3' onclick="pushNum(3)" value = '3'>3</button>
      <button id = 'opt3' onclick="pushOpt(3)" value = '*'>*</button><br>

      <button id = 'btn0' onclick="pushNum(0)" value = '0'>0</button>
      <button>.</button>
      <button id = 'result' onclick="calNum()">=</button>
      <button id = 'opt4' onclick="pushOpt(4)" value = '/'>/</button>
    </div>
  <script src = "./index.js"></script>
  </body>
  </html>
  ```
- javascript

  ```javascript
  var h = document.getElementById("h1");
  h.innerHTML = "Making a calculator";
  var p = document.getElementById("p");
  p.innerHTML = "Jack's FirstCal";
  var crtNum = '';
  var result = '';
  var dp = document.getElementById("display");
  dp.innerHTML = crtNum;

  function pushNum(num) {
  crtNum = document.getElementById('btn' + num).value;
  dp.innerHTML += crtNum;
  }

  function clearNum() {
  dp.innerHTML = "";
  }

  function pushOpt(num) {
  crtNum = document.getElementById('opt' + num).value;
  dp.innerHTML += crtNum;
  }

  function calNum() {
  result = eval(dp.innerHTML);
  dp.innerHTML = result;
  }
  ```
- css

  ```css
  body {
    background-color: orange;
  }
  p {
    font-family: verdana;
    font-size: 20px;
  }
  h1 {
    color: black;
  }
  button {
    font-family: verdana;
    text-align: center;
    font-size: 40px;
    width : 2em;
    height: 2em;
  }
  .display {
  background-color : gray;
  font-family: orange;
  text-align: right;
  font-size: 40px;
  width : 8.5em;
  height: 1.5em;
  }
  ```
