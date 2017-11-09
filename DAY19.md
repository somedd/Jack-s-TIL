# DAY19
## 20171109
# TIL
## #1. 2차원 배열
  - 배열안에 배열이 들어있는 것으로, 2차원, 3차원까지 주로 사용한다.
  ```javascript
  var arr = [];
  arr.push([1,2,3]);
  arr.push([4,5,6]);
  ```
  - 배열 주소의 의미 : arr[0] = [arr의 주소 + 0번째]를 읽으라는 의미이다.
  - n*m행렬에서 a(ij) = m * i + j로 표현할 수 있다.
  - 2차원 배열의 순회 n * m
  ```javascript
  var arr = [[1,2,3],[4,5,6]];
  for (var i = 0; i < arr.length; i++) {
    for (var j = 0; j < arr[i].length; j++) {
      console.log(arr[i][j]);
    }
  }
  for (var i = 0; i < 6; i++) {
    console.log();
  }
  ```
# My Coding
## 연습문제#1
  - 5 * 10배열에 1부터 50까지 채우세요 루프는 두 개 사용할 것. push사용하지말 것.
  ```javascript
  var arr = [];
  for (var i = 0; i < 5; i++) {
    arr[i] = [];
    for (var j = 0; j < 10; j++) {
      arr[i][j] = i * 10 + (j + 1);
    }
  }
  console.log(arr);
  ```
  - 위 배열을 1차원 행렬로 바꾸기.
  ```javascript
  var arr2 = [];
  for (var i = 0; i < 5; i++) {
    for (var j = 0; j < 10; j++) {
      arr2[i * 10 + j] = arr[i][j];
    }
  }
  console.log("arr2 : " + arr2);
  ```
## 연습문제#2
  - 특정 원소의 주변값 읽기
  - 2차원 배열과 값을 인자로 입력받아서 해당 값이 존재하면, 상하좌우값을 출력하는 함수를 구현!
  - (1) 배열에 값이 있는지 검색, (2) 값이 없으면 리턴 (3) 값이 있다면 위쪽 값 검색 (4)좌,우,하 검색 및 출력
    ```javascript
    var norarr = [];
    var mkNum = function() {
      return Math.floor(Math.random() * 1000 + 1);
    };
    var mkArr = function() {
      var temp = [];
      for (var i = 0; i < 4; i++) {
        temp[i] = [];
        for (var j = 0; j < 4; j++) {
          temp[i][j] = mkNum();
        }
      }
      return temp;
    };
    var findNum = function(val, arr) {
      for (var i = 0; i < 4; i++) {
        for (var j = 0; j < 4; j++) {
          if (val === arr[i][j]) {
            console.log("찾는 값 : " + val + "이 있습니다!");
            if (!!arr[i - 1][j]) { //위
              console.log("찾으려는 원소의 위 값 : " + arr[i - 1][j]);
            }
            if (!!arr[i][j - 1]) { //왼쪽
              console.log("찾으려는 원소의 왼쪽 값 : " + arr[i][j - 1]);
            }
            if (!!arr[i][j + 1]) { //오른쪽
              console.log("찾으려는 원소의 오른쪽 값 : " + arr[i][j + 1]);
            }
            if (!!arr[i + 1][j]) { //아래
              console.log("찾으려는 원소의 아래 값 : " + arr[i + 1][j]);
            }
            return;
          }
        }
      }
      console.log("찾는 값이 없습니다.");
    };
    norarr = mkArr();
    console.log(norarr);
    ```
## 연습문제#3
  - 배열의 스왑 구현하기.
  ```javascript
  var arr = [[1,2,3],[4,5,6]];
  var arraySwap = function(arr, x1, y1, x2, y2) {
    var temp;
    temp = arr[x1][y1];
    arr[x1][y1] = arr[x2][y2];
    arr[x2][y2] = temp;
  };
  arraySwap(arr, 0, 1, 1, 1);
  console.log(arr);
  ```
## 연습문제#4.
  - 2차원 배열의 원소 한 칸 옮기기
    ```javascript
    //position : "left", "right", "up", "down"
    function arrayMove(arr, x1, y1, position) {
      if(position === "left" && y1 > 0) {
        arraySwap(arr, x1, y1, x1, y1 - 1);
        return true;
      } else if(position === "right" && y1 < 3) {
        arraySwap(arr, x1, y1, x1, y1 + 1);
        return true;
      } else if(position === "up" && x1 > 0) {
        arraySwap(arr, x1, y1, x1 - 1, y1);
        return true;
      } else if(position === "down" && x1 < 3) {
        arraySwap(arr, x1, y1, x1 + 1, y1);
        return true;
      } else {
        return false;
      }
    }
    ```
## 연습문제#5.
  - x 주변의 값 찾기 : 4*4배열에 1부터 15까지 숫자와 x가 들어있을 때, x주변의 숫자를 return!
    ```javascript
    ```
## 숫자퍼즐 구현하기.
  1. html + js 만들기
  ```html
  <div id = "puzzle"><span id = "n00"><\span> <span id = "n01"><\span> <\div>
    <div><span id "n10"> <\span> <\div>
  ```
  2. css로 span을 적당히 키워줍니다.
  3. js구현하기
    - div에 버튼 이벤트 리스너 추가
    - 어떤 span이 눌렸는지 체크
    - 움직일 수 있다면, 스왑
    - 반복
  4. 추가 구현
    - 섞기 : 무작위 스왑을 여러번 수행하는 것이 제일 좋다.
    - 움직인 횟수 체크
    - 다 정리했으면 성공! 메세지 출력!
