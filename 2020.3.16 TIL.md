### summary

- 돔을 조작할 수 있는 메서드들이 있다. 도큐먼트를 기준으로 혹은 요소를 기준으로
- 돔을 하나 선택해서 가져오고 싶을 때 쿼리 셀렉터, 쿼리셀렉터 올 중 택해서 사용
- 클래스네임, 혹은 태그네임으로 선택할 경우, live collection이기 때문에 조작 과정에서 내가 원하는 만큼의 조건문과 반복문 수행이 안 될 수 있기 때문













- **window 객체**

  - 전역객체임
  - 다양한 함수, 이름 공간, 객체 등이 포함
  - var에 지정한 것이, window에서 접근 가능
  - 개발자 도구 - window - 메서드 등의 정보 살펴볼 수 있음

- **DOM 접근**

  - 단일 Node
    - document.getElementByID(id)
      - id 값은 한 번만 지정 가능하니 무조건 하나의 단일 노드를 리턴
    - **document.querySelector(selector)**

  - 아래의 나머지는 하나임이 보장되지 않으니, 배열 형태로 리턴 [Node, ... ] (유사배열 형태)

  - HTMLCollection(live)
    - live collection -> 반복문이나 조건문에 따라 값이 바뀔 때 바뀐 값이 실시간으로 반영됨
      - 인자로 들어가는 값은 #id, .clsss, tagname의 선택자
      - 순회는 NodeList를 기준으로 하자
      - 선택시 querySelector, querySelectorAll만 사용하자
    - document.getElementsByTagName(class)
    - document.getElementsByClassName(class)
  - NodeList(non-live) - 경우에 따라 live collection일 수 있음
    - **document.querySelectorAll(selector)**

- **DOM 조작**

  - 문서의 구조화된 표현을 제공하여, DOM 구조(크롬 창의 탭)에 접근할 수 있는 방법을 제공
  - 구조화된 노드와 오브젝트로 문서를 표현함
  - 주요 객체
    - window: DOM 문서를 표현하는 창, 가장 최상위 객체
    - document: 페이지 콘텐츠의 진입점 역할을 하며, <body> 등 다른 요소들을 포함함
    - navigator, location, history, screen (브라우저 창 조작)
      - history.back() 뒤로가기 누른 것과 같은 효과
  - 노드의 생성과 삽입, 조작
    - document.createElement(tagName): 특정 태그를 생성
    - document.createTextNode(text): 텍스트 노드를 생성
    - parentNode.appendChild(Node): 마지막 자식 요소로 추가
    - parentNode.removeChild(Node): 해당 요소를 제거
    - 하나하나 노드를 생성하기보다는 innerHTML, insertAdjacentHTML 메서드 사용 권장
  - 노드에 CSS 속성 적용
  - innerHTML

  

  











- DOM: 문서 객체 모델의 약자로 객체 지향 모델로써 구조화된 문서인 HTML 문서를 조작하기 위한 API를 표현하는 형식
- DOM level 0: DOM이 만들어지기 이전의 특정 웹브라우저에 종속된 DOM. DOM 표준화 이전에 있던 단계를 말함
- DOM 트리: HTML 문서의 계층 관계를 표현하는 트리 형태의 분석











### DOM

- 클라이언트 측 JavaScript의 핵심
- 웹 브라우저와 웹 문서의 내용 객체화
  - 웹 브라우저와 웹 문서의 기능이나 내용에 접근 + 정보를 얻을 수 있도록
  - 모든 기능과 내용을 객체화한 것
  - 각각의 객체는 프로퍼티로 정보를 읽거나 설정 가능
- 웹 브라우저 창의 위치를 알고 싶다면
  - window 객체의 창의 위치를 알려주면 프로퍼티를 읽어옴
  - 같은 방법으로 웹 문서의 특정 요소를 접근하여 정보를 얻어오거나 수정 가능
- 객체화 -> 구조화 -> 계층으로 구성됨
- 현재 웹 브라우저 윈도우에서
  - Window 객체와 Document 객체의 활용도 높음
  - 웹 문서를 보여주는 창이 DOM의 기준이 되는데,
  - 웹 브라우저가 하나의 웹 문서를 보여주고, 이는 다양한 HTML 요소를 포함하기 때문











#### 윈도우의 크기와 위치 정보

- 웹 브라우저 창의 크기 (브라우저 창의 UI 요소 포함)
  - var windowWidth = window.outerWidth; (Height도 마찬가지)
- 웹 브라우저 창의 크기 (브라우저 창의 UI 요소 제외)
  - var webViewWidth = window.innerWidth; (Height도 마찬가지)
