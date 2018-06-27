# 2018/06/21 (JK Feedback 강의)
## XIB vs StoryBoard

### XIB(NIB)이란?
- NIB(Next Interface Builder) : NIB파일(인터페이스 빌더 리소스 파일), 현 시점에서 NIB은 없다.
- XIB(XML Interface Builder) : XIB 파일은 XML 형식이라서 사람이 읽을 수 있고, 형상관리 도구에서 추적도 가능하다.
  - 애플이 NextStep을 인수하면서, 당분간 NIB을 썼었다. 하지만, NIB파일이 Binary파일로 되어있기 때문에 사람이 읽을 수 없어서, XML파일이 베이스인  XIB로 바꾸었다.
  - XML이란? HTML을 표현하기 위한 확장 방식.
- 특징
  - 화면 UI를 기록하는 XML
  - 안드로이드의 layout XML과 비슷
  - XIB에는 하나 이상의 뷰 객체가 존재할 수 있음
  - 소스버전관리 사용을 위해 nib 대신 xib 사용
  - MVC 구조에서 뷰와 컨트롤러를 분리하기 위함

- IPA 앱 Bundle 구조와 관련성
  - 앱 번들 내부 Resources 디렉토리에 위치
  - 컴파일된 결과가 저장됨 예) CustomCell.xibc
  - 실제로는 뷰 객체가 **아카이브**(**Archived**) 되어 있음
  - 실행시점에 Unarchive해서 파일 소유자(File’s owner)에 연결
  - 인스턴스 변수에 아웃렛(IBOutlet) 연결

- 아카이브된 뷰-객체 관련 UIView 메소드
  - 뷰 객체를 모두 언아카이브(unarchive) 처리한 직후 호출
    ```swift
    override func awakeFromNib() {
        print("awakeFromNib")
        super.awakeFromNib()
    }
    ```
  - 인터페이스 빌더에서 만든 뷰 객체를 언아카이브할 때만 호출
    ```swift
    required init?(coder aDecoder: NSCoder) {
        print("initWithCoder")
        super.init(coder: aDecoder)
    }
    ```
  - 뷰 객체를 직접 생성할 때만 호출
  - 지정 초기화 (designated initializer) 메소드
    ```swift
    override init(frame: CGRect) {
        print("initWithFrame")
        super.init(frame: frame)
    }
    ```

- XIB 만드는 방법
  - 새 파일 만들기 (File > New > Files... ) > User Interface > View
  - Hidden View : 스토리보드에서는 특정 슈퍼뷰에 하위에 속하지 않는 뷰를 만들 수 없지만 XIB에서는 (슈퍼뷰에 속하지 않은 상태로) 숨겨진 뷰를 만들어서 IBOutlet으로 연결할 수 있다.
  - 사용방법
    - NSBundle
      ```swift
      NSArray *nibObjects = [[NSBundle mainBundle] loadNibNamed:@"NXMyView"
                                                    owner:self
                                                  options:nil];
      UIView *nibView = [nibObjects objectAtIndex:0];
      var nibObjects = Bundle.main.loadNibNamed("NXMyView", owner: self, options: nil)
      var nibView = nibObjects?.first as! UIView
      ```
    - UIViewController
      ```swift
      UIViewController *aViewController
        = [[UIViewController alloc] initWithNibName:@"NXMyView"
                                            bundle:nil];
      [self.detailView addSubview:aViewController.view];
      var aViewController = UIViewController.init(nibName: "NXMyView", bundle: nil)
      self.detailView.addSubview(aViewController.view)
      ```
- 요약
  - 독립적인 뷰 디자인
  - 뷰단위 재사용성 높음
  - 화면사이즈 / 로컬라이즈 리소스 미리 보기
  - 동적으로 로딩 가능 (Lazy Loading)
  - 적용하기 어려운 경우
    - 콘텐츠 구성이나 레이아웃이 동적으로 바뀌는 경우
    - 인터페이스 빌더에서 바꿀 수 없는 속성
    - 뷰 컨트롤러 사이의 연결 (Transition Animation)

- **결론 : 코드로 화면 요소를 만드는 것을 권장하는 조직도 있지만, 항상 옳은 선택은 아니다.**
  - 아래 조건에 따라서 선택하도록 하자.
    - 반복적으로 재사용하는 단위가 뷰인가? 아니면 뷰컨트롤러인가?
    - 빠른 prototype을 제작을 위한 화면 전체 흐름이 중요한가?
    - 코드로 처리해야만하는 커스텀 UI 처리가 얼마나 많은가?
    - 유니버설 앱이면서 화면 대응, 버전 대응, 단말 대응을 해야하는가?
    - 서버에서 주는 데이터 구조에 따라 달라지는 동적 화면인가?
    - 화면 레이아웃 처리를 디자인 타임에 하는가? 런타임에 하나?
    - UI 리소스가 얼마나 많은거나 복잡한가?
    - 팀내에서 코드가 익숙한가? IB가 익숙한가?
