# 2018/06/08
# 화면의 전환
  - #1. Navigation Interface
  - #2. 모달

## #1. Navigation Interface

1. Navigation Controller
2. Navigation Stack
3. Navigation Interface 구현방법
4. Navigation Bar

###  Navigation Interface란?
  - 계층적 구조의 화면전환을 위해 사용되는 ``드릴 다운 인터페이스.``
  - ``드릴 다운 인터페이스``란, 각 항목에 대한 세부항목이 존재하는 인터페이스

### 1. Navigation Controller
  - 네비게이션 컨트롤러는 ``컨테이너 뷰 컨트롤러로써, 네비게이션 스택을 사용하여, 다른 뷰 컨트롤러들을 관리한다.`` 이때, 네비게이션 스택에 담기는 뷰컨트롤러들을 ``컨텐트 뷰 컨트롤러``라고 한다.
  - 네비게이션 컨트롤러는 두 개의 뷰를 화면에 표시한다.
    1. 상위 네비게이션 컨트롤러의 뷰(화면의 상하에 보이는 뷰)
    2. 네비게이션 스택 내부 최상위 컨텐트 뷰 컨트롤러의 뷰

### 2. Navigation Stack
  - 가장 하위에 있는 VC(가장 먼저 추가된 VC)가 네비게이션의 루트 뷰 컨트롤러이며, 루트 뷰 컨트롤러는 네비게이션 스택에서 팝(Pop)되지 않는다. 네비게이션 스택의 가장 상위에 있는 VC(가장 나중에 추가된 VC)는 최상위 뷰 컨트롤러로 화면에 보이게 된다.
  - 네비게이션 스택에서의 화면이동
    - ``네비게이션 스택에 있는 VC들을 Push 또는 Pop을 이용하여 VC를 추가 또는 삭제``하며, ``UINavigationController``클래스의 메서드 또는 세그(Segue)를 이용하여 가능하다.

    1. ``UINavigationController``클래스의 메서드
      - ``func pushViewController(UIViewController, animated: Bool)``
        - 내비게이션 스택에 뷰 컨트롤러를 푸시하며, 푸시된 뷰 컨트롤러는 최상위 뷰 컨트롤러로 화면에 표시한다.
      - ``func popViewController(animated: Bool) -> UIViewController?``
        - 내비게이션 스택에 있는 최상위 뷰 컨트롤러를 팝하며, 최상위 뷰 컨트롤러 아래에 있던 뷰 컨트롤러의 콘텐츠가 화면에 표시됩니다.
      - ``func popToRootViewController(animated: Bool) -> [UIViewController]?``
        - 내비게이션 스택에서 루트 뷰 컨트롤러를 제외한 모든 뷰 컨트롤러를 팝하며, 루트 뷰 컨트롤러가 최상위 뷰 컨트롤러가 된다. 또한, 삭제된 모든 뷰 컨트롤러의 배열이 반환된다.
      - ``func popToViewController(_ viewController: UIViewController, animated: Bool) -> [UIViewController]?``
        - 특정 뷰 컨트롤러가 내비게이션 스택에 최상위 뷰 컨트롤러가 되기 전까지 상위에 있는 뷰 컨트롤러들을 팝한다.

    2. ``세그(Segue)``란? 스토리보드에서 한 화면에서 다른 화면으로의 전환


### 3. Navigation Interface 구현방법
  1. Navigation Controller에 포함할 뷰 컨트롤러에서 [Editor] - [Embed In] - [Navigation Controller]
  2. 코드로 생성 : ``UINavigationController(rootViewController: 루트 뷰 컨트롤러로 설정할 뷰 컨트롤러)``

### 4. Navigation Bar
  - 네비게이션 타이틀과 네비게이션 아이템으로 이루어져 있으며, 네비게이션 아이템도 또한 Stack으로 관리되며, 보여진다.

### 5. 참고 문서 / 링크
  - https://developer.apple.com/ios/human-interface-guidelines/app-architecture/navigation/
  - https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/NavigationControllers.html
  - https://developer.apple.com/documentation/uikit/uinavigationbar
  - https://developer.apple.com/documentation/uikit/uinavigationcontroller

