# 2018/06/15 (JK Feedback 강의)
## ML(Machine Learning) iOS Programming
  - ML은 현재 나온지 2-3년이 되어가고 있는데, 각 분야로 ML을 어떻게 쓸 것인가? 고민하고 있음.
  - 앞으로 할 수 있는 것이 훨씬 많아질 것인데, 그 전에 현재까지 얼마나, 또는 어떻게 쓰는지에 대해 공부해보는 시간.
  - 순서
    1. iOS 개발자에게 ML이란?
    2. ML의 배경
    3. CreateML

### iOS 개발자에게 ML이란?
  - 먼저, **알고 있다는 지식** 이라는 것은 두 가지로 나누어질 수 있음.
    - 형식지(Explicit Knowledge) : TV를 켜기 위해서 해야하는 일과 같이 절차가 있고 굉장히 형식적인 것.
    - 암묵지(Tacit Knowledge) : 걷는 것, 말하는 것, 코딩하는 것과 같이 형식적이고 규칙적이지 않은 것.
  - Descriptive(형식지) VS Procedural(암묵지)
    - 형식지는 선언적으로 표현이 가능해서, 절차가 명확하고 누구나 똑같이 배울 수 있음.
      - Ex) 구구단, 프로그램 코드
    - 암묵지는 설명하기 어렵고, 배우는 과정도 다르고 알려주는 방식도 재각각이다.
      - Ex) 외국어 배우기, 피아노 연주하기, 자전거 타기, 사람얼굴 인식하기
  - 이 일을 컴퓨터한테 시켜본다면, 어떨까?
    - 형식지는 프로그래밍 구현이 비교적 쉽다. (알고리즘 구현)
    - 암묵지는 프로그래밍 구현이 상대적으로 어렵다. (인공지능, 신경망, ML)

### ML의 배경
  - **신경망** 을 따라 만든 것. (**뉴런** 의 반응작용.)
  - 어떤 입력을 받았을 때, 주변 시냅스들에게 어떤 영향을 주는 지를 기반으로 했다.
  - ANN(인공지능 뉴런 네트워크)
    - XOR

### CreateML
  - 현재 제일 잘하고 있는 것들이, 이미지 분석이다. 또한, 트레이닝(학습)을 많이 해야 정확해짐.
    - **즉 중요한 것이 얼마나 많은 데이터를 학습하게 하느냐가 중요하다.**
    - 참고 : https://developer.apple.com/videos/play/wwdc2018/703/
    - 최근에는 각 도구들이 많아지고, 논문이 많아지면서, 공유를 하기 시작하고, 입증을 위한 경쟁이 시작됐다.
    - 그 중에 애플도 ML의 Model들을 제공하기 시작했음. 대부분 물체 인식 관련 모델들이 많다.  (https://developer.apple.com/machine-learning/build-run-models/)
  - 어떻게 사용하는가? ML Model을 앱에 넣고 사용하면 된다.
    - Model은 일반적으로 제공하기에 사용하기만 하면된다.
  - 하지만, ML Model은 어떻게 만들까? **CreateML** 을 import한다.(Ex) 필기체 인식
    - Model을 만들기 위한 Swift Class들. (DataSource, DataTable 등등.. / PDF파일 참고)
    - 직접 개인의 데이타들을 넣어주기만 해도 만들어 줌.
      1. Image
      ```
      import AppKit
      import CreateML

      let builder = MLImageClassfierBuilder.init()
      builder.showInLiveView()
      ```
      2. Text : 긍정적인 글과 부정적인 글 분석하기
      3. Tabular Data : 예를 들어, 방의 갯수, 화장실 갯수, 위치, 평수를 통해서 집의 가격을 예측하는 것.

  - **결론은 프로그래밍으로 복잡한 코드를 짜야하는 일들을 ML을 통해서, 보다 간단히 해결할 수 있다는 것!**
    - 또한, 이를 응용한 앱을 만들수도 있다는 것을 생각해보길.
