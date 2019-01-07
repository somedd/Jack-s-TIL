# 2018/01/07

## RxSwift in 4 hours (4,5,6,7/11) by 곰튀김님

- ### 출처

  - [Github링크](https://github.com/iamchiwon/RxSwift_In_4_Hours)
  - [영상링크](https://youtu.be/2uumx7Vzidc)


### 4. 기본 Operator

- **just**
  - Step1에서 `Observable` 을 `Create` 해서 `seal`에다가 ` OnNext`로 데이터를 전달했었는데, 더욱 간단하게 데이터를 직접 받아주는 메서드들 중에 하나가 `just`

- **from**

  - 예제

    ```swift
    Observable.from(["RxSwift", "In", "4", "Hours"])
        .subscribe(onNext: { str in
            print(str)
        })
        .disposed(by: disposeBag)
    /* 
    RxSwift
    In
    4
    Hours
    */ 
    ```

- **map**

  - 바꿔치기

    ```swift
    Observable.from(["with", "곰튀김"]) //stream
        .map { $0.count }
        .subscribe(onNext: { str in
            print(str)
        })
        .disposed(by: disposeBag)
    /* 
    4
    3
    */ 
    ```

- **filter **

### 5. Operator 종류들

- just, from
- map, flatMap
  - **map vs flatMap**
    - map은 데이터를 넣으면 데이터타입이 나오는데, flatMap은 데이터를 넣으면 스트림이 나온다.
- filter
- operators
  - 생성
  - 변환
  - 필터링
  - 결합
  - 오류처리
  - 조건과 불린 연산자
  - 수학과 집계 연산자
  - 역압 연산자
  - 연결
  - Observable 변환
  - [A Decision Tree of Observable Operators](http://reactivex.io/documentation/ko/operators.html)
    - 내가 사용하려는 연산자를 못 찾았을 경우에 사용하면 유용하다. 

### 6. Marble Diagram 이해하기

- 참고 사이트
  - <http://rxmarbles.com/>
  - <http://reactivex.io/documentation/operators.html>
  - <https://itunes.apple.com/us/app/rxmarbles/id1087272442?mt=8>

### 7. Next / Error / Completed

- Step2 소스 수정해가면서, 진행!

- **SubScribe**

  - **그동안 배운 여러가지 Operator들을 사용하고 나서, 그 데이터를 사용하고자 할 때, 즉, 쓰고자 할 때 쓰는 것이 `subScribe` 이다.**

  - `subScribe()` 
    -  받아온 데이터가 내려오고 없어진다. 실행만 시키고, 결과에 신경쓰고 싶지 않을 때, 사용.
      - Ex) Analytics 사용 시, 해당 코드를 비동기로 처리할 경우

  - `.subscribe(on: (Event<Any>) -> Void)` 

    - 가장 기본적인 형태로, 이벤트 타입이 온다.
    - 다른 Operator들은 리턴 값이 스트림이다. 하지만, subscribe는 disposable이다.
    - event 종류
      - `.next`:  데이터 전달.
      - `.error` : 에러가 났을 경우.
      - `.completed` : 해당 스트림이 끝났을 경우.

    ```swift
    Observable.from(["RxSwift", "Hello", 4, "World"])
        .subscribe { (event) in
            switch event {
            case .next(let str): break
            case .error(let err): break
            case .completed: break
            }
        }
        .disposed(by: disposeBag)
    }
    ```

- **자주 쓰는 함수를 활용한 SubScribe 사용 Tip.**

  ```swift
  // 기본 형태
  Observable.from(["RxSwift", "Hello", 4, "World"])
      .subscribe(onNext: { s in
          print(s)
      })
      .disposed(by: disposeBag)
  // 자주 쓰는 함수 Example
  func output(_ s: String) -> Void {
      print(s)
  }
  // 활용
  Observable.from(["RxSwift", "Hello", 4, "World"])
      .subscribe(onNext: output)
      .disposed(by: disposeBag)
  ```
