### CSS 정렬



- Absolute: relative 요소를 기준으로 함. 이 때 부모 요소를 relative로 지정해줌
  - 부모요소에 relative가 없다면?
    - 상위에 static 이외의 position 요소가 없다면 최종적으로는 body를 찾아감
  - relative는 기존 레이아웃이 깨지지 않고, absolute는 레이아웃이 변경될 수 있음 (제 위치를 버릴 수 있음)
- Flex - 정렬을 편하게 하기 위해 제안된 개념
  - 부모요소(container, dispaly: flex), 자식요소(item)
  - main axis
    - justify-content
  - cross axis
    - align-items









### form, input



- Label - for를 통해서 input의 id 값과 동일하게 처리, 연결
  - Label과 for를 함께 쓰는 것을 권장 (스크린 리더를 위한 웹 접근성 향상을 위해)
  - for를 사용하지 않을 경우 Label 태그 안에 input태그를 중첩시키는 방법으로
- 1rem = 16px
  - rem 값은 문서의 최상위 요소인 html 요소의 크기를 기준으로 함 
  - px 대신 rem, em을 사용하면 상대적인 크기를 지정하기 때문에 사용자 화면을 고려한 비율을 나타낼 수 있음
- Input태그 - for
  - for를 통해서 input의 id값과 동일하게 정의하면, 해당 input의 라벨로 지정되어 라벨에 커서 위치 시에도 입력란 선택 가능
  - 커서처리와 마우스 hover 또한 UI를 위한 요소
- input태그 - required (예외처리 - 메시지는 span에)
- Input태그 - placeholder (입력 란의 초기값 보여짐)
- required autofocus (해당 인풋으로 빠른 포커징, 즉 바로 입력 가능 UX, UI)
- required autocomplete="username" - 자동완성
  - username은 autocomplete가 가진 값들 중 하나
  - input for의 username은 id값
- => required, autofucs, autocomplete와 같은 속성은 실제로 나중에는 서버에서도 예외처리를 해야
- Label에 별 달기 - :after
  -  HTML에 바로 적용이 아닌 의사 선택자를 이용할 경우, 추후 스타일 속성을 적용하거나 할 때 편함
  - after를 쓰지 않고 스타일링할 경우, span 태그나 다른 태그를 이용해서 감싸줘야하는데, after 사용하면 그럴 필요 x
- margin shorthand
  - 1- 사방, 2- 상하, 좌우, 3 - 상, 좌우, 하, 4 - 상, 우, 하, 좌









### 덧



- 개발자도구 console의 이용 상황?
  - 간단한 BOM, DOM 혹은 자바스크립트 코드의 output을 확인하기 위해 주로 사용함
  - 추가로 이벤트를 디버깅하거나 모니터링하기도



- HTML에서 예외처리를 하는 것이 좋은지? 아니면 JavaScript에서 하는 것이 좋은지?
  - HTML로만 예외처리를 했을 때 처리하지 못하는 부분이 발생하는데, 이 부분을 자바스크립트에서 처리해줌
  - form이나 input 태그에 대한 예외처리 또는 검증 작업은 추후 서버에서 한 번 더 검증하는 방식으로 이루어지는 것이 바람직

