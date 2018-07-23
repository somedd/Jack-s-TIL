# 2018/07/21
# Let us go Summer(https://iosdevkor.github.io/let_us_go_2018_summer/)

## 1. Xcode에서 디버깅하기 (이재성님)
- Debug
- BreakPoint
- lldb: Xode에서 기본으로 내장되어 있는 디버거.
  - 주요 명령어
    - print: 값출력
      - p/x(16진수), p/o(8진수), p/t(이진수)
    - expr: 값입력
    - po
- Symbolicate: 받은 Crash 로그를 분석하기 위함.
- ETC
  - View hierarchy

## 2. 코드 응집도 높이기 (곰튀김님)
- 응집도를 높인다는 것? 흩어져있는 코드(메서드)들을 보기 쉽게 놓는 것.
- 응집도를 왜 높여야 할까?
  - 읽기 쉽고, 따라가기 쉽고, 이해하고, 찾고, 유지보수하기 쉬워지기 때문에!
- Case #1. Data + Logic + UI: `//Mark`를 활용하여, 각각 나눈다.
- Case #2. Data Setter:
- Case #3. Overrides
- Case #4. Selector
- Case #5. Delegate
- Wrapper를 사용한다는 개념!

## 3. Observable Operator (엉덩숭아님)
- 모르겠음......
- https://github.com/fimuxd/RxSwift

## 4. iOS TDD 실무에 적용하기 (유금상(AnyObject)님)
### 4-1. iOS TDD 하는법
- TDD를 하기 위해서는 팀을 설득시켜야하는데, 미지에 대한 두려움 떄문에 적용하지 못하고 있음. 이를 해결 하기 위해서는 지식이 필요함.
- 그렇다면 지식을 전달하는 방법은?
  - 가르치는 느낌이 들면 안되고, 존중 받는 느낌이 들게 얘기를 해야됨. 즉, 함께 찾아내보자!
  - 또한, 팀, 상사, 다른직군 등을 설득하자!
- 신뢰!!!!!가 가장 중요함.

### 4-2. 어떻게 적용할까?
- 계획하기
  - 가능한 자세하게.
  - 빼먹지 말것.ㅌㅈ
- 디자인, 기획, 서버가 완전히 끝나야 개발을 시작할 수 있다고 생각해서느 안된다.
- 하는 방법!
  - 커맨드 + U 후의 주기가 빨라야 한다.
    - 시뮬레이터에 앱이 실행/종료되는 과정이 포함되기 때문에, 큰 프로젝트는 굉장히 느리다.
    - 이를 위해, TestTarget을 분리한다.
  - WWDC 2018 Testing And Tips
- 상황별 TDD 방법
  - 레거시 코드: 레거시 코드 자체가 아닌 덧붙이는 코드를 TDD해야한다.

## 5. Texture Reactive Wrapper 만들고 응용하기.
- Texture란? UIKit를 베이스로 퍼포먼스를 높이기 위한 프레임워크.
  - 퍼포먼스가 넘나 좋음. main Thread만 쓰지 않기 때문에.
  - Constraints가 없음!

## 6. 미리보는 Marzipan
- Marzipan = iOSMac
