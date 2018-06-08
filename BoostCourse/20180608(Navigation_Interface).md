# 2018/06/08
## Navigation Interface

1. Navigation Controller
2. Navigation Stack
3. Navigation Interface 구현방법
4. Navigation Bar

## 0. Navigation Interface란?
  - 계층적 구조의 화면전환을 위해 사용되는 ``드릴 다운 인터페이스.``
  - ``드릴 다운 인터페이스``란, 각 항목에 대한 세부항목이 존재하는 인터페이스

## 1. Navigation Controller
  - 네비게이션 컨트롤러는 ``컨테이너 뷰 컨트롤러로써, 네비게이션 스택을 사용하여, 다른 뷰 컨트롤러들을 관리한다.`` 이때, 네비게이션 스택에 담기는 뷰컨트롤러들을 ``컨텐트 뷰 컨트롤러``라고 한다.
  - 네비게이션 컨트롤러는 두 개의 뷰를 화면에 표시한다.
    1. 상위 네비게이션 컨트롤러의 뷰(화면의 상하에 보이는 뷰)
    2. 네비게이션 스택 내부 최상위 컨텐트 뷰 컨트롤러의 뷰

## 2. Navigation Stack
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


## 3. Navigation Interface 구현방법
  1. Navigation Controller에 포함할 뷰 컨트롤러에서 [Editor] - [Embed In] - [Navigation Controller]
  2. 코드로 생성 : ``UINavigationController(rootViewController: 루트 뷰 컨트롤러로 설정할 뷰 컨트롤러)``

## 4. Navigation Bar
  - 네비게이션 타이틀과 네비게이션 아이템으로 이루어져 있으며, 네비게이션 아이템도 또한 Stack으로 관리되며, 보여진다.

## 5. 참고 문서 / 링크
  - https://developer.apple.com/ios/human-interface-guidelines/app-architecture/navigation/
  - https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/NavigationControllers.html
  - https://developer.apple.com/documentation/uikit/uinavigationbar
  - https://developer.apple.com/documentation/uikit/uinavigationcontroller
