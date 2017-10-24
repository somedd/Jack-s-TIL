DAY7
====
2017/10/24
----------
# TIL
## #1. JS 파일 읽기와 쓰기 *편집기 사용하기
### block <=> non-block
- block : 어떤 행동에 대해 오래걸리지만 꼭 하는 개념.
- non-block : 어떤 행동에 대해 못하면 못한다고 feedback하는 개념

### 동기(Sync)와 비동기(Async)
1. 동기 : 하나의 이벤트를 다 할 때까지 아무것도 못한다.
   
   *cpu : 빠른 작업이기 때문에 동기로 처리한다.

- Code (text.txt를 읽어서 그대로 출력)
~~~~~~~~~~javascript
var fs = require('fs'); //fs객체를 변수fs에 넣어주세요. fs = file sysyem.
var foo = function(err, data) {
  if (err) {
          console.error("error 발생");
          cosole.error(err);
  } else {
          console.log(data);
  }
};
fs.readFile('test.txt','utf8', foo); //객체인 함수를 매개변수로 사용.
console.log("hahaha"); //javascript는 비동기이기 때문에 hahaha를 먼저 출력한다.
~~~~~~~~~~
2. 비동기 : 하나의 이벤트를 시키고 다른 것도 할 수 있다.

   *javascript는 모두 비동기이다. 즉, 오래걸리는 일은 무조건 비동기로 처리한다.

   *Network(internet), file : 시간이 걸리므로 비동기로 처리한다.

- Code (text.2.txt의 값을 읽어서 값들의 합을 출력)
~~~~~~~~~~~~~javascript
var fs = require('fs');
var data = fs.readFileSync('test2.txt', 'utf8');

var array = [];
array = data.split("\n");
var sum = 0;
for(var i = 0; i < array.length - 1; i++) { //또는 array.pop();을 사용하면 된다.
   sum += parseInt(array[i]);
}
console.log(sum);
~~~~~~~~~~~~~

### spring.split 사용법
~~~~~~~~~javascript
 var a = "1, 2, 3, 4";
 a.split(",");
//결과 : ['1', '2', '3', '4']
~~~~~~~~~
- undefined 또는 NaN을 선별할 경우, !!a를 활용한다. 
  *type을 boolean(true or false)로 바꾸고 싶을 때 사용한다.

## #2. 객체(Object)
