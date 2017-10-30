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
