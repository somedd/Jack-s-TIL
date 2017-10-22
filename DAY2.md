DAY2
====
2017/10/17
----------
# TIL
## "parseInt"의 두가지 용도
<pre>1. 문자열을 정수로 바꿀 때
2. 소수점을 정수로만 표현할 때</pre>
## 논리 연산자
<pre>&&(AND), ||(OR), !(NOT), ===(equal)</pre>
## MEM구조
<pre> 1. CODE : 실행코드가 들어간다.
 2. DATA : "Hello", 전역변수와 같은 값이 들어가 있음.
 3. HEAP : 객체, 배열이 들어가는 곳. Ex) var a = {1, 2, 3}
 4. STACK : 함수 안에서 만든 변수가 쌓이는 곳.</pre>
## 배열(Array)
<pre> 1. javascript에서만 배열을 객체라고 정의함.
 2. 배열을 string으로 바꾸는 methods : a.join();
 3. 배열은 참조(reference)라서 한번 복사하면 계속 영향을 받는다.</pre>
# My Coding 
## Making a calender
### #1.
<pre><code>console.log("월 화 수 목 금 토 일");
var x;
for (var i = 1; i < 25; i++) {
console.log("%d  %d  %d  %d  %d  %d  %d", i, i+1, i+2, i+3, i+4, i+5, i+6);
    i = i+6;
    if (i === 28) {
      console.log("%d  %d  %d", i+1, i+2, i+3);
    }
  }
</code></pre>
### #2. spring 이용
<pre><code>console.log("  월 화 수 목 금 토 일");
var x = "";
var str = "  ";
  for(var i = 1; i < 32; i++) {
    if (i % 7 === 0) {
      x = x + str + i + "\n"; 
    } else {
      x = x + str + i; 
    }
  }</code></pre>

## 별찍기
### #1.
input : 4

output
~~~~~~
  *
  **
  ***
  ****
~~~~~~
My solution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
var input = parseInt(prompt('몇 줄을 출력하시겠습니까?'));
var str = "";
for (var i = 0; i < input; i++) {
  for (var j = 0; j < input; j++) {
    if (i >= j) {
      str = str + "*";
    } else {
      str = str + " ";
    }
  }
  str = str + "\n";
}
console.log(str);
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
