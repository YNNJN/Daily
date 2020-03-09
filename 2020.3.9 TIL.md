- W3C: World Wide Web Consortium의 약자로, 웹 표준을 개발하고 논의하며 제정하는 조직
- DOCTYPE: HTML의 문서형식 선언으로, HTML 및 마크업 언어의 DTD 또는 버전을 명시함
- Metadata: 문서 또는 파일에 관한 정보를 제공하는 내부 데이터











### 1. HTML5의 이해



#### HTML이란

- Hyper Text Markup Language

  - Hyper text : 각 문서 내부마다 다른 문서에 연결되는 링크를 가지고있는 형태
  - Hyper text를 주고받는 규칙: HTTP(Hyper Text Transfer Protocol)
  - Markup: 큰 제목, 문단 등 문서의 구조를 잡는 작업
  - Language: 그것을 지원
  - 즉 문서의 구조를 잡기 위한 언어

  

  - 연산기능 없음
  - 콘텐츠 성격 표시만
  - 웹 용 콘텐츠(글과 그림)의 구조를 지정하는 컴퓨터 언어
  - 웹 서버에 저장되어 웹 브라우전의 요구에 따라 불려짐
  - 웹 브라우저에 불려진 HTML은 클라이언트의 웹 브라우저에 의해 해석되어 내용이 화면에 보여짐











#### 역사

- 1차 웹 브라우저 전쟁 (Netscape vs Internet Explorer)
  - 웹브라우저 간의 호환성 결여, 즉 같은 기능도 다른 HTML, CSS 표현을 사용함
  - 이미지 참고_wikipedia(browser wars)
- 2차 웹 브라우저 전쟁
  - 오픈 소스화된 Netscape -> 파이어폭스, 오페라.. 등장
  - Internet Explorer도 웹 표준 준수하겠다는 선언 이끌어냄
- W3C의 HTML3.2권고(1997) -> XHTML권고(2000) -> HTML5권고(2014)
  - HTML3.2는 HTML 사용법을 수용한 타협안
  - XHTML은 XML의 엄격함을 주요 내용으로 하는 웹 표준
  - HTML5는 웹 어플리케이션 개발 API를 다수 포함

- 최근

  1. 웹 기반 사업과 기술의 발전에 따라 HTML의 한계 극복

     - Ajax: 자스 이용하여 웹 서버와 동기화 된 웹의 한계 극복

     - Web2.0, 미디어의 일반적인 사용, 모바일 디바이스, 웹 어플리케이션 등장

  2. 동적인 웹을 위한 표준화된 기술 요구

  3. 웹 관련 업체들(WHATWG)이 자체적으로 워킹 그룹을 만듦 (Apple, Google, Microsoft, Mozilla)
     - HTML5 명세서 작업 - W3C 인정, HTML5 초안 발표 - XHTML2 개발 중단, HTML5에 집중
  4. 대-통합