## #2. 모달

### 모달이란?
  - 화면전환 기법으로, 이목을 집중해야 하는 화면을 다른 화면 위로 띄워(Presenting) 표현하는 방식으로, 꼭 이목을 끌어야하는 화면에서 사용한다.

### 1. ViewController를 화면에 나타내는 2가지 방법
  1. ``컨테이너뷰 컨트롤러에 Embed``하기
  2. 뷰컨트롤러의 나타내기(``present``) 사용하기.
    - 모든 뷰 컨트롤러 객체가 사용 가능하다.
    - 뷰 컨트롤러를 present하면, 이 전 뷰 컨트롤러와 계층이 형성되고, 사라질(``dismiss``) 때까지 유지된다.

### 2. 프레젠테이션 및 전환 프로세스
  - VC의 프레젠테이션은 프로그래밍 방식 또는 세그(Segue)를 사용하여 구현 가능하다.
  - 프레젠테이션 스타일 : VC의 ``modalPresentationStyle`` 프로퍼티에 상수를 할당하여 사용.
    1. 전체화면 프레잰테이션 스타일(`UIModalPresentationFullScreen`): 보여질 VC를 덮으면서, 화면 전체에 표시된다.
      - Tip : `UIModalPresentationOverFullScreen`을 사용하면, 투명도를 설정한만큼 하위 뷰가 보이도록 할 수 있다.
    2. 팝오버 스타일(`UIModalPresentationPopover`) : 추가정보, 포커스, 선택한 객체와 관련된 항목 목록을 표시하는데 사용한다. 팝업 뷰 외부에 탭을 하면 자동으로 팝업을 닫는다.(iPad에서만 지원가능)
    3. 현재 컨텍스트 스타일(`UIModalPresentationCurrentContext`) : 아래 VC의 컨텐츠 영역에 컨텐츠를 올리는 형태
    4. 커스텀 프레젠테이션 스타일 : 사용자가 직접 정의한다. (`UIPresentationController`)를 상속받아 사용.
      - https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/DefiningCustomPresentations.html#//apple_ref/doc/uid/TP40007457-CH25-SW1

  - 전환 스타일(Transition Style)
    - VC를 표시하는데 사용하는 애니메이션 유형을 결정하고, `modalTransitionStyle`프로퍼티에 지정하여, 기본 스타일을 설정할 수 있다.
      - https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/CustomizingtheTransitionAnimations.html#//apple_ref/doc/uid/TP40007457-CH16-SW1

### 3. ViewController를 나타내기 VS 보여주기
  - `UIViewController`클래스의 VC를 표시하는 두가지 방법
    - showViewController:sender:와 showDetailViewController:sender:메서드
      - 컨테이너뷰 컨트롤러는 뷰 컨트롤러를 모달 방식으로 표시하는 대신, 이를 서브뷰로 통합할 수 있다. 기본 동작은 뷰 컨트롤러를 모달 방식으로 표시합니다.
    - presentViewController:animated:completion:메서드:  뷰 컨트롤러를 항상 모달 방식으로 표시한다.
      - 이 메서드를 호출하는 뷰 컨트롤러는 궁극적으로 프레젠테이션을 처리하지 못할 수도 있으나, 프레젠테이션은 항상 모달 방식을 채택한다.

### 4. 다른 스토리보드에서 정의된 뷰 컨트롤러 접근
  ```
  let storyboard: UIStoryboard = UIStoryboard(name: "SecondStoryboard", bundle: nil)
  if let myViewController: MyViewController = storyboard.instantiateViewController(withIdentifier: "MyViewController") as? MyViewController {
  	self.present(myViewController, animated: true, completion: nil)
  }
  ```

### 5. 참고 문서 / 링크
  - https://developer.apple.com/ios/human-interface-guidelines/app-architecture/modality/
  - https://developer.apple.com/library/content/featuredarticles/ViewControllerPGforiPhoneOS/PresentingaViewController.html
