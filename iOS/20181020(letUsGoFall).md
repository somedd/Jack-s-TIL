# 2018/10/20

# Let us go fall(https://iosdevkor.github.io/let_us_go_2018_fall/)

## 1. React-Native 도전 후기 (클린트님)

## 2. 알아보자 DI와 Deli(kawoou님)

- Dependency Injection?
  - 왜 써야할까? 
  - IoC Container
  - DELI (https://github.com/kawoou/Deli)
    - Component 
    - Autowired

## 3. Debugging With Xcode, LLDB and Chisel (민소네님)

- 왜 LLDB를 파게 되었는가?
  - swift 기반 프로젝트의 컴파일 속도가 느려서
- LLDB 명령어
  - 일반
    - continue(c)
    - next(n)
    - step in(s)
    - finish
  - 변수검사 (frame: )
    - frame variable(v) : 해당 frame에서의 모든 변수를 보여줌
    - frame variable --no -args 
    - frame info : 현재 frame 정보
    - up : frame 위로 이동
    - down 3 : frame 아래로 이동
    - frame select 12
  - Thread 상태
    - thread liss
    - thread select 
    - thread until  19(line number)
    - thread jump --line 19(line number) : 뒤로 갈 경우, 메모리 점프에 의해서 crash가 발생할 수 있다.
    - thread return 
    - thread backtrace(bt) (all)
  - Evaluating Expression (표현식 계산)
    - settings set target.language swift 선언해야됨.
    - expr var
  - 기본적으로 Python이 내장되어 있음.
- Chisel 툴 소개
  - Facebook에서 만듬. 내장 언어가 모두 Python.
  - 접근성, **Autolayout 관련 명령어**를 지원
  - View를 이미지로 만들어서 preview로 볼 수 있음.

## 4. Swift Generics (과니님)

- 유연하고, 재사용성이 가능한 개발을 할 떄 사용한다라고 명시되어있음.
- Type Safe(컴파일 시 Type Check) 개념이 Generics을 사용할 때 중요하다.

- Parameter & Argument의 차이를 명확히 아는 것이 중요함.
- https://github.com/tiny2n/Generic

## 5. Advanced Higher-Order Function (곰튀김님)

- Function vs Value
- function stores acts
- General Async Function

## 6. ARKit (라이언님)

- https://github.com/tokijh/ARVideoPlayer