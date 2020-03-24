

### BootStrap Components

- **breadcrumb** - UI UX 원칙
  - 사이트나 웹 앱에서 유저의 위치를 보여주는 부차적인 내비게이션 시스템
  - 유저에게 '맥락 정보'의 소스가 되며, 지금 어디에 있는지? 어디로 갈 수 있는지? 어디로 가야하는지?에 대한 답을 줌
  - 브레드스크럼은 주 내비게이션을 대체 x, 구분하는 기호를 사용함, 디자인의 중심이 되지 않음

- **alert**
  - 깃헙 변경사항 확인 창
  - 새로고침 하면 사라짐
- **horizontal, card**
  - 텀블벅

- **Carousel**

  - 슬라이드가 넘어가는 회전목마 형태, 계속 루핑
  - 자바스크립트가 없으면 동작 x
  - 특정한 시간에 주기를 거쳐 액티브 클래스가 부여됐다가 지워졌다가를 반복, 실시간으로 변함
  - 화살표 역시 CSS로 이루어져있기 때문에 원하는 속성을 추가로 부여하거나 덮어씌우는 형식으로 바꿀 수 있음
  - 네이버 영화

- **form** - 장고 프로젝트에서 활용

- **Modal** - 클릭하는 순간 입력할 수 있는 창이 뜸

  - airbnb

  - Style - display: none; -> display: block;
  - 버튼에는 Eventlistner가 적용된 것

- Carousel과 Modal은 id로 트리거가 있음 - 이거로 이걸 열겠다

  - 때문에 data-target과 id 값이 정확히 일치해야

- 컴포넌트의 이름 기억하기

  - **hamburger** animation - jonsuh.com/hamburgers/ (only CSS)
  - **pagination** - **1** 2 3 ... 15 **>**





### +

