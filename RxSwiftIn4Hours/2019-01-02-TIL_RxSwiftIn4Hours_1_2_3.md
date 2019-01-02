# 2018/01/02

## RxSwift in 4 hours (1,2,3/11) by 곰튀김님

- ### 출처

  - [Github링크](https://github.com/iamchiwon/RxSwift_In_4_Hours)
  - [영상링크](https://youtu.be/2uumx7Vzidc)

- ### 목차

  1. ReactiveX 사이트 둘러보기
  2. 비동기 작업과 Observable
  3. Disposable / DisposeBag
  4. 기본 Operators
  5. Operator 종류들
  6. Marble Diagram 이해하기
  7. Next, Error, Completed
  8. Scheduler
  9. RxSwift 응용해보기
  10. Subject
  11. 확장라이브러리들 그리고 마무리

### 1. ReactiveX 사이트 둘러보기

- RxSwift는 ReactX 시리즈들중에 하나로, Observable Stream을 가지고, 비동기 프로그래밍하기 위한 API이다. 맨 처음 MS에서 만들었다.
  - <http://reactivex.io/> - Docs에서 한국어가 제공되니, 한번 정독하자 고고
  - [RxSwift](https://github.com/ReactiveX/RxSwift)
- RxSwift를 왜 쓸까?
  - Async한 작업들을 간결하게 쓰기 위해.

- 사이트 내부 카테고리
  - **Docs**
    - **Observable**: 제일 중요.
    - **Operators**: 더 잘 쓸 수 있다.
    - Single: 알면 좋다.
    - **Subject**: 내가 무언가를 만들 수 있다.
    - **Sceduler**: 여러 군데 활용할 수 있다.
  - Languages: 이 개념을 알면, 다른 언어에서도 사용할 수 있다.
  - Resources: 강좌, 예제 등 자료들을 얻을 수 있다.

### 2. 비동기 작업과 Observable

- Sync/Async 비교

  - DispatchQueue에는 2가지(**ConcurrecyQueue, SerialQueue**), 2가지(**Sync, Async)**가 있다.
    - Concurrecy Queue - Sync 또는 Async
      - Ex. `DispatchQueue.global()`
    - SerialQueue - Sync 또는 Async

  - Swift

    - Sync

      ``````swift
       @IBAction func onLoadSync(_ sender: Any) {
          guard let url = URL(string: loadingImageUrl) else { return }
          guard let data = try? Data(contentsOf: url) else { return }
           
          let image = UIImage(data: data)
          imageView.image = image
      }
      ``````

    - Async

      ``````swift
      @IBAction func onLoadAsync(_ sender: Any) {
          DispatchQueue.global().async {
              guard let url = URL(string: loadingImageUrl) else { return }
              guard let data = try? Data(contentsOf: url) else { return }
      
              let image = UIImage(data: data)
              DispatchQueue.main.async {
                  self.imageView.image = image
              }
          }
      }
      ``````

- PromiseKit: 비동기 프로그래밍 라이브러리 중 하나. 다른 언어에서 널리 사용됨.

  - `Promise`를 `seal`에다가 `fulfill`로 전달. `done`으로 결과를 받아서 처리.

  ``````swift
  @IBAction func onLoadImage(_ sender: Any) {
      imageView.image = nil
  
      promiseLoadImage(from: loadingImageUrl)
          .done { image in
              self.imageView.image = image
          }.catch { error in
              print(error.localizedDescription)
          }
  }
  
  // MARK: - PromiseKit
  
  func promiseLoadImage(from imageUrl: String) -> Promise<UIImage?> {
      return Promise<UIImage?>() { seal in
          asyncLoadImage(from: imageUrl) { image in
              seal.fulfill(image)
          }
      }
  }
  ``````

- RxSwift

  - `Observable`를 `seal`에다가  ` Next`로 전달. `subscribe`으로 결과를 받아서 처리.

  ```swift
  @IBAction func onLoadImage(_ sender: Any) {
      imageView.image = nil
  
      _ = rxswiftLoadImage(from: loadingImageUrl)
          .observeOn(MainScheduler.instance)
          .subscribe({ result in
              switch result {
              case let .next(image):
                  self.imageView.image = image
  
              case let .error(err):
                  print(err.localizedDescription)
  
              case .completed:
                  break
              }
          })
  }
  
  @IBAction func onCancel(_ sender: Any) {
  }
  
  // MARK: - RxSwift
  
  func rxswiftLoadImage(from imageUrl: String) -> Observable<UIImage?> {
      return Observable.create { seal in
          asyncLoadImage(from: imageUrl) { image in
              seal.onNext(image)
              seal.onCompleted()
          }
          return Disposables.create()
      }
  }
  ```

### 3. Disposable DisposeBag

```swift
var disposable: Disposable?
disposable?.dispose()

var disposeBag = DisposeBag()
```