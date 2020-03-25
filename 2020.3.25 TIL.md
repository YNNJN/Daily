### Bootstrap Review

- Bootstrap은 HTML, CSS, JS로 구성된 오픈소스 라이브러리임
  - 반응형, 모바일 대응을 위한 FE 컴포넌트
- **Utilities**
  - 박스모델을 기준으로 밖->안
  - position
  - display
  - spacing - margin, padding
  - border
  - color
  - flex
- **Component**
  - alerts - 깃헙
  - badge - 쇼핑몰
  - breadcrumb - home / 여성 / 아우터 / 자켓
  - buttom
  - card
  - carousel - < > 양쪽 끝의 버튼이 아이디로 같이 연결되어야
    - js
  - form / input
  - modal - 배경은 어둡게, 창이 띄워져 focusing 되는
  - navbar
    - js
  - pagination

- **Grid system**
  - 균형감 있는 레이아웃을 구성하기 위한 방법
  - bootstrap에서는 반응형으로 레이아웃을 자유롭게 구성할 수 있음
  - break point
    - .col, .col-sm, .col-md, .col-lg, .col-xl
  - .container
    - bootstrap의 grid system을 사용하려면, 상위에 .container가 존재해야 함
    - .container
    - .container-fluid
  - .row
    - 12개의 컬럼으로 구성
    - .col-{breakpoint}-{number}
  - offset
    - margin-left를 영역만큼 줌









### 미디어쿼리

- 디바이스 크기 별로
- minwidth maxwidth 직접 정의도 가능
- CSS에 바로 넣어주면 됨
- and는 @media에서만 적용 - [참조_MDN 미디어쿼리](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Media_queries)

```css
// Extra small devices (portrait phones, less than 576px)
@media (max-width: 575.98px) { ... }

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) and (max-width: 767.98px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) and (max-width: 991.98px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) and (max-width: 1199.98px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```



```css
// Extra small devices (portrait phones, less than 576px)
// No media query for `xs` since this is the default in Bootstrap

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```









### Goolgle font

- Standard / import

- ```css
  @import url('https://fonts.googleapis.com/css?family=Hi+Melody|Noto+Sans+KR&display=swap');
  h1 {
    font-family: 'Hi Melody', cursive;
  }
  p {
    font-family: 'Noto Sans KR', sans-serif;
  }
  ```

- 다른 브라우저들에서도, 아래의 버전에 해당하는 범위 안에서 가능

  - Google Chrome: version 4.249.4+
  - Mozilla Firefox: version: 3.5+
  - Apple Safari: version 3.1+
  - Opera: version 10.5+
  - Microsoft Internet Explorer: version 6+ ->웬만해선 잘 작동

- 웹 폰트 최적화 방법 찾아보기











### +

- 클래스를 재사용하는 형식으로 작성 권장 

- Bem - 클래스 네임에 일관성이 없다 - 하여 제안됨 
  - 0313 review 폴더 확인
  - 부트스트랩으로 네이밍에 대한 힌트 얻기
- CSS 네이밍 관련 가이드. 네이밍에 절대적인 정답은 없지만 참고
  - BEM: http://getbem.com/
  - 에어비앤비 CSS 스타일 가이드: https://github.com/airbnb/css











### Git

- 분산형 버전관리 시스템(DVCS)
- git status가 가장 중요 명령어 - CLI의 특성 때문
  - GUI(Graphic User Interface)
    - alert, 경고 표시
  - CLI(Command Line Interface)
    - 명령어 전 어떤 시행도 하지 않음
    - 명령 실행 후 결과를 아래에 보여줌

- Post-it

  - git bash에서는 경로부터 보기
  - git init으로 초기화 (저장소 생성)

  ```bash
  ~/Desktop/git
  $ git init
  Initialized empty Git repository in C:/Users/multicampus/Desktop/git/.git/
  ~/Desktop/git (master)
  $ git init
  ```

  - git status

  ```bash
  $ git status
  On branch master
  
  #버전 이력이 없음
  No commits yet
  
  #현재 버전에 등록되어있지 않은 파일
  Untracked files:
  	#커밋될 곳에 포함시키려면(staging area) add 명령어 이용하라
    (use "git add <file>..." to include in what will be committed)
          a.txt
  
  #커밋할 것 없고, 다만 새로 생긴 파일은 있음
  nothing added to commit but untracked files present (use "git add" to track)
  ```

  - git add

  ```bash
  $ git add .
  $ git status
  On branch master
  
  No commits yet
  
  #커밋될 변경사항
  Changes to be committed:
  	#unstage하려면 아래의 명령어를 이용하라
    (use "git rm --cached <file>..." to unstage)
          #새로운 파일
          new file:   a.txt
  ```

  - git commit

  ```bash
  $ git commit -m 'Init'
  [master (root-commit) ebd83a4] Init
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 a.txt
   
  $ git status
  On branch master
  #커밋할 것 없고 작업 공간도 깨끗함
  nothing to commit, working tree clean
  
  $ git log --oneline
  ebd83a4 (HEAD -> master) Init
  ```

- Clone 명령어는 pull의 역할 아닌 init의 역할임

  - 로컬에서 저장소를 초기화하는 방법
    - git init - 특정 폴더를 저장소로 활용
    - git clone - 특정 원격저장소를 복제

