DAY7
====
2017/10/24
----------
# TIL
## #1. JS 파일 읽기와 쓰기 *편집기 사용하기
### 1. block <=> non-block
- block : 어떤 행동에 대해 오래걸리지만 꼭 하는 개념.
- non-block : 어떤 행동에 대해 못하면 못한다고 feedback하는 개념

### 2. 동기(Sync)와 비동기(Async)
- 동기 : 하나의 이벤트를 다 할 때까지 아무것도 못한다.
   
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
- 비동기 : 하나의 이벤트를 시키고 다른 것도 할 수 있다.

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

### 3. spring.split 사용법
~~~~~~~~~javascript
 var a = "1, 2, 3, 4";
 a.split(",");
//결과 : ['1', '2', '3', '4']
~~~~~~~~~
- undefined 또는 NaN을 선별할 경우, !!a를 활용한다. 

  *type을 boolean(true or false)로 바꾸고 싶을 때 사용한다.

## #2. 객체(Object)
### 1. 객체란 무엇인가?
- 객체는 DATA를 잘 관리하기 위해서 사용한다.
- javascript안에서 배열은 열로 관리하기 때문에 힘들다. 그래서 객체를 사용한다.
- 상태(속성)와 행동(메소드)을 가진다.
### 2. 객체지향프로그래밍의 특징
- 유지보수가 쉬워진다.
- 대형 프로그램을 짜기 쉬워진다.
- 객체와 객체가 협력해서 일을 한다.
- 객체는 일에 대한 책임을 진다. : 메소드에 대한 책임을 지는 것.
- 객체는 객체에 메세지를 보낸다. : 메소드를 통해서 다른 객체에 일을 시킴.
- 객체는 자율적으로 일을 한다.
  *메세지를 통해 들어온 이벤트를 하느냐 마느냐는 받은 객체가 결정하는 것이다.
### 3. 객체 만들기
~~~~~~~~~javascript
var m1 = {       //m1이라는 객체
  name: "Honux", //'이름'이라는 상태
  hp: 100,       //'체력'이라는 상태
  mp: 50,        //'마나'라는 상태
  power: 10,     //'힘'이라는 상태
  attack: function(target) { //'공격'이라는 행동(메소드)
    target.hp -= this.power; //this = 나라는 뜻이다. (내 객체)
  }
};
~~~~~~~~~
#### this 키워드
- 함수 또는 메소드 안에서 사용시 주로 함수를 소유한 객체
- 객체 안에서 사용시 객체 자체를 가르킨다.

  *this의 값을 바꿀 수 없다. Ex) this = m2; : 안되는 것임.

### 4. 기본 생성자들
~~~~~~~~~~javascript
var a = new String(); // a = "";
var b = new Object(); // b = {};
var c = new Array(); // c = [];
~~~~~~~~~~
- 생성자를 이용해 생성된 객체는 prototype이라고 하는 속성을 갖는다.
- 속성을 prototype으로 구현하면 의미가 이상해진다. 사용하지 않는게 좋다.
- Ex) m1이라는 객체의 attack, show, eat을 prototype으로 구현한다면?
~~~~~~~~~~~~~javascript
Human.prototype.attack = function(target) {
target.hp -= this.power
    };
Human.prototype.show = function () {
    console.log('%s의 상태입니다. Hp : %d / MP :  %d / Power : %d', this.name, this.hp, this.mp, this.power);
    };
Human.prototype.eat = function (target) {
    this.hp += target.energy;
    console.log("%s이 %s를 먹었습니다.",this.name,  target.name);
    };
~~~~~~~~~~~~~
### 5. 객체 멤버에 접근하는 방법
- a.name = a["name"] : 서로 같은 의미이다.
- object.keys(a); : 해당 객체의 모든 key값을 볼 수 있다.

### 6. 배열과 객체
- 객체 안에 속성값이 배열이 될 수 있다.
  
  *생성자 선언 후, 배열 생성하고 push로 구현

### 7. 객체와 참조
- 객체도 마찬가지로 참조 변수에 할당된다.