- 이외에 screenX, screenY, pageXOffset, pageYOffset 프로퍼티가 존재











#### 윈도우의 생성

- Window 객체의 open 메서드 사용
- var newWindow = window. open("login/index.html", "Login", "width=500, height=350, menubar=yes, location=yes, resizable=yes, scrollbars=yes, status=yes")
  - "login/index.html"은 새로 생성된 창에서 열 HTML 페이지
  - "Login"은 새로 생성된 창의 이름
    - HTML에서 title로 설정하는 창의 이름과 다름
    - 기존 창의 이름과 비교하여 같은 이름이라면 새로 창을 생성 않고 url만 변경
  - 나머지 인자는 창의 속성 나타냄











#### 새로운 표준 DOM

- HTML 문서의 모든 요소에 접근할 수 있게 하기 위해 문서를 트리로 표현
- 중첩된 요소들은 부모와 자식 관계로 계층화됨
- 웹문서를 구조화하면 요소 사이의 관계로 모든 요소 접근 가능
- 각 요소를 노드 객체라고 부름 (HTML 요소, 도큐멘트, 텍스트, 속성까지 의미)
- 새로운 DOM 표준은 노드를 기준으로 각 노드에 접근하는 방식을 제공함











#### 새로운 방법_노드의 순환

- 주변 노드들에 대한 탐색 가능 - 필요할 때 찾아 쓰기

- 노드 객체의 부모 노드에 접근
  - parentNode 프로퍼티
- DOM 문서 트리 내에 같은 계층에 있는 요소들에게 접근
  - nextSibling과 previousSibling 사용
    - nextSibling - 형제 계층 또는 이웃 계층으로 불리는 같은 계층의 바로 다음 노드에접근
    - previousSibling - 바로 앞 노드에 접근
    - 즉 getElementsByTagName과 getElementByld를 이용하여 접근하기 원하는 노드 또는 그 근처의 노드에 접근하여
    - 노드 객체 프로퍼티(childNodes, firstNode, lastNode, nextSibling, previousSibling)으로 노드 선택
- 문서 내 노드 접근
  - getElementsByClassName()
    - 요소의 class 속성 값을 이용하여 노드 객체를 선택하는 프로퍼티가 표준화됨
    - Class 속성으로, 같은 값을 가지는 요소가 여럿 있을 수 있으므로 배열로 결과를 반환함
  - getElementsByName()
    - name 속성 값으로 노드 객체에 접근할 수 있음
  - querySelectorAll()
    - CSS 셀렉터를 이용하여 노드를 선택함
    - 일치하는 모든 노드를 배열로 반환함
    - querySelector도 셀렉터를 이용해 노드를 선택하지만, 일치되는 첫번째 노드만을 반환함
    - querySelectorAll은 Document 객체일 뿐만 아니라 노드 객체의 프로퍼티임











#### 웹 문서의 조작

- 노드의 종류에 따라
  - 요소의 속성이나 CSS 속성 변경
  - 입력 폼의 값을 읽거나 변경
  - 문서 내에 새로운 HTML 요소와 콘텐츠 삽입
- document.write()
  - 함수 내부에 사용하여 이벤트로 호출하면 -> 기존 문서 전체를 지워버리고 콘텐츠를 출력함에 유의
- writeln()
  - 줄바꿈을 표시한다는 것 외에는 write와 동일함
  - 그러나 HTML에서는 줄바꿈을 무시하기 때문에 <pre> 요소를 포함하는 콘텐츠를 출력하기 전에는
  - write와 writeln이 동일한 결과를 보임
- 노드의 생성과 삽입
  - createElement() / createTextNode()
    - 요소와 텍스트 노드 생성
  - appendChild()
    - 특정 노드의 자식으로 노드를 삽입하기 위해 사용
  - insertBefore()
    - 특정 요소 앞에 삽입하기 위해 사용
    - 부모노드.insertBefore(삽입할 노드, 레퍼런스 노드)
  - replaceChild()
    - 자식 노드 중 특정 노드를 새로운 노드로 치환하는 역할
    - 부모노드.replaceChild(새로운 노드, 바뀔 노드)
- 노드의 속성 조작 (스타일링)
  - element.style
    - element.style.color
    - element.style.backgroundColor
  - getAttribute(attributeName), setAttribute(attributeName, value) 메서드 사용
  - 각각 속성 값을 가져오고, 속성을 속성값으로 설정함
- 노드에 CSS 속성 적용
  - CSS 정의가 되어있는 style 프로퍼티 사용 -> 접근한 노드의 CSS 속성을 직접 적용 / 변경 가능
  - 노드.style.css속성 = css 속성값
