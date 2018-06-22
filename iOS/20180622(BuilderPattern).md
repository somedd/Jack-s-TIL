# 2018/06/22
## Builder Pattern

### 빌더 패턴(Builder Pattern)이란?
- 복잡한 객체의 생성을 그 객체의 표현과 분리하여, 생성 절차는 항상 동일하되 결과는 다를 수 있게 만드는 패턴.

### 빌더 패턴의 구조.
![builderPatter_screensh1](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Builder_UML_class_diagram.svg/1400px-Builder_UML_class_diagram.svg.png)
- Director : 객체 생성 방식에 대한 책임을 진다. ConcreateBuilder를 인자로 받아 동작 수행.
- Builder : 객체 생성하는 추상 인터페이스
- ConcreteBuilder : Builder의 구현 클래스. 객체 생성 결과에 대한 구체적인 구현 책임을 진다.
- Product : Builder를 이용해서 Director가 만들어낸 최종 객체

### 왜 사용할까?
1. 불필요한 생성자를 만들지 않고 객체를 생성
2. 데이터의 순서에 상관 없이 객체를 생성
3. 사용자 입장에서 명시적으로 이해하기 쉽게 생성

### 빌더 패턴을 사용하기 좋은 경우
1. 여러 요소를 갖는 복잡한 객체를 생성할 필요가 있을 때
2. 어떤 객체를 여러 가지 방법으로 생성할 필요가 있을 때

### 빌더 패턴 VS 추상 팩터리 패턴
1. 주로 복잡한 객체 생성 <-> 객체의 단순, 복잡성은 상관없다.
2. 여러 단계를 거쳐 마지막 단계에서 객체 반환 <-> 한 단계로 객체를 생성하여 즉시 반환
3. 빌더를 통한 여러 가지 방법으로 객체를 생성 <-> 한 가지 방법으로 객체를 생성
4. 한 가지 타입의 특정 객체 생성에 초점 <-> 같은 종류의 여러 가지 객체 생성에 초점
