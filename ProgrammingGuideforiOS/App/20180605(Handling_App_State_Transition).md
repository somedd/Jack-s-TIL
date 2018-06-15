# App Programming Guide for iOS
## 2018/06/05

## Strategies for Handling App State Transitions
> 이번 섹션은 앱의 상태 변화에 따라 어떻게 코드를 작성해야 하는지에 대한 가이드라인과 팁.

> 앱의 상태전환이 일어날 때 시스템이 app object에게 알림을 주고, app object는 이를 app delegate에게 전달한다. When state transitions occur, the system notifies the app object, which in turn notifies its app delegate.

> 앱의 상태변화를 감지하고 이에 대응하기 위해서 `UIApplicationDelegate` 프로토콜의 메서드를 사용할 수 있다.

> 예를 들어, foreground -> background로 갈때 you might write out any unsaved data and stop any ongoing tasks.

### 1. What to Do at Launch Time.
-  app delegate’s `application:willFinishLaunchingWithOptions:` and `application:didFinishLaunchingWithOptions:` methods to do the following:
	- Check the contents of the launch options dictionary for information about why the app was launched, and respond appropriately.
	- Initialize your app’s critical data structures.
Prepare your app’s window and views for display:
		- Apps that use OpenGL ES for drawing must not use these methods to prepare their drawing environment. Instead, defer any OpenGL ES drawing calls to the applicationDidBecomeActive: method.
		- Show your app window from your application:willFinishLaunchingWithOptions: method. UIKit delays making the window visible until after the application:didFinishLaunchingWithOptions: method returns. -> window에 대한 준비를 이 두 메서드에서 하라.

- At launch time, the system automatically loads your app’s main storyboard file and loads the initial view controller. 메인스토리보드보드 파일을 로드하고 뷰 컨트롤러를 초기화


- application:willFinishLaunchingWithOptions: method to show your app window and to determine if state restoration should happen at all.
- Use the application:didFinishLaunchingWithOptions: method to make any final adjustments to your app’s user interface.

- `application:willFinishLaunchingWithOptions: method`와 `application:didFinishLaunchingWithOptions: method`의 과정은 5초이내로 완료해야한다.

- 초기화 과정에서 시간이 오래 걸리는 작업 같은경우는 보조스레드를 사용하면 좋다.

### The Launch Cycle

* not running > active, background > foreground(active), active상태로 가기전에 짧게 inactive state를 거친다.


## 2. What to Do When Your App Is Interrupted Temporarily
- applicationWillResignActive에서 구현해줄것
	- Save data and any relevant state information.
	- Stop timers and other periodic tasks.
	- Stop any running metadata queries.
	- Do not initiate any new tasks.
	- Pause movie playback (except when playing back over AirPlay).
	- Enter into a pause state if your app is a game.
	- Throttle back OpenGL ES frame rates.
	- Suspend any dispatch queues or operation queues executing non-critical code. (You can continue processing network requests and other time-sensitive background tasks while inactive.)

### Responding to Temporary Interruptions
- 예: 전화왔을 때 대응할 메서드가 어딘지

## 3. What to Do When Your App Enters the Foreground
- applicationWillEnterForeground:
- applicationDidBecomeActive:

## 4. What to Do When Your App Enters the Background
- foreground > background 갈 때 applicationDidEnterBackground: 사용