- innerHTML
  - 보안적 취약점 있으니 주의
  - createElement()와 createTextNode() 그리고 appendChild()를 한꺼번에 처리하는 효과 발휘
  - 특정 요소 내부에 HTML 코드를 삽입하는 가장 빠른 방법
  - element.innerHTML(text)
- insertAdjacentHTML
  - 보안적 취약점 있으니 주의
  - element.insertAdjacentHTML(text)
    - Position 지정 가능: beforebegin, afterbegin, bbeforeend, afterend (무적)

















- **이벤트**

  - 브라우저에서 특정한 이벤트가 발생하면 이에 대한 이후 행위를 정의할 수 있음

  - 이벤트를 정의하는 경우 인라인으로도 작성 가능하나 분리하여 작성하는 것이 좋음

  - 아래는 가능한 이벤트의 예시

    - load, copy, mouseover, click, submit

  - </onclick> - 태그 자체 속성으로 넣지 말자

    - 태그 별로 스타일 속성을 주는 것과 같이, 좋지 않은. HTML과 자스를 분리하자

  - addEventListener

    - EventTarget.addEventListener(type, listener, [, useCapture]);

    ```javascript
    const button = document.querySelector('button');
    button.addEventListener('click', function() {
    	console.log('click');
    })
    ```

    - for... of - 안에 있는 원소 값들을 하나하나 출력

    - 첫번째 인자 type: 이벤트 유형
    - 두번째 인자 listener: 이벤트가 발생했을 때 실행할 콜백 함수(핸들러)
    - 세번째 인자 useCapture: 기본값 false, 버블링. true인 경우 캡처링
      - var clickfunc(함수 내용)로 함수를 따로 정의하고 넣어줄 수 있겠지만 지양. 스탠다드 폼 눈에 익힐 것













- **이벤트 전파**
  - 이벤트는 해당 요소에서 전파되며, 캡처링과 버블링으로 구분됨
  - 항상 캡처링(위에서 아래)부터 시작하여 버블링(아래에서 위)으로 종료됨
    - 둘 중 어느 것을 기준으로 할 지 내가 정의해야
    - addEventListener의 세 번째 인자로서, useCapture를 통해 특정 상황에 대해 이벤트 관리가 가능
    - 기본적으로 false값이니 -> 버블링이 기본
  - 캡처링
  - 버블링
  - (실습) 클릭에 따라 전파되는 모습, event 객체와 관련하여 이벤트가 발생하면 첫 번째 인자로 들어오는 값, target 값이 버튼으로 모두 동일, current_target (button - div - body로 전파되고, 각 노드값)
  - 이벤트 객체와 this
    - 이벤트 리스너의 콜백함수에서 this를 활용하는 경우, 이벤트 리스너에 바인딩되어있는 요소가 지정됨. 버블링에 의해 this 값이 계속 변경될 수 있음.











- 이벤트 객체
  - 이벤트에 지정된 함수(핸들러)는 이벤트 객체를 매개변수로 받을 수 있음
  - 대표적으로 아래와 같은 속성과 메서드 있음
    - Event.target: 이벤트가 원래 발생하였던 대상
    - Event.currentTarget: 이벤트가 발생하였던 대상
    - Event.preventDefault(): 이벤트를 취소
    - Event.stopPropagation(): 이벤트 전파 중단















- 이벤트 핸들러: 이벤트 객체에 할당되어 해당 객체의 이벤트 반응에 호출되어 처리되는 프로퍼티
- DOM Level 2 Event Model: 표준으로 정해진 이벤트 처리 API
- 이벤트 전파: 이벤트가 발생한 객체에 머물지 않고 상위 객체에 이벤트를 전파하는 것















#### 이벤트 핸들러

- DOM 객체에 할당되어 해당 객체이 이벤트 반응에 호출되어 처리되는 프로퍼티
  - 이벤트 발생 감시 -> 이벤트 감지 -> 지정된 자바스크립트 코드 또는 함수 호출
- 이벤트 모델이란 이벤트 핸들러와 이벤트 API를 정의해놓은 것
  - 기본 이벤트 모델
  - 표준 이벤트 모델
  - 인터넷 익스플로러 이벤트 모델
- 사용법
  - 특정 객체에 이벤트 핸들러 지정 -> 지정 객체에 이벤트 발생 -> 이벤트 핸들러 감지, 정의한 작동 실행
  - 지정 방법
    - HTML 요소에 직접 지정
    - JavaScript에 이벤트 핸들러 적용











(실습)

개발자 도구 - 이벤트 리스너 - 리무브도 가능