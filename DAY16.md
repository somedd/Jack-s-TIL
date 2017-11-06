# DAY 16

## 20171106

# TIL

## #1\. 좋은 코딩습관

  ### 1. 불필요한 코드는 지운다.
  ### 2. 좋은 함수를 선언한다. 좋은함수란? 1개의 기능을 구현하는 것.

## #2\. 알고리즘
### 1. 재귀
  - 점화식
    ```javascript
    function diff(n) { //a(n) = a(n-1) + 7의 등차수열을 함수로!(점화식으로)
      if ( n == 0 ) {
        return 1;
      }
      return 7 + diff(n-1);
    }
    ```
  - 다이나믹 프로그래밍(원래 이름 : 메모이제이션) 활용
    - 기존 form
      ```javascript
      var fibo = function(n) {
          if (n == 0) {
            return 0;
          } else if (n == 1) {
            return 1;
          } else {
            return fibo(n - 1) + fibo(n - 2);
          }
      };
      ```
    - 다이나믹 프로그래밍 form
      ```javascript
      var arr = [];
      for (var i = 0; i < 50; i++) {
        arr[i] = 0;
      }
      var fibo = function(n) {
        if (n === 0 || n == 1) {
          arr[n] = 1;
          return 1;
        }
        if (arr[n] !== 0) { //이미 계산을 해 본 경우
          return arr[n];
        }
        arr[n] = fibo(n - 1) + fibo(n - 2); //처음 계산을 하는 경우
        return arr[n];
      };
      for(var i = 0; i < 10; i++) {
          console.log(i, fibo(i), fibo(2));
      }
      ```
