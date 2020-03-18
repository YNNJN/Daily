### HTML

- HTML이 무엇인지, 지금까지 어떠한 흐름을 거치며 HTML5가 되었는지, HTML5의 설계 원칙, 중요한 특징, Browser 지원 현황, 웹표준(접근성, Semantic), content 모델에 따른 분류, API 사이트와 유용한 Tutorial 사이트들

---



- 브라우저 전쟁
- 브라우저가 파편화되어있었고, 통합되는 과정에서 표준이 생겨남
- 자스는 에크마 스크립트를 표준으로 하여
- 과거 버전의 레거시 코드들이 낯설게 와닿을 수 있음
- HTML은 문서의 구조를 잡음 - 마크업
- 5로 넘어오면서 시맨틱 태그 생김 - 문서에서의 역할에 대한 의미를 담고있음
- 각각의 태그들이 어떤 목적과 의미를 가지고있는지 정리









### CSS

- CSS의 기본 개념, Cascading order, inheritance, CSS 발전 흐름, Module별 분류, Browser support, Vendor prefix, IE 버젼별 조건부주석, 렌더링모드 지정, CSS 박스모델, Selector, DOM과 DOM으로 할 수 있는 일들

---



- 선택자 관련 개념들 (우선순위)
- 어디를 스타일링 하겠다-가 필요 -> 선택자 개념
- 폭포수처럼 하나씩 적용되는데, 그에 대한 우선순위가 있었음
- 단위는 px, rem, em 등 다양한 형식의 단위들이 있었음
- 각각의 요소는 네모네모
- block, inline 요소로 보여짐

- position, float 위치
  - absolute, fixed, ...
  - 신문의 레이아웃 - float로, 이미지를 왼쪽으로 띄우는 형식으로 구현









### JavaScript

- Javascript 흐름, 동적 데이터 타입(Dynamic typing), 연산자, 객체, 배열, 동적 파라미터, Script 선언위치
- function의 기본 개념, 호출 패턴에 따라 달라지는 this, 상속을 가능하게 해 주는 prototype, 다른 언어와 다른 유효 범위 scope
- Javascript module화와 함수형 프로그래밍을 가능하게 해 주는 Closure, Prototype을 이용하여 객체지향(OOP)을 구현하는 방법

---



- 이러한 문서들의 조작은 자바스크립트가 함
- 데이터 타입은 원시 타입(undefined, null도 포함)과 객체 타입
- 객체 선언 및 활용
- 배열, 순회 (for in은 주의하여 활용)
- 함수 정의(화살표 함수, 클로저) - 문법 눈에 익히기
- 이벤트, DOM 조작(Core Javascript가 아닌)
  - 브라우저에서 발생하는 일들이 이벤트를 통해 정의됨
  - 돔 조작에서는 쿼리 셀렉터,쿼리 셀렉터 올을 기억
  - createElements(), 요소 추가

