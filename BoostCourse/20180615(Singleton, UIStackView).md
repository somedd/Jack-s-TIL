# 2018/06/15
# Singleton Pattern
- 싱글톤이란? `특정 클래스의 인스턴스가 오직 하나임을 보장하는 객체`를 의미한다.
  - 특징으로는, 애플리케이션이 요청한 횟수와 관계 없이 이미 생성된 같은 인스턴스를 반환한다.
- `Cocoa Framework`에서의 싱글톤 디자인 패턴
  - FileManager : 애플리케이션 파일 시스템 관리
  - URLSession : URL 세션 관리
  - NotificationCenter : 등록된 notification 관련 정보를 사용
  - UserDefaults : Key-Value 형태로, 데이터 저장 및 관리
  - UIApplication : 중앙제어 애플리케이션 객체
- 주의할점!
  - 환경설정, 네트워크 연결처, 데이터 관리 등등 여러 개 만들어질 필요가 없는 경우에 많이 사용한다. 하지만, `멀티 스레드 환경에서 동시에 싱글턴 객체를 참조할 경우 원치 않은 결과를 가져올 수 있다.`

# UIStackView
  - 스택 뷰의 레이아웃은 다음과 같은 프로퍼티를 통해 조정한다.
    - axis
    - distribution
    - alignment
    - spacing
  - 스택 뷰는 `arrangedSubviews`프로퍼티로 포함된 뷰들을 관리한다. 이 프로퍼티는 순서가 있는 배열이라고 할 수 있다.
  - UIStackView 클래스의 주요 프로퍼티
    - `var arragedSubviews: [UIView]`
    - `var axis`
    - `var distribution`
    -  `var spacing`
  - UIStackView의 주요 메서드
    - `func addArragedSubview(UIView)` : 배열 마지막에 뷰를 추가한다.
    - `func insertArragedSubview(UIView, at: Int` : 특정 인덱스에 뷰를 추가한다.
    - `func removeArragedSubview(UIView)` : 스택뷰의 배열로부터 뷰를 제거한다.
