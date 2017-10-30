# DAY11

## 2017/10/30

# TIL

## #0\. 공부해야될 과목들

1. 자료구조
2. 알고리즘
3. 네트워크(HTTP)
4. 데이터베이스(DB)
5. 운영체제(OS)

**공부는 독학사!**

## #1\. 함수(Function)
### 1. 함수란?
  - 입력이 같으면, 출력이 무조건 같아야 한다. Ex)x가 1일 때, y가 두개 나오면 안된다.
  - 반드시 괄호가 있어야 함수 호출이 이루어진다.
### 2. 매개변수가 있는 함수 정의하기
  - 매개변수가 수학적 함수의 X를 담당한다.
  - 연습문제
    ```javascript
    //매개변수 두 개 사용하는 다음 함수를 구현하고 실행해 봅시다.
    var repeat = function(num, text) {
      for(i = 0;i < num;i++) {
        console.log(text);
      }
    };
    repeat(2, "hello");
    ```
### 3. 리턴 값이 있는 함수와 없는 함수
  - return이 없는 함수는 변수에 넣을 경우 **undefined**
  - 연습문제
    ```javascript
    var test1 = function(text) {
      if (text === "exit") {
        return;
      }
      console.log("이게 보여요?");
    };
    test1("hoho");
    test1("exit");
    ```
### 4. call by value와 call by reference
  - call by value : **기본 타입의 경우**, 매개변수에 변수가 아닌 **값** 을 전달한다.
  - call by reference : **나머지 객체의 경우**, 변수의 **참조** 를 전달한다.

### 5. 함수를 언제 만들어야 할까?
  - 줄 수가 지나치게 길어질 경우(10줄 정도)
  - 인덴트가 지나치게 깊어져도 함수로 빼자.
  - 함수는 반드시 한 가지 일만 하도록 하자.

### 6. 함수의 시그니쳐
  - 시그니처 : 함수의 이름, 매개변수, 리턴 타입
### 7. 디폴트(default)
  - 함수 내에서 기본값
## #2. Canvas
## #3. 콜백(Callback) 함수
## #4. 애로우 함수

# My Coding
## #1.연습문제
  1. 배열의 첫번째 원소와 마지막 원소의 순서를 바꾸는 함수를 구현해 봅시다.
  - My solution
      ```javascript
      var changeIdx = function(arr) {
        var temp = arr[0];
        arr[0] = arr[arr.length - 1];
        arr[arr.length - 1] = temp;
        return arr;
      };
      var x = [1, 2, 7, 8, 9];
      changeIdx(x);
      console.log(x);
      ```
  2. 전에 풀었떤 프로그램을 함수를 이용해서 다시 구현해 봅시다.
  3. 구구단을 출력하는 함수를 만들어 봅시다.(default값은 2단)
  - My solution
      ```javascript
    var printkkd = function(num = 2) {
      for(var i = 1; i <= 9; i++) {
        console.log("%d x %d = %d", num, i, num * i);
      }
    };
    printkkd();
    console.log("===========")
    printkkd(5);
    ```
## #2.canvas활용
0. 체스판 만들기
    - My solution
      ```javascript
      for(i = 0; i < 8; i++) {
      if (i % 2 === 0) {
          for(j = 0; j < 8; j = j + 2) {
            ctx.fillStyle = "black"
        ctx.fillRect(80 * j, 60 * i, 80, 60);
      }
        for(j = 1; j <  8;j = j + 2) {
                  ctx.fillStyle = "white"
        ctx.fillRect(80 * j, 60 * i, 80, 60);
        }
      } else {
              for(j = 1; j < 8; j = j + 2) {
       ctx.fillStyle = "white"
        ctx.fillRect(80 * j, 60 * i, 80, 60);
      }
           for(j = 1; j < 8; j = j + 2) {
       ctx.fillStyle = "black"
        ctx.fillRect(80 * j, 60 * i, 80, 60);
      }
      }
      }
      ```
1. 로봇 그리기
    - My solution
      ```javascript
      ctx.strokeStyle = "black";
      ctx.strokeRect(280, 100, 80 , 60)
      ctx.strokeRect(290, 110, 20 , 15)
      ctx.strokeRect(330, 110, 20 , 15)
      ctx.strokeRect(300, 140, 40 , 15)
      ctx.beginPath();
      ctx.moveTo(320, 160);
      ctx.lineTo(320, 260);
      ctx.moveTo(240, 180);
      ctx.lineTo(400, 180);
      ctx.moveTo(320, 260);
      ctx.lineTo(260, 330);
      ctx.moveTo(320, 260);
      ctx.lineTo(380, 330);
      ctx.stroke();
      ```
2. 라이언 그리기
    - My solution
        ```javascript
      var bgImage = new Image();
      bgImage.onload = function () {
        ctx.drawImage(bgImage, 20, 20);
      };
      bgImage.src = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQr3-KMhBbHMcaWYpKdRpcaLSqIsCohg3dSNvsQnhd5-B5cIP2-Dg";
      ctx.beginPath();
      ctx.fillStyle = "GoldenRod"
      ctx.lineWidth = 4;
      ctx.arc(320, 180, 60, 0, 2*Math.PI,false)
      ctx.fill();
      ctx.stroke();
      //얼굴모양

      ctx.beginPath();
      ctx.moveTo(280, 160);
      ctx.lineTo(310, 160);
      ctx.fill();
      ctx.stroke();
      //왼쪽눈썹

      ctx.beginPath();
      ctx.moveTo(330, 160);
      ctx.lineTo(360, 160);
      ctx.fill();
      ctx.stroke();
      //오른쪽눈썹

      ctx.beginPath();
      ctx.moveTo(295,175);
      ctx.arc(295, 175, 2, 0,2*Math.PI,false)
      ctx.fill();
      ctx.stroke();
      //왼쪽 눈

      ctx.beginPath();
      ctx.moveTo(345, 175);
      ctx.arc(345, 175, 2, 0,2*Math.PI,false);
      ctx.fill();
      ctx.stroke();
      //오른쪽 눈

      ctx.beginPath();
      ctx.moveTo(320, 190);
      ctx.arc(320, 190, 2, 0,2*Math.PI,false);
      ctx.fill();
      ctx.stroke();
      //코

      ctx.beginPath();
      ctx.fillStyle = "White"
      ctx.moveTo(310, 190);
      ctx.lineTo(330, 190);
      ctx.fill();
      ctx.stroke();
      //코밑 1자

      ctx.beginPath();
      ctx.moveTo(320, 200);
      ctx.arc(310,200,10,0,3/2*Math.PI,false);
      ctx.fill();
      ctx.stroke();
      //코밑 왼쪽 원

      ctx.beginPath();
      ctx.moveTo(320, 200);
      ctx.arc(330,200,10,Math.PI,3/2*Math.PI,true);
      ctx.fill();
      ctx.stroke();
      //코밑 오른쪽 원

      ctx.beginPath();
      ctx.fillStyle = "GoldenRod";
      ctx.moveTo(365,140);
      ctx.arc(350, 130, 15, Math.PI/5, Math.PI*(8/7),true);
      ctx.fill();
      ctx.stroke();
      //오른쪽 귀

      ctx.beginPath();
      ctx.moveTo(300,127);
      ctx.arc(285, 130, 15, Math.PI*(23/12),Math.PI*(5/7) ,true);
      ctx.fill();
      ctx.stroke();
      //왼쪽 귀

        ```
