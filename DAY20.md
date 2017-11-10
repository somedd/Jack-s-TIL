# DAY20
## 20171110
# TIL
## #1. 자료구조 공부해야할 것!
  - list
  - map(딕셔너리, 오브젝트)
  - tree
  - graph

## #2. 배열과 리스트(list)
### 1. ** 배열 VS 리스트 ** (배열과 리스트의 차이는?)
  - 먼저, 배열이나 리스트는 언제 사용할까?
    1. 임의의 원소를 자주 읽을 때 = random access
    2. 만약에 삽입이 빈번하게 일어난다면
      - 배열보다는 링크드 리스트라는 걸 많이 사용한다.
  - 배열
    - 크기가 고정되어 있다.
    - 특정 원소에 접근 복잡도 : O(1) //a[0]
    - 특정 원소의 값을 바꾸기 : O(1) //a[0] = 5;
    - 원소 삽입의 복잡도 : O(n)
      ```javascript
      //n자리에 x값을 넣는다.
      arr.length++;
      for(i = arr.length - 1; i >= n; i--) {
        arr[i] = arr[i - 1];
      }
      ```
    - 배열 메소드
      - init(size)
      - write(idx, value)
      - read(idx)
      - length()
      - addFirst(value)
      - addLast(value)
      - removeFirst() //return first calue
      - removeLast()
      - slice(start, end)
      - 구현해보기
        ```javascript
        var myArray = function(size) {
          this.array = [];
          this.array.length = size;
        };
        myArray.prototype.write = function(idx, value) {
          this.array[idx] = value;
        };
        myArray.prototype.read = function(idx) {
          return this.array[idx];
        };
        myArray.prototype.length = function() {
          return this.array.length;
        };
        myArray.prototype.addFirst = function(value){
          for(var i = this.array.length - 1; i > 0; i--) {
            this.array[i] = this.array[i - 1];
          }
          this.array[0] = value;
        };
        myArray.prototype.addLast = function(value) {
          this.array.length++;
          this.array[this.array.length] = value;
        };

        var arr = new myArray(5);
        arr.addFirst(1);
        arr.addLast(4);
        console.log(arr);
        ```

  - 리스트 : 크기가 가변적이다.(확장/축소 가능)
    - 크기가 가변적이다.(확장& 축소가 가능하다.)
    - 구현하기
      ```javascript
      var Node = function(v) {
        this.value = v;
        this.next = null;
      };
      var head = new Node(1);
      Node.prototype.append = function(v) {
        var n = new Node(v);
        n.next = this.next;
        this.next = n;
      };
      head.append(2);
      console.log(head);
      // head = {v : 1, next : {v : 3, next : null}};
      ```


# My Coding
