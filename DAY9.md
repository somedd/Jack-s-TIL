# DAY9

## 2017/10/26

# TIL

## #1\. 객체 첨자 (javascript에서 h.x와 h[x]의 차이는?)

- 객체를 배열처럼 처리하는 이유

  ```javascript
  var h = { name : "해나", status : "잠못잠", money : 9999999};
  h.money -= 5000;
  var x = prompt("어떤 속성을 바꿀래요?");
  var y = prompt("어떤 값으로 바꿀래요?");
  console.log(x, y);
  h.x = y;
  console.log(h);
  //결과는 x라는 key가 추가가 된다.
  //따라서, h[x] = y로 표기로 해야된다. (h[x] = h["money"])도 같은 의미.
  //값으로 속성을 접근하고 싶을 때 사용한다.
  ```

## #2\. for...in

- 객체를 사용한다.
- 배열로 사용하면 idx로 처리되기 때문에 사용하면 안된다.

  ```javascript
  var h = { name : "해나", status : "잠못잠", money : 9999999, age : 23, pc : 5, pet : ['에비츄', '스누피', '가필드'],
            work : function(money) {
              this.money += money;
            }};
  for (var x in h) {
  console.log(X);
  }
  ```

## #3\. 조건문과 반복문

### 1\. while 반복문

```javascript
while(조건) {
  console.log("참일때 실행됨");
}
```

### 2\. break

- break를 만나면 해당하는 하나의 반복문을 벗어난다.

  ### 3\. continue

- continue를 만나면 반복문의 처음으로 돌아간다.

- for(1 ; 2 ; 3)문에서 만나면, 3으로 간다.

  ```javascript
  console.log("start");
  for (var i = 0; i < 5; i++) { //i가 3이면 i++로 간다.
  console.log("1 %d", i);
  if (i >= 3) {
    continue;
  }
  console.log("2 %d", i);
  }
  console.log("end")
  ```

  ### 2\. while과 for문

- 아래의 두 소스는 똑같은 것임.
  ```javascript
  var i = 0; //(1)
  while (i <= 100) { //(2)
  console.log(i); //(3)
  i++; //(4)
  }
  ```
  ```javascript
  for (var i = 0; i <= 100; i++) {
   console.log(i);
  }
  ```

  ## #4\. html

# My Coding

## #1\. for in

1. 객체 h의 키와 값을 출력해보자.
2. 객체 h의 숫자 객체의 합을 출력해 보자.

- 객체 h

  ```javascript
  var h = {
  name: "해나",
  status: "잠못잠",
  money: 9999999,
  age: 23,
  pc: 5,
  pet: ['에비츄', '스누피', '가필드'],
  work: function(money) {
    this.money += money;
  }
  };
  ```

- 1-1\. My solution

  ```javascript
  for (var key in h) {
  console.log("%s :  %s", key, h[key]);
  }
  ```

- 1-2\. My solution

  ```javascript
  var sum = 0;
  for (var key in h) {
  if (typeof(h[key]) === 'number') {
    sum += h[key];
  }
  }
  console.log(sum);
  ```
