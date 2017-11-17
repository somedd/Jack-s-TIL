DAY5
====
2017/10/20
----------
# TIL
## UNIX 명령어 배우기
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. GUI(graphic user interface)
2. kernal(알맹이, 운영체제의 핵심) <-> shell
3. directory
(1) root directory : 최상위 디렉토리
(2) . : 현재 디렉토리
(3) .. : 부모 디렉토리
(4) ../.. : 2번 위로
(5) ~ : 홈 디렉토리
4. 절대경로& 상대경로
(1) 절대경로 : /로 시작하며, 모두 타이핑해서 입력한다.
(2) 상대경로 : /가 없이 시작하며, 현대디렉토리 하위로 이동한다.
5. r/w/e
(1) r : read (4)
(2) w : write (2)
(3) x : execute (1)
6. 명령어
(1) mv : 파일을 옮기거나 이름바꾸기로 사용가능
(2) rmdir : 디렉토리를 지운다. but, 비어있을 떄(empty)만 가능하다.
(3) rm : 파일 삭제 *rm -rf dir : 강제삭제(위험)
(4) pbcopy : 클립보드에 복사하기
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
## Git & Github의 기초사용법
### Git
~~~~~~~~~~~~~~~~~~~~~~~~
1. Git은 vcs(형상관리시스템)이다.
2. 로컬저장소(commit)와 원격저장소(push)가 있다.
   *우리가 하는 코딩은 .git을 안건드리는데 commit이 저장소를 건드린다.(로컬저장소 = .git)
2. 주요 명령어
(1) push : 서버에 올리는 명령어
(2) commit : 로컬저장소에 저장하는 명령어
(3) clone :  원격저장소 -> 로컬저장소로 동기화하는 명령어
(4) pull : 원격저장소 기반 로컬저장소를 동기화해주는 명령어
(5) add : stage위로 올리는 명렁어
(6) checkout : 끌어오는 명령어
~~~~~~~~~~~~~~~~~~~~~~~~
#### Git's Tip
~~~~~~~~~~~~~~~~~~~~~~~~
1. 옵션에서 -는 하나의 스펠링, --는 하나의 단어가 붙는다.
2. master가 가장 완벽하고 깨끗한 버전으로 사용함.
3. brach(나누는 것.) <=> merge(합치는 것.)
4. 
~~~~~~~~~~~~~~~~~~~
somed@JACK MINGW64 ~/proj/jack-s-TIL (master)
$ git log --oneline --graph --decorate --all
* 7854cc0 (HEAD -> master, origin/master, origin/HEAD) add kkkk in text.txt
* 7b6feaf First commit
* 987c606 Initial commit
여기서 origin은 원격저장소를 말하는 것임.
~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~~~~~~
#### 심화지식
~~~~~~~~~~~~~~~~~~~~~~~~~~
1. git에서 commit만 객체(object)이다. 그 외에는 모두 참조(reference)이다.
2. branch는 객체의 참조일 뿐이다. / branch = 객체의 참조, commit의 별명일 뿐임.
3. HEAD = 가장 마지막 commit의 참조임 
  *HEAD가 가리키고 있는 곳에서 객체를 새로 만드는 것이 commit이다. 즉 갱신임.
4. tag는 그냥 참조다. 움직이지 않음.
5. 작업하는 방식의 종류
(1) git flow
(2) github flow
(3) gitlab flow
6. merge는 두 개를 합쳐 새로운 commit을 만든다.
   *rebase는 두 개의 차이점을 드러내서 대상에게 통채로 얹어버린다.
7. 이해를 위한 사이트 : https://learngitbranching.js.org/
~~~~~~~~~~~~~~~~~~~~~~~~~~

