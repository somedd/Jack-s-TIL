# 2018/01/16

## RxSwift in 4 hours (9,10,11/11) by 곰튀김님

- ### 출처

  - [Github링크](https://github.com/iamchiwon/RxSwift_In_4_Hours)
  - [영상링크](https://youtu.be/2uumx7Vzidc)

### 9. RxSwift 응용해보기

- Step3  소스 수정해가면서, 진행!

  - 1단계: 기본 구현

    ```swift
    idField.rx.text.orEmpty
        .map(checkEmailValid)
        .subscribe(onNext: { isValidID in
            self.idValidView.isHidden = isValidID
        })
        .disposed(by: disposeBag)
    
    pwField.rx.text.orEmpty
        .map(checkPasswordValid)
        .subscribe(onNext: { isValidPW in
            self.pwValidView.isHidden = isValidPW
        })
        .disposed(by: disposeBag)
    
    Observable.combineLatest(
        idField.rx.text.orEmpty.map(checkEmailValid),
        pwField.rx.text.orEmpty.map(checkPasswordValid),
        resultSelector: { isValidID, isValidPW in isValidID && isValidPW })
        .subscribe(onNext: { b in
            self.loginButton.isEnabled = b
        })
        .disposed(by: disposeBag)
    ```

  - 2단계: input과 output으로 나누기

    - Input: ID, PW 입력

      ```swift
      let idInputObservable = idField.rx.text.orEmpty.asObservable()
      let idValidObservable = idInputObservable.map(checkEmailValid)
      
      let pwInputObservable = pwField.rx.text.orEmpty.asObservable()
      let pwValidObservable = pwInputObservable.map(checkPasswordValid)
      ```

    - output: Bullet(화면 내 각 validVIew), 로그인 버튼 Enable

      ```swift
      idValidObservable.subscribe(onNext: { isValidEmail in
           self.idValidView.isHidden = isValidEmail })
          .disposed(by: disposeBag)
      
      pwValidObservable.subscribe(onNext: { isValidPW in
      	self.idValidView.isHidden = isValidPW })
          .disposed(by: disposeBag)
      
      Observable.combineLatest(
          idValidObservable,
          pwValidObservable, 
      	resultSelector: { $0 && $1 })
          .subscribe(onNext: { b in
              self.loginButton.isEnabled = b
          })
          .disposed(by: disposeBag)
      ```

### 10. Subject

- 3단계: Subject 활용하기

  - input: *ID만

    ```swift
    let idInputText: BehaviorSubject<String> = BehaviorSubject(value: "")
    let idValid: BehaviorSubject<Bool> = BehaviorSubject(value: false)
    let pwInputText: BehaviorSubject<String> = BehaviorSubject(value: "")
    let pwValid: BehaviorSubject<Bool> = BehaviorSubject(value: false)
    
    let idInputObservable: Observable<String> = idField.rx.text.orEmpty.asObservable()
    let idValidObservable = idInputObservable.map(checkEmailValid)
    
    // 3-1.
    idValidObservable.subscribe(onNext: { (b) in
        self.idValid.onNext(b)
    })
    .disposed(by: disposeBag)
    // 3-2.
    idValidObservable.bind(to: idValid)
        .disposed(by: disposeBag)
    // 3-3.
    idInputObservable.map(checkEmailValid)
        .bind(to: idValid)
        .disposed(by: disposeBag)
    // 3-1, 3-2, 3-3 모두 같은 동작!
    ```

  - 4단계: 더 간단히 표현하기 및 input, output 메서드 분리

    - viewDIdLoad 

      ```swift
      let idInputText: BehaviorSubject<String> = BehaviorSubject(value: "")
      let idValid: BehaviorSubject<Bool> = BehaviorSubject(value: false)
      let pwInputText: BehaviorSubject<String> = BehaviorSubject(value: "")
      let pwValid: BehaviorSubject<Bool> = BehaviorSubject(value: false)
      
      override func viewDidLoad() {
          super.viewDidLoad()
          bindInput()
          bindOutput()
      }
      ```

    - Input

      ```swift
      func bindInput() {
          // 4단계: 위 3-1, 3-2, 3-3을 더 간단히 표현하기
          idField.rx.text.orEmpty
              .bind(to: idInputText)
              .disposed(by: disposeBag)
      
          idInputText
              .map(checkEmailValid)
              .bind(to: idValid)
              .disposed(by: disposeBag)
      
          pwField.rx.text.orEmpty
              .bind(to: pwInputText)
              .disposed(by: disposeBag)
      
          pwInputText
              .map(checkPasswordValid)
              .bind(to: pwValid)
              .disposed(by: disposeBag )  
      }
      ```

    - output

      ```swift
      func bindOutput() {
         idValid.subscribe(onNext: { isValidID in
           self.idValidView.isHidden = isValidID })
          .disposed(by: disposeBag)
      
          pwValid.subscribe(onNext: { isValidPW in
              self.idValidView.isHidden = isValidPW })
              .disposed(by: disposeBag)
      
          Observable.combineLatest(
              idValidObservable,
              pwValidObservable, 
              resultSelector: { $0 && $1 })
              .subscribe(onNext: { b in
                  self.loginButton.isEnabled = b
              })
              .disposed(by: disposeBag) 
      }
      ```

      

### 11. 확장 라이브러리들 그리고 마무리

- RxCocoa
  - Driver
  - Binding
  - Relay
- Unfinished Observable / Memory Leak
  - (참조) [클로져와 메모리 해제 실험](https://iamchiwon.github.io/2018/08/13/closure-mem/)
  - Tip: ViewWillDisappear 안에 ``disposeBag = DisposeBag`` 으로 해결 가능!

- 추천!!
  - [RxViewController](https://github.com/devxoul/RxViewController)
  - [RxOptional](https://github.com/RxSwiftCommunity/RxOptional)
  - [RxExtension](https://github.com/tokijh/RxSwiftExtensions)
  - RxGesture
- 참고 : [RxSwift Community Projects](https://community.rxswift.org/) 