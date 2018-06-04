# App Programming Guide for iOS
## 2018/06/04
### The App Life Cycle 관련 내용 중 보완할 내용
  - 왜 알아야 할까?
    - 앱은 작성된 코드와 시스템 프레임 워크간의 정교한 상호작용입니다. 시스템 프레임 워크는 모든 앱의 실행에 필요한 기본 인프라를 제공하며, 개발자는 앱에 어울리는 모양과 느낌을 코드로 구현합니다. 이 둘의 효과적인 상호작용을 위해 iOS 작동원리에 대한 이해가 필요합니다.

## 1. iOS App의 메인함수
```
int main(int argc, char * argv[])
{
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
    }
}
```

### 1-1. App초기화(App Loading Process) 과정 단순화
  1. App 실행: main() 함수 실행됨
  2. main(): UIApplicationMain() 생성
  3. UIApplicationMain(): UIApplication 객체 생성
  4. UIApplication 객체: Info.plist 파일을 바탕으로 앱에 필요한 데이터와 객체 로드
  5. AppDelegate 객체 생성 및 UIApplication 객체와 연결
  6. 이벤트 루프 생성 등 실행에 필요한 준비 진행
  7. 실행 완료 직전, ``AppDelegate의 application(_:didFinishLaunchingWithOptions:)`` 메시지 전송


## 2. Threads and Concurrency
  - 시스템은 기본적으로 앱의 main thread를 생성하는데, 필요에 따라 추가 thread를 생성하여 다른 작업을 수행 할 수 있습니다. iOS 앱의 경우, 직접 thread를 만들고 관리하는 대신 Grand Central Dispatch(GCD), operation objects, asynchronous 프로그래밍 기법을 사용하는 것이 좋습니다.
    - GCD를 이용하면 수행하고 싶은 작업과, 작업의 순서를 정할 수 있지만, 시스템이 CPU에서 작업을 가장 효과적으로 수행할 수 있는 방법을 결정 할 수 있도록 하는 것이 전반적인 성능을 향상시키고, 코드를 단순화 시킬 수 있습니다.
    - Thread와 concurrency(동시성)를 사용할때 다음 사항을 고려하세요.
      - View, Core Animation 그리고 UIKit 클래스와 관련된 작업은 main thread에서 실행되어야 합니다.
      - 오래 걸리는 작업은 백그라운드 스레드에서 수행해야합니다. 네트워크 작업을 포함하거나, 파일에 접근하거나, 많은 양의 데이터를 처리할 때는 GCD를 이용하여 비동기로 수행해야합니다.