# My Coding
## 연습문제#1.  같은 객체 타입 2개 구현하기.
- My solution
~~~~~~~~~~javascript
var m1 = {
  name : "Honux",
  hp : 100,
  mp : 50,
  power : 10,
  attack : function(target) {
  target.hp -= this.power;
  },
  eat : function(target) {
    this.hp += target.energy;
  }
}
var m2 = {
  name : "Jack",
  hp : 200,
  mp : 10,
  power : 5,
  attack : function(target) {
  target.hp -= this.power;
  },
  eat : function(target) {
    this.hp += target.energy;
  }
}
~~~~~~~~~~
## 연습문제#2.
1. food(name, energy) 생성자를 만들어 봅시다.
2. eat()메소드를 human에 추가해 봅시다.
3. 커피와 도너츠 객체를 생성해서 크롱에게 먹여봅시다.
- My solution
~~~~~~~~~~~~~javascript
function Food(name, energy) {      //#2-1.
  this.name = name;
  this.energy = energy;
};
function Human(name, hp, mp, power) {
  this.name = name;
  this.hp = hp;
  this.mp = mp;
  this.power = power;
  this.attack = function (target) {
    target.hp -= this.power;
  };
  this.show = function () {
    console.log('%s의 상태입니다. Hp : %d / MP :  %d / Power : %d', this.name, this.hp, this.mp, this.power);
  };
  this.eat = function (target) {   //#2-2.
    this.hp += target.energy;
    console.log("%s이 %s를 먹었습니다.",this.name,  target.name);
  };
};
var h1 = new Human("honux", 100, 20, 10);
var h2 = new Human("crong", 999, 1, 99);
var f1 = new Food("coffee", 10);
var f2 = new Food("doughnut", 20);

h2.eat(f1);                        //#2-3.
h2.show();
h2.eat(f2);
h2.show();
~~~~~~~~~~~~~
## 연습문제#3. h1 객체의 모든 속성과 값을 출력해봅시다.
~~~~~~~~~~~~~~~javascript
function Human(name, hp, mp, power) {
  this.name = name;
  this.hp = hp;
  this.mp = mp;
  this.power = power;
  };
function Food(name, energy) {
  this.name = name;
  this.energy = energy;
};
Human.prototype.eat = function (target) {
    this.hp += target.energy;
    };
var h1 = new Human("jack", 100, 100, 10);
var f1 = new Food("coffee", 100);
h1.eat(f1);
var keys = Object.keys(h1);
for (var i = 0; i < keys.length; i++) {
  var key = keys[i];
  console.log(key + " : " + h1[key]);
}
~~~~~~~~~~~~~~~

## 연습문제#4.
1. 배열을 만들고 1-100까지의 임의의 정수를 20개 넣습니다.
2. 배열에서 최대값과 최소값을 뽑는 함수 myMin(), myMax() 구현
3. 배열의 주어진 위치의 원소를 교체하는 mySwap(); 구현
4. 이 배열을 정렬합니다.
5. array.sort();를 사용해서 오름차순 내림차순 정렬
6. 2진 검색을 구현
- My solution
~~~~~~~~~~~~~~~~~javascript
var generateNum = function () {                   //#4-1. 난수생성
  return Math.floor(Math.random() * 100 + 1);
};
var myMin = function (arr) {                      //#4-2. 최소값, 최대값 구하는 함수
  var min = arr[0];
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] < min) {
      min = arr[i];
    }
  }
  return min;
};
var myMax = function (arr) {
  var max = arr[0];
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}
var mySwap = function (arr, idx1, idx2) {         //#4-3. 위치바꾸는 함수
  var temp;
  temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
  return arr;
};순
var mySort = function (arr) {                     //#4-4. 오름차순으로 정렬하는 함수(버블정렬)
  var tempArr = 0;
  var n = arr.length;
  for (var j = 0; j < n; j++) {
    for (var i = n; i >= 0; i--) {
      if (arr[i] > arr[i + 1]) {
        mySwap(arr, i, i + 1);
      }
    }
  }
  return arr;
};
/*mainArr.sort(function(a, b){                    //#4-5. *return a -b;는 오름차
  return b - a;
});*/
var myBinarySearch = function (arr, num) {        //#4-5. 2진탐색하는 함수
  var low = 0;
  var high = arr.length - 1;
  for (i = 0; i < arr.length; i++) {
    var mid = (low + high) / 2;
    var temp = arr[mid];
    if (temp == num) {
      return mid;
    } else if (temp > num) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return 0;
};
var mainArr = [];
for (var i = 0; i < 20; i++) {
  var a = generateNum();
  mainArr[i] = a;
}
mainArr = mySort(mainArr);
var num = prompt('찾고자 하는 숫자를 입력하세요.');
if (myBinarySearch(mainArr, num) == 0) {
  console.log(mainArr);
  console.log('찾고자 하는 숫자가 없습니다.');
} else {
  console.log(mainArr);
  console.log('찾고자 하는 숫자가 %d번째에 있습니다.', myBinarySearch(mainArr, num))
}
~~~~~~~~~~~~~~~~~
