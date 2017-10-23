DAY3
====
2017/10/23
----------
# TIL
## 배열과문자열
### 길이를 알 수 없는 배열의 마지막 원소를 읽어오려면?
~~~~
a[a.length - 1]
~~~~
### 문자열과 배열
~~~~~~~~~~~~~~~~
1. 문자열과 배열은 비슷하다. But, 문자열 : immutable, 배열 : mutable
   *배열에는 +가 없다.
2. push(제일 끝에 원소를 넣는 것.) <=> pop(제일 끝의 원소를 빼는 것.)
3. a.join();
   *a.join(""); : 1234, a.join("-"); : 1-2-3-4
4. javascript에서 한 배열 안에 다양한 Type사용이 가능하지만 비추천.
5. shift(맨 앞 원소를 없애는 것) <=> unshift(맨 앞에 원소를 추가하는 것.)
6. indexOF (Index를 0부터 탐색한다.) <=> lastIndexOF (index를 뒤에서부터탐색한다.);
   *값이 없으면 -1을 출력한다.
   *문자열도 사용가능
7. slice(1, 4) : 배열 내 1 <= index < 4의 값을 return.
   *기존값은 바뀌지 않는다.
   *문자열도 사용가능
8. splice(2, 3) : 배열의 index 2부터 3개를 잘라내고 해당 값을 배열로  return.
   *기존 값은 잘리고 난뒤 바뀐다.
   *문자열은 바꾸는게 안되니 불가능
9. 2차원 배열 : 배열에다가 배열을 push한 것.
10. foreach(), map(), reduce() *중요
11. concat(); : 배열 합치기. Ex) [1, 2].concat([3, 4, 5]);
~~~~~~~~~~~~~~~~
### Coding Tip
~~~~~~~~~~~~~~~~
arguments(parameter, 매개변수, 인자, 인수)는 건드리지 말자!
~~~~~~~~~~~~~~~~
# My Coding
## 연습문제
### #1. 배열의 마지막에 원소를 추가하는 함수append(array, data) 구현하기.
*function 이용
~~~~~~~~~~~~~~~javascript
var append = function(array, data) {
  array[array.length] = data;
}
var arr1 = [1, 2, 3];
append(arr1, 4);
console.log(arr1);
~~~~~~~~~~~~~~~
*배열의 method로 만들기
~~~~~~~~~~~~~~javascript
var a = [1, 2, 3];
Array.prototype.append = function(data) {
  this[this.length] = data;
}
a.append(4);
~~~~~~~~~~~~~~
### #2. pop(); 구현하기.
arr.length를 하나 줄여서 구현
### #3. shift();, unshift(); 구현하기.
  #3-1. shift();
~~~~~~~~~~~~~~~~javascript
var myShift = function(array) {
  for(i = 0; i < array.length - 1; i++) {
     array[i] = array[i + 1];
  }
   array.length--;
}
var arr1 = [1, 2, 3, 4, 5];
myShift(arr1);
console.log(arr1);
~~~~~~~~~~~~~~~~
  #3-2. unshift();

*1. i--;
~~~~~~~~~~~~~~~~~~~~javascript
var myUnshift = function(array, data) {
  for(i = array.length - 1; i >= 0; i--) {
     array[i + 1] = array[i];
  i = 0;
  array[i] = data;
}
var arr1 = [1, 2, 3, 4, 5];
myUnshift(arr1, 7);
console.log(arr1);
~~~~~~~~~~~~~~~~~~~~
*2. i++;
~~~~~~~~~~~~~~~~~~~~javascript
var myUnshift = function(array, data) {
  for(i = 0; i < array.length; i++) {
     array[array.length - i] = array[(array.length - i) - 1];
  }
  i = 0;
  array[i] = data;
}
var arr1 = [1, 2, 3, 4, 5];
myUnshift(arr1, 7);
console.log(arr1);
~~~~~~~~~~~~~~~~~~~~
*3. temp 이용
~~~~~~~~~~~~~~~~~~~~javascript
var myUnshift = function(arr, v) {
var temp = [];
for(i = 0; i < arr.length; i++) {
temp[i] = arr[i];
}
v = arr.length;
for(i = 0; i < n; i++) {
arr[i +  1] = temp[i];
}
arr[0] = v;
}
~~~~~~~~~~~~~~~~~~~~
### #4. 무작위 짝코딩 멤버를 추천해 주는 프로그램을 짜보자. 홀수일 경우는 어떻게 해야할지도 생각해 보자.
~~~~~~~~~~~~~~~~~~~javascript
var mkNum = function (input) {
  var x = Math.random();
  x = x * input
  x = x - x % 1;
  return x;
};
var inputName = function (arr, v) {
  for (var i = 0; i < v; i++) {
    var name = prompt((i + 1) + '번째 멤버의 이름을 입력하세요.');
    arr.push(name);
  }
}
var mkPartner = function (arr1, arr2, v) {
  for (i = v; i > 0; i--) {
    var x = mkNum(i);
    arr1.push(arr2[x]);
    arr2.splice(x, 1);
  }
};
var printPartner = function (arr, v) {
  console.log('*짝코딩 멤버입니다.*');
  for (i = 0; i < v; i = i + 2) {
    console.log('- %s와 %s는 짝입니다.', arr[i], arr[i + 1]);
  }
}
var num = parseInt(prompt('총 몇 명인지 입력하세요.'));
var member = [];
inputName(member, num);
var final = [];
if (num % 2 == 0) {
  mkPartner(final, member, num);
  printPartner(final, num);
} else {
  var y = mkNum(num);
  var solo = [];
  solo.push(member[y]);
  member.splice(y, 1);
  num = num - 1;
  mkPartner(final, member, num);
  printPartner(final, num);
  console.log('- %s는 혼자서 해야됩니다.', solo[0]);
}
~~~~~~~~~~~~~~~~~~~