- aria-hidden - 웹 접근성 관련
- sr-only - 스크린 리더 온리, 보통 클래스 이름으로 명명
- 부트스트랩에서 클래스명은 바꾸면 x, id는 수정하되 나머지도 바꿔야
- [lorem ipsum](https://www.lipsum.com/)
  - 이미지버전 - [picsum.photos](https://picsum.photos/200/300)

- 웹 접근성은 처음 개발할 때 고려? 아니면 완성 후에 추가?
  - 기획 단계에서부터 접근성까지 꼼꼼히 고려하면 좋겠지만 여의치 않을 때는 개발을 해나가면서 접근성을 디벨롭









### Portfolio Page

- edutak.github.io/portfolio-test/
- 높이를 전체 브라우저 높이로, fixed
  - 100%는 브라우저 전체라기보다는, 100vh가 정확함
- Startbootstrap
  - 부트스트랩 기본 테마, 템플릿
  - templete - resume, creative
  - 다운로드 - 바탕화면으로 옮김 - /resume
  - index.html -> 다른 선언이 없으면 내 사이트에서 바로 보여질 페이지를 의미
    - README.md 와 같이 의미를 함의하는 파일
  - resume_min, resume 차이?
    - 공백 자체에도 크기가 있기 때문에, 3kb -> 4kb, 조금이라도 파일 크기를 줄이기 위해
    - css minifier

- font awesome - css로 로고들을 그려놓은 사이트
- 이미지가 아닌 i 태그의 사용 이유?
  - i 태그이기 때문에 스타일링이 가능 - 색 바꾸기 등
- 배포
  - githubpages
  - username.github.io로 저장소 만듦 - index.html - 포트폴리오
  - 기술블로그를 githubpages로 이전해보기 - jekyll(ruby), gatsby(react), hexo(vue) (Markdown -> HTML/CSS)
- clone coding 시도해보기

- Materialize
  - 구글의 FE framework









### Grid system

- div class="container", "container-fluid"
  - container는 컨텐츠를 감싸는 wrapping 요소, 그리드 시스템의 필수 요소
  - .container - fixed width container로서 responsive fixed layout을 제공
    - 미디어쿼리에 의해 반응형으로 동작하며, 동일 break point 내에서는 viewport 너비가 늘어나거나 줄어들어도 고정폭을 가짐
  - .container-fluid - full width container로서 fluid layout을 제공
    - viewport 너비에 상관없이 언제나 콘텐츠 요소를 화면에 꽉 차는 너비를 갖게 함
  - padding에 문제가 발생하기 때문에 두 가지 container의 중첩 사용 x

- 12column grid
  - div class="row"의 자식 노드로
  - 12를 기준으로 화면을 균일하게 나눔 (나누기 유연한 값 12, 약수 많음)
    - col3 -> 4개로 균일 비율로 나눔
    - col6 -> 2개로 균일 비율로 나눔
  - 3개를 배치하는 데 1 / 2 / 1
    - col-3 col-6 col-3
- col-6 col-md-4
  - 3개으로 나눠져있다가 -> 화면 크기 줄이면 2개으로 나뉘어짐
  - 화면 크기 픽셀 기준은 Grid options에 따라 (medium = 768px)
  - 예를 들어 768px 이상일 때 3개, 미만에서 2개는
    -  row 4개, 6개 의미
    - 각각의 곱이 12가 됨
- 부트스트랩 grid system 은 container > row 안에 col의 구조로 사용되는 것이라고 이미 작성됨
  - 때문에 row 와 col 을 바꾸는 건 바람직 x
- 브라우저 너비에 따라 break point가 존재함, 
  - 1000px에 4개 요소를 배치
    - col-lg-3을 네개 (large의 break point가 960px이니)
  - Col-sm-1 -> 576px 이상일 때 한 칸의 영역을 가짐
  - Col-6 col-md-4
- .col-, .col-sm-, .col-md-, .col-lg-, .col-xl- 
  - 각종 디바이스에 따른 너비
  - 반응형을 쉽게 구현 가능하도록 도와줌
- gutter란 아이템들 사이 패딩 값
  - gutter 30px - 좌우 padding 15 * 2
  - class="row no-gutters"로 없앨 수 있음
- 위와 같이 반응형으로 조작하고 싶을 때 row로 묶고, 그 위는 항상 container
- 12칸 기준으로 12칸 넘어가면 wrap? 4, 3, 6 이면 4 3 한 줄, 6 한 줄? ㅇㅇ
- 12로 꽉 안차고 남는 경우도 가능? ㅇㅇ 굳이 모두 안채우고도 가능 - Offset
- .vertical alignment가 가능
  - Use flexbox alignment utilities
  - container의 기본 속성이 flex이기 때문에 이것이 가능
  - grid 아닌 flexd의 개념임에 유의
- Reordering
  - Order class를 주는 것도 flex로 구현된 것이기 때문
- Offset
  - Col-md-4 offset-md-4 => 상자 (띄고) 상자
  - 몇 칸을 가져가고 / 몇 칸을 띄울건지를 각각 의미함









### 실제 화면 분석

- row 안 row를 또 만들어 쓰는 방법(이중) 편리함
- 네모의 grouping을 눈여겨보기
  - 위 아래로 두 칸 한 번에 차지하는 것
- grid garden 해보기 - grid 속성 공부











### +

- 사용자 경험에서 스크롤이 아래로 내려가는 것은 거부감이 없어서 height를 위주로 반응형을 고려하지는 않음
  - navbar 같은 경우 너무 크지 않길 원한다 -> vh나 미디어 쿼리를 통해서 적당한 값을 줌
- 모바일 -> 웹 순서로 디자인
- d-none d-sm-block => 화면 작을 땐 작은 글씨 보이지 않도록
- 네이버와 같이 한 화면에 정보가 많은 UX의 경우
  -  특정 너비 이하일 때는 마진을 줄이고 ->  브라우저 크기를 더 줄이면 -> 영역을 숨기는 방식으로 설계
- 이미지 비율을 반응형으로
  - [참조_content/images](https://getbootstrap.com/docs/4.1/content/images/)
- [animate.css](https://daneden.github.io/animate.css/)