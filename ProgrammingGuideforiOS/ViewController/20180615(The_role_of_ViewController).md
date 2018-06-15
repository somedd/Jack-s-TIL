# ViewController Programming Guide for iOS
## 2018/06/15
[원문 링크](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/index.html#//apple_ref/doc/uid/TP40007457-CH2-SW1)

# OverView

## The Role of View Controllers

- 뷰컨트롤러의 역할
	1. Each view controller manages a portion of your app’s user interface
	2. as well as the interactions between that interface and the underlying data.
	3. View controllers also facilitate **transitions** between different parts of your user interface.

- The UIViewController class defines the methods and properties for managing your views,
- handling events, transitioning, and coordinating with other parts of your app.

- 뷰컨트롤러의 두가지 타입
	1. content
	2. Container

### View Management
- The view controller always has a reference to its root view and each view has **strong references** to its subviews.

- Container VC
	- The container does not manage the content of its children.
	- It manages only the root view, sizing and placing it.

### Data Marshaling

> Marshaling? 한 객체의 메모리에서의 표현방식을 저장 또는 전송에 적합한 다른 데이터 형식으로 변환하는 과정.

- VC는 뷰와 앱의 data를 사이의 intermediary를 수행.
- When you subclass UIViewController, you add any variables you need to manage your data in your subclass.
- **You should always maintain a clean separation of responsibilities within your view controllers and data objects.**
- Most of the logic for ensuring the integrity of your data structures belongs in the data objects themselves.
- UIDocument object

---


- You should always maintain a clean separation of responsibilities within your view controllers and data objects. Most of the logic for ensuring the integrity of your data structures belongs in the data objects themselves. The view controller might validate input coming from views and then package that input in the format that your data objects require, but you should minimize the view controller’s role in managing the actual data.

### User Interactions
- keywords: responder objects, responder chain, delegate, target, action, event

### Resource Management
- A view controller assumes all responsibility for its views and any objects that it creates.
- When the available free memory is running low, UIKit asks apps to free up any resources that they no longer need. -> ex) `didReceiveMemoryWarning`

### Adaptivity

- 환경에 따라 뷰컨트롤러를 바꾸지 말고, 환경에 맞게 뷰 컨트롤러를 활용하라.
- Coarse-grained changes happen when a view controller’s traits change.
- When the user rotates an iPhone from portrait to landscape, the size class might not change but the screen dimensions usually change.
