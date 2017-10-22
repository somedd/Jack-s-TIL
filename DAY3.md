DAY3
====
2017/10/18
----------
# My Coding
## 별찍기(이어서)
### #4.
input : 4

output
~~~~~~~~
   *
  ***
 *****
*******
 *****
  ***
   *
~~~~~~~~
My solution
~~~~~~~~~~~
var input = parseInt(prompt('몇 줄을 출력하시겠습니까?'));
var str = '';
for (var i = 0; i < input; i++) {
  for (var j = (input - 1); j >= 0; j--) {
    if (i >= j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  for (var k = 1; k < input; k++) {
    if (i >= k) {
      str = str + '*';
    }
  }
  str = str + '\n';
}
for (var i = 1; i < input; i++) {
  str = str + ' ';
  for (var j = 1; j < input; j++) {
    if (i <= j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  for (var k = 2; k < input; k++) {
    if (i < k) {
      str = str + '*';
    }
  }
  str = str + '\n';
}
console.log(str);
~~~~~~~~~~~
### #5.
input : 4

output
~~~~~~
****
*  *
*  *
****
~~~~~~
My solution
~~~~~~~~~~~
var input = parseInt(prompt('몇 줄을 출력하시겠습니까?'));
var str = '';
for (var i = 0; i < input; i++) {
  for (var j = (input - 1); j >= 0; j--) {
    if (i == 0 || i == input - 1) {
      str = str + '*';
    } else if (j == 0 || j == input - 1) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  str = str + '\n';
}
console.log(str);
~~~~~~~~~~~
### #6.
input : 4

output
~~~~~~
   *
  * *
 *   *
*     *
 *   *
  * *
   *
~~~~~~
My soluion
~~~~~~~~~~
var input = parseInt(prompt('몇 줄을 출력하시겠습니까?'));
var str = '';
for (var i = 0; i < input; i++) {
  for (var j = (input - 1); j >= 0; j--) {
    if (i == j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  for (var j = 1; j < input; j++) {
    if (i == j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  str = str + '\n';
}
for (var i = 1; i < input; i++) {
  str = str + ' ';
  for (var j = 1; j < input; j++) {
    if (i == j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  for (var j = (input - 2); j > 0; j--) {
    if (i == j) {
      str = str + '*';
    } else {
      str = str + ' ';
    }
  }
  str = str + '\n';
}
console.log(str);
~~~~~~~~~~


