DAY4
====
2017/10/19
# TIL
## 자료형과 변수
### 실행환경
~~
1. 인터프리터 : 코드를 한줄씩 즉각적으로 실행시킬 수 있는 것.
2. 컴파일러 : 프로그래밍 언어의 한 소스를 통채로 실행시키는 프로그램을 만들어주는 것.
~~
### immutable & mutable
-immutable : 값을 바꿀 수 없음. -> string
-mutable : 값을 바꿀 수 있음. -> string을 제외한 모든 자료형
### Coding Tip
1. 숫자는 한글자당 4byte, 문자는 한글자당 1byte
2. 논리연산자 xor : 둘이 다를 때만 true
3. const a = 3.14; : 상수만들기

# My Coding
## 연습문제
### #1. BMI를 계산하는 프로그램 구현하기.
My solution

  *1. 일반
~~~~~~~~~javascript
var weight = parseInt(prompt("체중(kg)을 입력하세요."));
var height = (0.01) * parseInt(prompt("신장(cm)을 입력하세요."));
var bmi = weight / height / height;
bmi = bmi.toFixed(2);
~~~~~~~~~
  *2. 함수활용
~~~~~~~~~javascript
var shorten = function(num) {
    return Math.round(num * 100) / 100;
}
if (bmi < 20) {
   alert("당신은 저체중입니다. BMI지수 : " + bmi);
} else if (20 <= bmi && bmi < 25 ) {
    alert("당신은 정상체중입니다. BMI지수 : " + bmi);
} else if (25 <= bmi && bmi < 30) {
    alert("당신은 과체중입니다. BMI지수 : " + bmi);
} else if (30 <= bmi && bmi < 35) {
    alert("당신은 비만입니다. BMI지수 : " + bmi);
} else {
    alert("당신은 고도비만입니다. BMI지수 : " + bmi);
}
~~~~~~~~~
### #2. 섭씨를 입력받아 화씨로 출력하는 프로그램 구현하기.
My solution
~~~~~~~~~javascript
var c = parseInt(prompt("섭씨온도를 입력하세요."));
var f = (c * (9/5) + 32);
alert("화씨 온도 : " + f);
~~~~~~~~~
