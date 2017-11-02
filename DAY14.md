# DAY14

## 2017/11/02

# TIL

## #1\. 변수의 스코프(Scope).

  ### 1\. 스코프(scope)란?

  - **변수의 유효범위!**

  ### 2\. 변수(variables)

  - 전역변수(global variables)
  - 지역변수(local variables) = 매개변수(parameter)
  - 자동 전역 변수 : 'var'가 없이 선언한 변수는 자동으로 전역변수가 된다. **절대 쓰지 말 것!**
  - "use strict" 에서는 깐깐해짐. 자동전역 변수를 사용할 수 없다.
  - for문 안에서 사용된 변수는 전역변수로 사용되는데, javascript만 그렇다!
  - const로 선언했을 경우, 값을 바꿀 수 없음.
  - let은 실수로 두번 선언하는 것을 막아줌. 또한 block scope로 그 블록 안에서만 유요하다!

  ### 3\. 클로져(closure)란 ?
  - **내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것**
  - Ex)
    ```javascript
    var outer = function() {
      var i = 10;
      var inner = function() { //inner함수 안에서 그 밖에 있는 변수 i를 사용함.
        console.log(i);
      }
      inner();
    };
    outer();
    ```
  - **호이스팅** : 변수가 있는지는 모르지만 존재가 있다는 것을 아는 것.
    - Ex)
      ```javascript
      console.log(a);
      var a = 10;
      console.log(a);
      //undefined
      //10
      ```

## #2\. 재귀(recursion)
  ### 1. 재귀(recursion)란?
  - 함수가 함수 안에서 자신을 다시 호출하는 것!
  - 재귀는 무조건 종료시점이 필요하다. 즉, **반드시 종료조건이 포함되어야 한다.**
  - Ex)
    ```javascript
    var countDown2 = function(n) {
      console.log(n);
      if (n < 1) { //종료조건
        return;
      }
      countDown2(n - 1);
    };
    countDown2(10);
    ```
  - 점화식 : 재귀나 다이나믹 프로그래밍으로 문제를 풀 때, 유용하게 사용할 수 있다.
  - **도전과제 : 재귀로 하노이 타워를 애니메이션까지 구현해 봅시다.**

## #3\. 애니메이션(animation)
  ### 1. setInterval(function, time), clearinterval(tid);
  ### 2. 공튕기기 구현하기.
  
# My Coding
  ## #1. 재귀 연습문제
  ### #1-1. a부터 b까지 정수를 더해서 리턴해주는 재귀함수를 구현하기.
  - My solution
    ```javascript
    var rsum = function(a, b) {
      if (a == b) {
          return a;
      }
      return b + rsum(a, b - 1);
    };
    var x = rsum(1, 10);
    console.log(x);
    ```
  ### #1-2. 팩토리얼을 재귀함수로 구현하기.
  - My solution ver1.
    ```javascript
    var fact = function(n) {
      if (n == 1) {
        return 1;
      }
      return n * fact(n - 1);
    };
    console.log(fact(3));
    ```
  - My solution ver2.
    ```javascript
    var str = "";
    var fact = function(n) {
    if (n == 1) {
       str += 1;
       return 1;
    }
    str += n + " * ";
    console.log(str);
    return n * fact(n - 1);
    };
    var x = fact(5);
    console.log("%s = %d", str, x);
    ```
  ### #1-3. 피보나치 수열을 재귀함수로 구현하기.
  - My solution
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
    console.log(fibo(6));
    ```
