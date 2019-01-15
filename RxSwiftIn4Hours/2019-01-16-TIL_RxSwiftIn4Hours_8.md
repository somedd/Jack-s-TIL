# 2018/01/16

## RxSwift in 4 hours (8/11) by 곰튀김님

- ### 출처

  - [Github링크](https://github.com/iamchiwon/RxSwift_In_4_Hours)
  - [영상링크](https://youtu.be/2uumx7Vzidc)

### 8. Scheduler

- Step2 소스 수정해가면서, 진행!
- `exMap3()`의 예제에서 IBAction으로 받았다는 것은 main thread에서 모두 동작하는 것이다. 즉, 비동기 처리가 안되고 있다는 것.

- `observeOn(Scheduler)`을 활용해서 사용한다.

  - `observeOn`아래로부터 지정해 놓은 Scheduler가 처리한다.

  ```swift
  @IBAction func exMap3() {
  Observable.just("800x600")
      .map { $0.replacingOccurrences(of: "x", with: "/") }
      .map { "https://picsum.photos/\($0)/?random" }
      .map { URL(string: $0) }
      .filter { $0 != nil }
      .map { $0! }
      .observeOn(ConcurrentDispatchQueueScheduler(qos: .default)) // Data를 받는 부분
      .map { try Data(contentsOf: $0) }
      .map { UIImage(data: $0) }
      .observeOn(MainScheduler.instance) // main thread에서 동작해야되기 때문에!
      .subscribe(onNext: { image in
          self.imageView.image = image
      })
      .disposed(by: disposeBag)
  }
  ```

-  `subscribeOn(Scheduler)`

  - subscribe이 될 때 부터 지정한 Scheduler가 처리한다는 의미로, 위의 `.observeOn(ConcurrentDispatchQueueScheduler.init(qos: .default))` 다르게 Data를 받기 전이나 후에 넣어도 된다.

- Tip

  - 아래의 메서드로도 충분하다.
    - `.observeOn(ConcurrentDispatchQueueScheduler(qos: .default))`
    - `.observeOn(MainScheduler.instance)`

- Side-Effect

  - 외부에 영향을 주는 부분.

  - Side-Effect를 허용해주는 것은 `subscribe`과 `do`다.

### 