- 누가누가 표준을 잘 지키나 [html5test](http://html5test.com/results/desktop.html) -> 웹 표준을 잘 지키고 있는 크롬

- [caniuse](caniuse.com) - 지원 가능한 브라우저 검색 - semantic

- HTML5의 의미 - 실용적 설계, 실용적 설계, 표현과 내용의 완벽한 분리, 플러그인 없이 미디어 처리 및 동적 작동, 최신 웹 기술(지오로케이션, 웹 소켓, 웹 스토리지, 웹 워커) 수용











#### 시작하기

- 텍스트 에디터 준비
  - 메모장과 같은 단순 텍스트 에디터에서도 가능하지만
  - HTML, CSS, javascript... 사용 권장
  - Notepad++, Kmodo Edit, Aptana Studio3(이클립스 기반, 코딩, 디버깅, 프리뷰 지원)
  - Visual Studio Code (네모네모에서 html css, snippets, open in browser, auto rename tag, auto close tag install)
  - fiddle로 질문 보내기
  - 크롬 개발자 도구 - 우클릭 - 검사
- DOCTYPE 지정
  - 웹브라우저가 정확히 HTML 표현하기 위해 html버전 명시
  - 꺽쇠 안 !DOCTYPE html 표시
- HTML 작성 규칙
  - 요소: HTML의 마크업 명령어, 콘텐츠의 구조를 정의함(요소가 영향력을 미치는 콘텐츠의 범위가 중요)
    - 콘텐츠 + html 요소(요소를 꺽쇠로 둘러쌈, 태그)
    - 대소문자 구분 x
    - 마침 태그 없이 단독으로 사용되는 요소 = 빈 요소 (self closing)
      - br(줄바꿈), img(이미지)
    - 요소의 속성 기술: 요소명 뒤에 공백을 하나 두고 속성명 = "속성값" 형식으로 기술
- head - body 처리 전, 처리되어야 하는 설정 부분
  - html 파일의 메타데이터 스크립트와 css 등이 위치
  - 타이틀, 기타 설정
- body - 콘텐츠가 담기는 곳



<img src="/Users/myung/Desktop/1200px-DOM-model.svg.png" alt="Dom tree" style="zoom:40%;" />



이미지 출처 [wikipedia](https://en.wikipedia.org/wi…)











#### HEAD 설정

- 웹브라우저에는 표시되지 않지만 중요 설정 내용 담음

- HEAD에 위치하는 요소

  - 타이틀 지정: HTML 파일의 제목으로, 웹브라우저 타이틀 바에도 나타남

  - 문자 인코딩: 텍스트 에디터의 문자 인코딩 설정 = HTML 헤더 부분에 설정한 문자 인코딩

  - 메타요소: 메타데이터(파일에 대한 정보 가진 데이터) 정의하는 부분

    - 문자 인코딩, 설명, 키워드, 작성자, 저작권, 연락처, 작성일을 작성
    - 구글 등 검색 로봇에 의해 수집되는 정보이므로 필요
    - 마침 요소가 필요없는 단독 요소임
      - meta charset = "UTF-8"
      - meta name = "description" content = " "
      - meta name = "keywords" content = " "
      - meta name = "author" content = " "
      - meta name = "copyright" content = " "
      - meta name = "reply-to" content = " " (연락처 메일 입력)
      - meta name = "date" content = " " (국제시간으로 입력)

  - [Open Graph Protocol](https://ogp.me/): 메타정보에 해당하는 제목, 설명 등을 쓸 수 있도록 정의 property="og.."

    - 카톡에 링크 보냈을 때 보이는 썸네일에 대한 규약
    - head 태그 사이에 작성
    - 페이스북이 만듦

  - 웹 사이트 분석해보기

    - 크롬 웹스토어에서 Web Developer 설치
    - information tap - view document outline

  - 외부 파일 연결

    - 웹페이지는 HTML, CSS, Javascript 3가지로 이루어짐

    - 유지보수를 위해 다른 파일로 분리

    - CSS, Javasciprt를 HTML 파일에 연결하는 방법 (링크요소 이용)

      - link rel = "stylesheet" href = "css/style.css"
      - script src = "js/script.js"

      

    <img src="/Users/myung/Desktop/스크린샷 2020-03-09 오후 1.19.16.png" alt="HITML과 연결" style="zoom:30%;" />













#### 기존의 HTML과 달라진 meta요소와 Empty요소

- 지금까지의 HTML 요소와 다르게 meta요소가 시작 요소만을 가지고, 맺음 요소는 존재 x
- 기존 HTML 요소가 웹브라우저에 해당 콘텐츠가 어떤 구조와 의미를 갖는지 알려주는 역할이었다면, meta요소는 웹 브라우저에게 문서정보를 알려주는 역할
- 일반적 HTML 요소가 내용을 감싸는 형식이라면 meta 요소는 속성과 속성 값의 정보를 담고있을 뿐 내용을 감싸는 것 x, 따라서 내용을 가지고 있지 않은 요소,  즉 Empty요소라고 부름
- 이러한 Empty 요소에는 omg, area, br, hr, input이 있음











### 2. 문서 구조화 1



#### 마크업언어

- 구조적 마크업
  - 문서의 구조 정의
  - 콘텐츠의 의미 또는 역할
  - 콘텐츠의 종속 관계
- 표현적 마크업 (예전 HTML모델, 현재는 개발 x)
  - 문서의 외형 정의
  - 문서 레이아웃
  - 콘텐츠 디자인
- 초창기에는 구조적 & 표현적 마크업을 혼용 -> 디자인 요구 늘어나 -> 한계
- 혼재할 시 문제점
  - 웹 접근성 저해, 더 높은 유지 비용 발생, 문서 크기 비대화

- 현재 - HTML은 문서 구조만 정의, CSS는 문서 레이아웃과 디자인 정의











#### HTML 요소

- 인라인 / 블록 요소 (디스플레이 속성)
  - 인라인 - span, img -> 같은 줄에 표현됨
    - 강조, 링크, 이미지
  - 블록 - 한 줄 한 줄
    - 제목, 문단, 인용문











#### 섹션 요소

- 섹션이란 의미가 연결되는 콘텐츠의 집합

- 자체적으로 제목과 내용 가질 수 있는 독립적 콘텐츠 단위

- 기존엔 div 요소에 아이디, 클래스 속성 적용하여 섹션 분리 -> HTML5에서는 자주 사용하는 섹션을 추려 새로운 요소로 추가함

  - 추가된 섹션 요소 - 시맨틱 태그

    - 컨텐츠의 의미를 설명하는 태그
    - 실제 동작은 div와 같지만, 마크업 시 html 코드 상에서 의미를 담아보자는 시도(개발자 도구에서 확인 가능)
    - HTML5에 새롭게 추가된 시맨틱 태그 - header, nav, aside, section, article, footer

    - 개발자와 사용자 뿐만 아니라 검색 엔진에 의미 있는 정보의 그룹을 태그로 표현
    - 단순히 구역을 나누는 것(non semantic 요소: div, span 등) 뿐만 아니라 의미를 가지는 태그 사용 지향





<img src="/Users/myung/Desktop/html5 structure.png" alt="html5 structure" style="zoom:70%;" />



이미지 출처 [Openclassrooms](https://openclassrooms.com/en/courses/2479876-build-your-website-with-html5-and-css3/2491630-structuring-your-page)











#### 그룹 콘텐츠 요소

- 그룹으로 내용을 분리하는 블록 레벨 요소를 의미, 즉 마크다운 문법이 html에서 어떻게 표현되는지
- 기존의 HTML 요소가 대부분, 역할을 정의
  - p, hr, ol, ul, pre, blockquote, figure, div







#### 텍스트 관련 요소

- a, b vs **strong**, i vs **em**, span, br, img







- 접근성, 검색엔진 최적화에 중점 두어 HTML 공부할 것

- [MDN web docs](https://developer.mozilla.org/ko/docs/Web/HTML/Element)가 가장 좋은 책, 사전처럼 참고할 것