# My Coding
## #1. Making a Hangman
  - javascript
    ```javascript
    var canvas = document.getElementById("drawHm");
    var ctx = canvas.getContext("2d");
    var crtStr = [];
    var h = document.getElementById("h1");
    h.innerHTML = "Making a calculator";
    var p = document.getElementById("p");
    p.innerHTML = "Jack's FirstHangman";
    var dp = document.getElementById("display");
    dp.innerHTML = crtStr;
    var count = document.getElementById('life');
    count.innerHTML = 10;
    var dpHint = document.getElementById('hint');
    dpHint.innerHTML = 'Hint : ';
    //hint start
    var hint = [ //[i][0] : hint
      ["country", "korea", "america", "china"],
      ["drink", "coffee", "juice", "water"],
      ["color", "blue", "green", "gray"],
      ["fruit", "apple", "orange", "cherry"],
      ["transportation", "car", "train", "bus"],
      ["sports", "soccer", "basketball", "tennis"]
    ];
    var mkHintNum = function() {
      var chHint = Math.floor(Math.random() * 6);
      return chHint;
    };
    var mkAnswerNum = function() {
      var chAns = Math.floor(Math.random() * 3 + 1);
      return chAns;
    };
    var prtHint = function(str2) {
      dpHint.innerHTML += str2;
    };
    //hint end
    //quiz start
    var mkQuiz = function(num1, num2) {
      var temp = [];
      for (var i = 0; i < (hint[num1][num2]).length; i++) {
        temp.push('_');
      }
      return temp;
    };
    var prtQuiz = function(str1) {
      dp.innerHTML = str1.join(" ");
    };
    var checkAnswer = function(char, num1, num2) {
      var arr = hint[num1][num2].split("");
      var find = false;
      for (var i = 0; i < arr.length; i++) {
        if (arr[i] == char) {
          crtStr[i] = arr[i];
          console.log(crtStr);
          console.log(arr);
          find = true;
        }
      }
      if (find == false) {
        count.innerHTML -= 1;
      }
      return crtStr;
    };
    var pushChar = function(num) {
      if (count.innerHTML >= 1) {
        var x = document.getElementById('btn' + num).value;
        crtStr = checkAnswer(x, hintNum, answerNum);
        dp.innerHTML = crtStr.join(" ");
        drawHm(count.innerHTML);
      }

    };
    //quiz end
    //drawing start
    var drawHm = function(num) {
      if (num == 9) {
        ctx.beginPath();
        ctx.moveTo(50, 180);
        ctx.lineTo(160, 180);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 8) {
        ctx.beginPath();
        ctx.moveTo(75, 180);
        ctx.lineTo(75, 60);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 7) {
        ctx.beginPath();
        ctx.moveTo(75, 60);
        ctx.lineTo(150, 50);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 6) {
        ctx.beginPath();
        ctx.moveTo(150, 50);
        ctx.lineTo(150, 70);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 5) {
        ctx.beginPath();
        ctx.moveTo(165, 85);
        ctx.arc(150, 85, 15, 0, 2 * Math.PI, false);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 4) {
        ctx.beginPath();
        ctx.moveTo(150, 100);
        ctx.lineTo(150, 140);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 3) {
        ctx.beginPath();
        ctx.moveTo(150, 110);
        ctx.lineTo(120, 110);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 2) {
        ctx.beginPath();
        ctx.moveTo(150, 110);
        ctx.lineTo(180, 110);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 1) {
        ctx.beginPath();
        ctx.moveTo(150, 140);
        ctx.lineTo(120, 160);
        ctx.stroke();
        ctx.closePath();
      } else if (num == 0) {
        ctx.beginPath();
        ctx.moveTo(150, 140);
        ctx.lineTo(180, 160);
        ctx.stroke();
        ctx.closePath();
        dpHint.innerHTML = "Game Over!";
      }
    };
    //drawing end
    //main start
    var hintNum = mkHintNum();
    var answerNum = mkAnswerNum();
    crtStr = mkQuiz(hintNum, answerNum);
    prtQuiz(crtStr);
    prtHint(hint[hintNum][0]);
    // main end
    console.log(crtStr);
    console.log("힌트 :", hint[hintNum][0]);
    console.log(hint[hintNum][answerNum]);
    ```
  - html
    ```html
    <!DOCTYPE html>
    <html lang="en">

    <head>
      <meta charset="UTF-8">
      <link rel="stylesheet" href="./mkHangman.css">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Making a hangman.</title>
    </head>

    <body>
      <h1 id='h1'>Making a Hangman game</h1>
      <p id='p'>title</p>
      <div>
        <div id='display' class='display'>display</div>
        <div id='life'> life score </div>
        <div id='hint'> hint </div>
        <canvas id="drawHm" width="200" height="200"></canvas> <br />

        <button id="btn1" onclick="pushChar(1)" value='a' )>a</button>
        <button id="btn2" onclick="pushChar(2)" value='b'>b</button>
        <button id="btn3" onclick="pushChar(3)" value='c'>c</button>
        <button id="btn4" onclick="pushChar(4)" value='d'>d</button>
        <button id="btn5" onclick="pushChar(5)" value='e'>e</button>
        <button id="btn6" onclick="pushChar(6)" value='f'>f</button>
        <button id="btn7" onclick="pushChar(7)" value='g'>g</button> <br/>
        <button id="btn8" onclick="pushChar(8)" value='h'>h</button>
        <button id="btn9" onclick="pushChar(9)" value='i'>i</button>
        <button id="btn10" onclick="pushChar(10)" value='j'>j</button>
        <button id="btn11" onclick="pushChar(11)" value='k'>k</button>
        <button id="btn12" onclick="pushChar(12)" value='l'>l</button>
        <button id="btn13" onclick="pushChar(13)" value='m'>m</button>
        <button id="btn14" onclick="pushChar(14)" value='n'>n</button> <br />
        <button id="btn15" onclick="pushChar(15)" value='o'>o</button>
        <button id="btn16" onclick="pushChar(16)" value='p'>p</button>
        <button id="btn17" onclick="pushChar(17)" value='q'>q</button>
        <button id="btn18" onclick="pushChar(18)" value='r'>r</button>
        <button id="btn19" onclick="pushChar(19)" value='s'>s</button>
        <button id="btn20" onclick="pushChar(20)" value='t'>t</button>
        <button id="btn21" onclick="pushChar(21)" value='u'>u</button> <br />
        <button id="btn22" onclick="pushChar(22)" value='v'>v</button>
        <button id="btn23" onclick="pushChar(23)" value='w'>w</button>
        <button id="btn24" onclick="pushChar(24)" value='x'>x</button>
        <button id="btn25" onclick="pushChar(25)" value='y'>y</button>
        <button id="btn26" onclick="pushChar(26)" value='z'>z</button>
      </div>
      <script src="./mkHangman.js">
      </script>
    </body>

    </html>
    ```
  - css
    ```css
    h1 {
      color : green
    }

    ```
