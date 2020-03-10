- CSS: Cascading Style Sheets의 약자로 HTML 문서에 외형을 정의하기 위한 스타일 단어
- 선택자: CSS 스타일 적용을 위해 HTML 문서 내의 단일 요소 또는 요소들을 선택하는 구문 규칙
- 의사 클래스: 요소의 기본 상태와는 무관하게 링크, 동적, 구조적 상태를 이용하는 선택자의 일부









### 1. CSS 문서표현 1

- Cascading Style Sheets

- HTML 문서 요소에 스타일 적용 위해 사용
  - [HTML 요소 참고서](https://developer.mozilla.org/ko/docs/Web/HTML/Element)
  - [콘텐츠 카테고리](https://developer.mozilla.org/ko/docs/Web/Guide/HTML/Content_categories)
- 디자인 정의, 관리, 재활용에 용이한 장점
- CSS는 스타일 언어, HTML 이외에 다른 프로그래밍 언어와 사용 가능함









#### 작동 방법

- HTML(문서구조정의) + CSS(문서 외형 정의) -> 짝을 이루어 사용

- CSS 작성 방법은 다음과 같음

  - HTML 요소에 직접 CSS 정의: HTML 요소에 **스타일 속성** 이용 (내부참조)

    - 동일 요소 공통 적용 불가
    - 수정 및 변경시 모든 HTML 코드 검토
    - 체계적 관리와 변경 불가능

  - CSS를 모아서 정의: HTML **헤더 부분에 style 요소** 사용 (내부참조)

    - CSS 코드가 위치한 HTML 파일에만 적용되므로
    - 전체 수정 시 모든 HTML 파일 수정해야
    - style요소에는 type, media가 있음

  - 따라서 **CSS 파일 만들어 HTML에 연결** (권장) (외부참조)

    - HTML이 서버에서 웹 브라우저로 로드될 때 CSS 파일도 같이 로드

    - 1. HTML 코드 작성

      2. 빈 파일을 .css 확장자로 저장

      3. CSS 파일 경로 지정 - HTML 코드 head 부분에 link요소 사용

         - 외부 리소스를 HYML 문서와 연결하는 link요소는 리소스의 관계를 나타내는 rel 속성, 리소스의 위치를 지정하는 href 속성이 필수

         	- link rel="stylesheet" (CSS 파일 연결)
         	- href="css/style.css" (연결하고자 하는 리소스 파일 경로 지정)
         	- 하나의 HTML 파일에 여러 개의 link 요소 사용하여 각기 다른 여러 CSS 파일 링크 가능

      4. CSS 작성, HTML 파일 열어 적용되는 과정 확인하면서 작성

- 텍스트 크기 및 스타일, 레이아웃, 섹션 요소의 크기, 테두리, 배경색 또는 이미지, 화면 전환이나 요소들의 움직임까지 CSS에서 정의 가능

- 구조적으로 잘 설계된 CSS는 CSS 파일 내부에서 다른 CSS 파일을 불러오기도 함











#### 기술 방식

(기초 선택자, 고급 선택자 위주로 정리)

(되는 것 vs 하면 안 되는 것 정리)



- 셀렉터 {속성 선언}
- 셀렉터{선언(프로퍼티:값); 선언(프로퍼티:값);}

- 크롤링 시 개발자 도구 - copy - copy selector 했던 그 selector!
  - #sect1 > ul > li:nth-child(1)
  - id            ul태그    li중 첫번째
  - id는 문서에서 한 번만 등장 가능

- 특정 요소를 선택하여 스타일링하기 위해
  - h1{font-size: 1.5em;}
  - 선택자란 HTML의 '어떤 요소'에 속성들이 적용되는지 정의함
    - 다양한 요소 명, 클래스, ID 또는 복잡한 논리형 등으로 다양
  - 속성 선언이란 선택자를 통해 선택된 HTML 요소에 적용할 스타일 속성 내용
    - 속성(정의하는 스타일의 내용)과 값(키워드, 단위가 있는 수치)으로 구성됨
- 모든 형태를 박스 형태로 보고, 너비와 높이를 정의할 수 있음











#### 타입, 고급 속성

- 타입 선택자
  - HTML 요소 명, 요소의 클래스 속성 값, ID 값
    - **HTML 선택자**
  - 특정 요소에 CSS 속성 적용 위해서는 클래스 선택자(.), ID 선택자(#) 이용
    - **클래스 선택자**는 요소들을 원하는 그룹으로 묶음, 동일한 클래스 값을 가지는 모든 요소에 적용
      - 스타일 적용을 위한 그룹으로 생각하면 됨
    - **ID 선택자**는 HTML ID 속성 값에 CSS를 적용, 문서 내의 같은 ID를 가진 유일한 요소에 적용
  - 여러 요소에 동일한 CSS 스타일 적용 위해 클래스 속성 이용할 수 있지만
    - 이미 클래스 속성 적용한 경우 스타일 그룹 위해 클래스 속성 지정 불가
    - 따라서 그룹 지정형식(,) 사용
      - 이 방법은 추후 고급 선택자, 의사 클래스에도 동일하게 적용됨
- 고급 선택자
  - HTML 문서 요소들을 계층 관계를 이용하여 선택하는 선택자
  - 자손(>)은 하위 계층 내부에 중첩되는 계층은 신경쓰지 x
    - 따라서 직계 자손 요소 개념을 사용
  - 형제 요소는 일반(~) / 인접(+) 형제 요소(바로 아래 있는 형제 요소)로 구분됨











#### 의사 클래스

- 개발자가 직접 지정 안 한 가짜 클래스, 클래스의 특징을 가짐
- HTML 요소 선택의 범위를 넓힘
- : 의사 클래스 명
  - 선택자 뒤에 붙어 선택자의 상태를 기준으로 선택
  - :link - 한 번도 클릭하지 않은 링크 (히스토리에 없는 링크 상태 의미)
  - :visited - 보라색 방문 체크
  - Text-decoration: none; - 링크에 밑줄 표시 사라짐
- 동적 의사 클래스
  - 마우스와 커서에 관한 상태를 의사 클래스로 나타냄
  - :active - 마우스로 클릭했을 때의 상태 의미
    #IE에서 active 의사 클래스가 tr 요소에 잘 적용 x -> :hover 적용
  - :hover - 마우스 커서가 올라간 상태 의미
  - => 링크 뿐 아니라 대부분의 요소에 적용 가능, HTML과 CSS만으로 동적 페이지 제작
  - :focus - 서식 폼과 같은 요소에 마우스 위치하여 입력 또는 선택 상황 의미 (요소가 포커스를 가짐)
- 구조적 의사 클래스
  - HTML 구조에 따른 의사 클래스, 형제와 자손 그리고 몇 번째 요소인지로 상태를 구분함
  - :root - 문서의 최상위 요소 의미, 단독으로 사용
  - :empty - 비어있는 요소 의미    #<p></p>와 같이
  - :only-child: 형제가 없는 요소, 자신이 속한 부모 요소의 유일한 자손 요소
  - :only-of-type: 같은 타입의 형제가 없을 때 사용
  - :first-child, :last-child
  - :nth-of-type(n), :nth-last-of-type(n)
  - :first-oftype, :last-of-type
- 기타 의사 클래스
  - :lang() - 지정한 언어 속성을 가지는 요소
  - :not() - 부정을 의미, 괄호 안에 클래스 등의 다양한 선택자 지정 가능 (논리 의사 클래스)
- 의사 엘리먼트
  - 기존 요소에 추가로 새로운 요소를 정의함으로써 독립된 스타일 적용 가능
  - :first-letter, :first-line, :after, :before











#### 속성 선택자

- 선택자[속성="속성값"]
- 속성과 속성 값 선택자는 속성 값이 정확히 일치하는 요소를 선택함
  - [속성="속성값"] 형태로 하이퍼 링크 속성이 외부 URL의 형태를 가진 요소를 선택하는 것은 어려움
    - 이 경우 등식을 통해 원하는 선택을 함
    - a[href^="http://"]{color: pink;} - 하이퍼링크 속성 값이 "http://"로 시작하는 a 요소 선택
- 미디어 쿼리
  - 현재 HTML 문서가 보여지는 화면이 어떤 것인지 파악
  - 미디어 쿼리 구문: link 요소에 속성으로 적용
    - 미디어 쿼리 값 + 미디어 쿼리 속성값











#### 상속

- 속성 중에는 상속이 되는 것과 되지 않는 것이 있음 (모두 상속되는 것 x)
  - 상속되는 것
    - text 관련 요소(font, color, text-align), 스타일링 관련 요소(opacity, visibility)
  - 상속 되지 않는 것
    - Box model 관련(width, height, margin, padding, border, box-sizing, display)
    - Position 관련(position, top/right/bottom/left, z-index)
  - 각 태그들에 대한 상속 여부는 MDN 문서에서 확인 [MDN margin](https://developer.mozilla.org/ko/docs/Web/CSS/margin)

- 우선순위를 아래와 같이 그룹을 지을 수 있음
  - 중요도(금)
    - !important
  - 선택자 우선순위(은)
    - 인라인 / id 선택자 / class 선택자 / 요소 선택자
  - 소스코드 순서(동)
    - 나중에 정의된 것이 더 우선순위를 가짐













#### CSS를 사용하여 확장자를 감지해서 태그를 자동으로 붙게 하는 방법

- 속성 선택자와 의사 엘리먼트를 적절히 사용해야
- 이는 CSS 작성 중 특정 요소를 선택하기가 까다로운 경우에 속함
- 스크립트에서 작성해야할 것 같은 자동화된 스타일을 작성하기 위해서는 다양한 선택자 조합해야
  - li요소 직계 자식인 a 요소의 속성을 검사
  - a 요소의 href 속성이 '.doc', '.pdf', '.xls' 파일 확장자인지 확인하여 선택
  - 그런 다음 :after 의사 엘리먼트를 이용하여 선택자에 따른 표식을 뒤에 붙임
  - 파일 확장자마다 스타일 설정을 해야















- Box model: 웹의 모든 요소가 적용되는 모델로 모든 요소가 상자와 같은 사각형 영역으로 표현되는 모델
- Positioning: position 속성으로 요소의 위치 속성을 상대 위치 또는 절대 위치 등으로 나타내는 것
- 마진 겹침 현상: 상하 마진이 연속될 때 큰 수치의 마진으로 겹쳐 마진이 의도와 다르게 넓게 작용되는 것을 막아주는 현상











### 2. CSS 문서표현 2





#### 단위

- px, %, em, rem, viewport 기준단위
- em: 요소에 지정된 사이즈에 상대적 사이즈를 가짐 (배수)
- rem: 최상위 요소(HTML)의 사이즈를 기준으로 배수 단위를 가짐 (root em, root 기준)
- viewport 기준 단위 - vw, vh, vmin, vmax [caniuse_viewport](https://caniuse.com/#search=viewport)



(실습)

- 기본적, 브라우저 픽셀은 16px
- 16 * 1.5 = 24px (rem) - 어디에 적용해도 같은 값
- 24 * 1.5 = 36px (em) - 자기가 가질 수 있는 값의 배수를 가짐











### CSS 박스 모델

- CSS 지탱하는 모든 요소들이 가진 특성
- HTML 문서 body 부분의 모든 요소가 사각형 영역을 가지고 있음 - 레이아웃과 디자인에 영향
- 박스들의 위치와 상관관계 지정하는 방식을 정의함









#### 구성

- content - 실제 내용이 위치
- Padding - 테두리 안쪽의 내부 여백, 요소에 적용된 배경의 컬러, 이미지는 패딩까지 적용
- border - 테두리 영역
- Margin - 테두리 바깥의 외부 여백, 배경색 지정 불가

![css_box_model_chrome](/Users/myung/Desktop/웹/css_box_model_chrome.png)

- 사방에 적용할 때 - 줄여 쓸 수 있다
- shorthand를 통해 표현 가능

![스크린샷 2020-03-10 오전 11.45.12](/Users/myung/Desktop/웹/스크린샷 2020-03-10 오전 11.45.12.png)



- border도 같은 방식으로 shorthand를 통해 표현 가능
- 웹브라우저마다 기본 margin과 padding 설정 존재
  - -> 새로운 스타일 적용시 혼란 야기 가능
  - -> 초기화해야
    - Margin: 0;
    - padding: 0;









#### box-sizing

- CSS에 기본으로 정의된  모든 요소의 box-sizing은 content box
  - padding을 제외한 순수 contents 영역만을 box로 지정함
- 그런데 인간이 영역 구분할 때 보통 border까지의 너비를 기준으로 함
  - 따라서 box-sizing을 border-box로 지정
  - box-sizing: border-box;
- 정확한 요소의 크기: width와 height로 정한 값 + padding 값, border의 굵기 값 + margin 값











#### margin Collapse

- 마진 상쇄, 마진 탑과 바텀을 1rem, 3rem 줬을 때 

- 인접 형제 요소간 top bottom이 함께 정의되는 경우 margin이 겹쳐서 보임



<img src="/Users/myung/Desktop/웹/Margin Collapse.png" alt="Margin Collapse" style="zoom:50%;" />

이미지 출처 [CSS Layout](https://fr.slideserve.com/teal/an-introduction-to-cascading-style-sheets-css-layout-and-the-css-box-model-powerpoint-ppt-presentation)











#### display 속성

- 인라인 / 블록레벨 요소 (HTML4.1까지) - 디스플레이 값이 어떻게 정의되어있는지에 따라
  - 대표적 블록레벨 요소
    - Div / ul, ol, li / p / hr / form
  - 대표적 인라인 레벨 요소
    - Span / a / img / input / ...

- display: block
  - 줄바꿈이 일어나는 요소
  - 화면 크기 전체의 가로폭을 차지함
  - 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
- display: inline
  - 줄바꿈이 일어나지 않는 행의 일부 요소
  - content 너비만큼 가로 폭을 차지함
  - width, height, margin-top, margin-bottom을 지정할 수 있음
  - 상하여백은 line-height로 지정함
- display: inline-block
  - block과 inline 레벨 요소의 특징을 모두 가짐
  - inline처럼 한 줄에 표시 가능하며
  - block처럼 width, height, margin 속성을 지정할 수 있음









#### margin auto

- 블록은 기본적으로 화면 너비의 100%를 가짐
  - -> 가질 수 없다면(사용자가 일정 크기만 지정, 가질 수 있는 것보다 작게 지정했을 때
  -  -> 나머지를 margin으로 자동으로 줌
- 인라인은 컨텐츠 영역만큼만 가짐

- 따라서 블록과 인라인의 속성에 따른 수평 정렬이 다르게 됨
  - 즉 블록의 경우 margin right: auto, margin left: auto로 가운데 정렬이 된 것 처럼 보일 수 있음
  - 인라인의 경우 text-align: center

| block                                        | inline        | inline              |
| -------------------------------------------- | ------------- | ------------------- |
| margin-right: auto;                          | ■□□□□□□□□□□□□ | text-align: left;   |
| margin-left: auto;                           | □□□□□□□□□□□□■ | text-align: right;  |
| margin- right: auto;<br />margin-left: auto; | □□□□□□■□□□□□□ | text-aling: center; |

- 박스모델에서도 parameter가 세 개인 경우, 좌우를 동시에 지정하는 것이 일반적이기 때문에
  - 세 번째 그림에서 두 번째 변수 20px은 자동설정된 좌우 마진 값











#### 서체

(텍스트, 컬러, 배경, 목록 위주로 정리)

- 서체 지정과 텍스트 설정
  - Font-family
    - :font-family: (사용할 서체), (대안 서체1), (대안 서체2)
- 서체 크기 조절
  - Font-size
  - 서체 크기 단위 - pt, pc(12pt = 1pc), px, %(부모 요소에 대한 사대적 크기), em(서체의 대문자 크기에 대한 비율), ex(서체의 소문자 크기 비율 - 영문일 경우 정확한 서체 크기를 맞추기 위해 사용) 
- 변형 서체
  - Italic, Bold, Small cap
  - Italic -> font-style 속성 - italic, oblique, normal
  - Bold -> Font-weight 속성- bold, bolder, lighter, 100~900, normal
  - Small cap -> font-variant 속성

- 텍스트 스타일 설정
  - 단어 간격: word-spacing 속성 사용
  - 행간 설정: line-height 속성
  - 텍스트 정렬: text-align 속성 사용
    - 텍스트 정렬은 블록레벨 요소에만 적용됨
    - 세로 정렬은 인라인 요소(상대적 수직 위치)와 테이블 셀(셀 안에서 위치)에만 적용됨
  - 텍스트 인덴트: text-indent









#### 컬러

- 웹 색상 코드
  - 16진수 표현(#4B0082), 10진수 표현(rgb(255, 0, 0)), HSL 표현, 색상 키워드(영어 색 이름 미리 지정)
- 투명도 설정
  - 10진수 색상 코드에만 적용 가능
- 텍스트 색 설정
- 배경 설정
  - 크기, 배경 색, 이미지 설정 가능
  - 배경 색: back-ground-color 속성
  - 이미지: back-ground-image 속성
  - 반복: background-repeat 속성
  - 고정: background-attachment 속성 - fixed, scroll









#### 목록과 표

- 블릿 - list-style-type 속성 이용
  - 순서가 있는 목록 형태
    - decimal, decimal-leading-zero
    - upper-alpha, lower-alpha
    - Upper-roman, lower-roman
  - 순서가 없는 목록 형태
    - disc(까만), circle(빈), square
  - 블릿이 없는 목록 - 네비게이션 만들 때 유용
    - List-style-type: none;
- margin과 padding
- border 설정(테두리 선 설정)
  - border-width, border-style, border-color
  - table{1px solid black;} 으로 축약해서 제시 가능
- 셀 padding 설정 - 셀의 여백 조절
  - 셀에 margin 설정은 적용 안 됨
- 빈 셀 감추기 - empty cells 속성 <table>에 적용 - hide, show
  - border-collapse 속성이 collapse로 설정되어 있으면, empty-cells 속성이 적용되지 않음
  - => 반드시 셀 여백이 있는 표에만 적용됨
- caption 위치와 정렬 - caption-side 속성