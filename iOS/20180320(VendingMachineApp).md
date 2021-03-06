# 2018/06/19
## VendingMachineApp 정리
- 이번 프로젝트에서 적용한 디자인패턴:
  - MVC패턴 : M,V의 코드 범용성(재사용성)을 높이고 자 할 때, 유지보수하기 쉬운 구조를 사용하고자 할때 (이러한 장점은 각 객체의 역할을 분리하기 때문에 가능)
  - 옵저버 패턴 : Model-Controller간 소통이 필요한 경우 - 타깃과 액션 : 해당 객체(타깃)에 직접 메서드(액션)를 지정해주고자 할 때
  - Rodponder Chain패턴 : 앱 사용시 발생하는 이벤트들을 처리 및 관리하고자 할 때 - 싱글톤 패턴 : 하나의 원본데이터만 사용하고자 할 때, 인스턴스를 만드는 데 리스크가 클 경우

- iOS프로그래밍
  1. MVC 객체 역할과 데이터 흐름
  2. ViewController 라이프사이클
  3. 커스텀 뷰 객체 만들기
  4. 뷰 Frame 과 Bound
  5. 상대적인 좌표 시스템
  6. 코어 그래픽스

- 이번 미션에서 공부한 iOS 프로그래밍 내용 중에서 학습하기 가장 어려웠던 것은 어떤 것인가?
  - 앱 생명주기 및 아카이빙, Responder Chain패턴

- 개발 경험
  1. 프로토콜에 의존하도록 의존성 역전 원칙을 구현했는가
  2. 정적 화면 만들기
  3. 코드로 동적 화면 만들기
  4. 숫자, 문자열 값을 의미있는 코드로 표현하기

- 레벨2에서 분리한 UserMode와 AdminMode 구조를 앱 만들때 적용하기 수월했나? 어려운 부분은 어떻게 개선했나?
  - 사용자/관리자 모드: 레벨 2에서 코드로만 구현했었던 UserController, AdminController를 각각 ViewController로 구현하는 과정에서 Model과 View와의 관계, 소통 및 동작방식을 이해하는 것이 어려웠습니다. 특히, 힌트로 나왔던 클래스 또는 메서드들을 사용해야할 때, 사용법을 몰라서 헤맸습니다. 예전에는 코드를 우선으로 구현해가면서 이해하는 방향으로 학습했었지만, 이번 미션에서는 동작원리 이해를 우선으로 하고, 코드로 적용해나가면서 해결하였습니다.

- 그 외에 학습하기 어렵거나 시간이 오래 걸린 것은 무엇이고, 어떻게 극복했나?
  - 앱 생명주기와 아카이빙 관련 학습을 하는데 오래걸렸습니다. 특히, 아카이빙/언아카이빙한 데이터를 저장하고 불러오는 시점을 정해주는 것을 고민했었는데, 앱 생명주기 개념을 정확히 이해하며 해결했습니다. (스탠포드 강의, 아론힐리가스의 iOS프로그래밍 책, 구글링만 하루 넘게 했었던..)
