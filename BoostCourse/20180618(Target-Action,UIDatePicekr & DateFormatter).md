# 2018/06/18
# Target-Action
- Target-Action 디자인 패턴이란?
  - 타겟 : 프레임워크 객체를 포함한 모든 객체, 보통 VC가 일반적이다. `액션이 호출될 객체`
    - 객체는 이벤트가 발생할 때 다른 객체에 메시지(액션 메세지)를 보내는 데 필요한 정보를 포함한다.
  - 액션 : 특정 이벤트가 발생했을 때 호출할 메서드
  - 왜 사용할까?
    - 같은 메서드가 여러 클래스에 정의되어 있는 경우도 있고, 그런 클래스의 인스턴스가 여러개인 상황도 있다. 이런 여러 가지 상황에서 우리가 원하는 객체를 Target으로 지정하면 해당 액션을 실행할 객체를 상황에 따라서 선택할 수 있기 때문에.

- 액션 메서드의 두가지 방식
  ```
  // 프로그래밍 방식
  @objc func doSomething(_ sender: Any) {

  }

  // 인터페이스 빌더
  @IBAction func doSomething(_ sender: Any) {

  }
  ```

- 컨트롤 이벤트의 종류 : 컨트롤 이벤트는 `UIControlEvents`라는 타입으로 정의되어 있다.(`UIControlEvents.이벤트이름`)

  1. touchDown : 컨트롤을 터치했을 때 발생하는 이벤트
  2. touchDownRepeat : 컨트롤을 연속 터치 할 때 발생하는 이벤트
  3. touchDragInside : 컨트롤 범위 내에서 터치한 영역을 드래그 할 때 발생하는 이벤트
  4. touchDragOutside : 터치 영역이 컨트롤의 바깥쪽에서 드래그 할 때 발생하는 이벤트
  5. touchDragEnter : 터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔다가 다시 들어왔을 때 발생하는 이벤트
  6. touchDragExit : 터치 영역이 컨트롤의 일정 영역 바깥쪽으로 나갔을 때 발생하는 이벤트
  7. touchUpInside : 컨트롤 영역 안쪽에서 터치 후 뗐을때 발생하는 이벤트
  8. touchUpOutside : 컨트롤 영역 안쪽에서 터치 후 컨트롤 밖에서 뗐을때 이벤트
  9. touchCancel : 터치를 취소하는 이벤트 (touchUp 이벤트가 발생되지 않음)
  10. valueChanged : 터치를 드래그 및 다른 방법으로 조작하여 값이 변경되었을때 발생하는 이벤트
  11. primaryActionTriggered : 버튼이 눌릴때 발생하는 이벤트 (iOS보다는 tvOS에서 사용)
  12. editingDidBegin : `UITextField`에서 편집이 시작될 때 호출되는 이벤트
  13. editingChanged : `UITextField`에서 값이 바뀔 때마다 호출되는 이벤트
  14. editingDidEnd : `UITextField`에서 외부객체와의 상호작용으로 인해 편집이 종료되었을 때 발생하는 이벤트
  15. editingDidEndOnExit : `UITextField`의 편집상태에서 키보드의 `return` 키를 터치했을 때 발생하는 이벤트
  16. allTouchEvents : 모든 터치 이벤트
  17. allEditingEvents : `UITextField`에서 편집작업의 이벤트
  18. applicationReserved : 각각의 애플리케이션에서 프로그래머가 임의로 지정할 수 있는 이벤트 값의 범위
  19. systemReserved : 프레임워크 내에서 사용하는 예약된 이벤트 값의 범위
  20. allEvents : 시스템 이벤트를 포함한 모든 이벤트

# UIDatePicker & DateFormatter
## UIDatePicker
  - Date Picker는 날짜 및 시간을 입력하는 컨트롤, 특정 시점의 날짜와 시간 또는 시간 간격을 입력할 수 있다.
  - 주요 프로퍼티
    - `var datePickerMode: UIDatePickerMode`: Date picker의 모드를 결정
      - 기본값은 `dateAndTime`
      - time, date, dateAndTime, countDownTimer 네가지 모드를 설정할 수 있다.
    - `var date`: Date: date picker에 보여지게 될 날짜
    - `var calendar`: Calendar!: date picker에 사용되는 캘린더
    - `var locale: Locale?`: date picker에서 사용하는 로케일
    - `var timeZone: TimeZone?`: date picker에서 표시된 날짜에 반영된 시간대
    - `var maximumDate: Date?`: date picker에서 보여줄 수 있는 최대 날짜
    - `var minimumDate: Date?`: date picker에서 보여줄 수 있는 최소 날짜
    - `minuteInterval`: Int: date picker에서 분을 표시하는 간격. 기본값과 최솟값은 1이고 최댓값은 30
    - `var countDownDuration: TimeInterval`: date picker의 모드가 countDownTimer로 설정될 경우 date picker에 표시되는 초깃값
  - 주요 메서드
    - `func setDate(Date, animated: Bool)`: date picker에 처음 표시할 날짜를 설정

## DateFormatter
  - 주요 메서드와 프로퍼티
    - `func date(from: String)`: 주어진 문자열을 Date 객체(날짜와 시간)로 변환하여 반환
    - `func string(from: Date)`: 주어진 Date 객체를 문자열로 변환하여 반환
    - `func setLocalizedDateFormatFromTemplate(String)`: 지정된 로케일을 사용하여 날짜 형식을 설정
    - `var dateStyle: DateFormatter.Style`: DateFormatter의 날짜 형식
    - `var timeStyle: DateFormatter.Style`: DateFormatter의 시간 형식
    - `var dateFormat: String!`: 고정 형식 날짜 표현을 사용할 때의 날짜 형식
    - `var locale: Locale!`: DateFormatter의 로케일
    - `var timeZone: TimeZone!`: DateFormatter의 시간대
  - 예제
    1. 날짜 형식(Date 객체) -> 문자열 형식(textual representation)
      ```
      import UIKit

      let dateFormatter = DateFormatter()
      dateFormatter.dateStyle = .full
      dateFormatter.timeStyle = .none

      let date = Date(timeIntervalSinceReferenceDate: 118800)

      // US English Locale (en_US)
      dateFormatter.locale = Locale(identifier: "en_US")
      print(dateFormatter.string(from: date)) // Tuesday, January 2, 2001

      // KOR Korean Locale (ko_KR)
      dateFormatter.locale = Locale(identifier: "ko_KR")
      print(dateFormatter.string(from: date)) // 2001년 1월 2일 화요일
      ```

    2. 문자열 형식 -> 날짜 형식
      ```
      import UIKit

      let dateFormatter = DateFormatter()

      let dateString = "1970-01-01 08:03:30 +0000"
      dateFormatter.dateFormat = "yyyy-MM-dd HH:mm:ss ZZZ"
      print(dateFormatter.date(from: dateString)!) // 1970-01-01 08:03:30 +0000
      ```
