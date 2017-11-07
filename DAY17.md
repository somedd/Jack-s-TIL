# DAY17
## 20171107
# TIL
## 알고리즘 기초
### 1. 정렬(Sorting)이란?
  - 무작위로 나열된 배열이나 리스트의 원소를 순서대로 재배치하는 알고리즘
  - **시험에도 많이 나오고, 면접에도 잘 나오고, 실제로도 많이 쓰기 때문에 중요!**
  ####1-1. 라이브러리 함수.
  - 일반적으로 각 언어에는 정렬함수가 제공이 된다.
  - 하지만, 정렬할 수 있는 대상&기준이 필요하다. 그거를 활용해야됨.
  - 연습문제
### 2. 객체 정렬
### 2.5 안정 정렬
### 3. 선택 정렬
  - 배열에서 남은수 중 가장 작은 수를 앞부터 채워 준다.
### 4. 버블 정렬
### 5. 삽입 정렬
# My Coding
## 연습문제
### #1. 정렬(오름차순, 내림차순 등)
- 1.숫자 5개 정렬
  ```javascript
  var num = [5, 2, 3, 4, 1];
  num.sort(function(a, b) { return a - b; }); //오름차순
  console.log(num);
  num.sort(function(a, b) { return b - a;}); //내림차순
  console.log(num);
  ```
- 2.단어 5개 정렬
  ```javascript
  var char = ['a', 'c', 'e', 'i', 'd'];
  char.sort();
  console.log(char);
  ```
- 3.사람 객체(name, money) 5개를 만들어서 이름과 재산순으로 각각 정렬해 봅시다.
  ```javascript
  var apj = [
    {name : 'jack', money : 5000},
    {name : 'koo', money : 1000},
    {name : 'honux', money : 10000},
    {name : 'will', money : 4000},
    {name : 'ryan', money : 3000}
  ];
  console.log("객체 재산순");
  apj.sort(function(a, b) { return a.money - b.money;});
  console.log(apj);
  console.log("객체 이름순");
  apj.sort(function(a, b) {
    if (a.name > b.name) {
      return 1;
    } else if (a.name === b.name) {
      return 0;
    } else {
      return -1;
    }
  });
  console.log(apj);
  ```
### #2. 셔플(Shuffle)함수 구현.
  - solution
    ```javascript
    //honux shuffle
    Array.prototype.shuffle = function() {
    	for(var i = 0; i < this.length * 5; i++) {
    		var idx1 = Math.floor(Math.random() * this.length);
    		var idx2 = Math.floor(Math.random() * this.length);
    		var temp = this[idx1];
    		this[idx1] = this[idx2];
    		this[idx2] = temp;
    	}
    };

    //Will shuffle
    Array.prototype.shuffle3 = function() {
    	var x;
    	for(var i = 0; i < this.length * 5; i++) {
    		var idx = Math.floor(Math.random() * this.length);
    		[x] = this.splice(idx, 1);
    		this.push(x);
    	}
    };

    //knuth shuffle
    Array.prototype.shuffle2 = function() {
    	for(var i = this.length - 1; i >= 0; i--) {
    		var idx1 = Math.floor(Math.random() * i);
    		var temp = this[idx1];
    		this[idx1] = this[i];
    		this[i] = temp;
    	}
    }

    var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    arr.shuffle();
    console.log(arr);
    arr.shuffle2();
    console.log(arr);
    arr.shuffle3();
    console.log(arr);
    ```
### #3. 선택정렬
  - solution
    ```javascript
    function selectionSort(arr) {
      for (var i = 0; i < arr.length - 1; i++) {
        var min = arr[i];
        var pos = i;
        for(var j = i + 1; j < arr.length; j++) {
          if (arr[j] < min) {
            min = arr[j];
            pos = j;
          }
        }
        arr[pos] = arr[i];
        arr[i] = min;
      }
    }

    selectionSort(arr);
    console.log(arr);
    ```
