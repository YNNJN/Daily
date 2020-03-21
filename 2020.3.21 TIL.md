### JavaScript

- **Event**
- script는 body가 끝나기 직전에 위치하는 것을 권장
- 대개 const를 쓰고 값이 변해야하는 변수일 경우 let을 쓰면 코드 깔끔
- 전역변수가 아니기 위해서는 함수 또는 블록 안에 변수를 넣으면 됨
- (초기화함수(){ 내용 })(); 으로 선언과 동시에 호출할 수 있음
  - 전역변수 사용을 최소화할 수 있는 방법임
- 이벤트 핸들러 내에서 this와 이벤트 객체 e에 대한 e.currentTarget은 이벤트가 등록되어있는 객체를 가리킴
  - 직접 클릭한 것이 무엇인지 알고싶다면? e.target
- 이 때 클릭한 버튼 내에 여러 요소가 있다면 - e.target으로 해당 요소가 선택되는 문제
  - 즉 타겟이 되는 요소가 복잡하게 하위 요소를 가질 때의 처리
  - (M1 CSS 이용) data-value="" 값을 버튼의 클래스마다 주고, 그 하위 요소들에 point-events: none; 하여 요소들이 같은 값을 갖도록 하여 해결
    - 동적으로 컨텐츠가 생성될 때 효과적
  - (M2 JavaScript 이용) 와일문 안에서 체크해서 부모 노드를 타고 올라가게 함
    - 타겟 요소를 직접 선택해야 하는 상황이 다른 데서 발생하는 복잡한 경우에 효과적
    - event.target.dataset.value는 아래와 동일한 의미
    - event.target.getAttribute('data-value')
- 이벤트 호출을 최소화하기 위해 -> 이벤트 위임
  - 자식에 매번 이벤트 호출하는 것이 아닌, 부모에 addEventListner('click', 함수)
  - 페이스북, 인스타처럼 스크롤 범위에 따라 부분 정보를 로드하는 방식의 무한 스크롤 인터페이스의 경우 이벤트 위임 방식이 효과적으로 사용됨
  - 데이터가 하나하나 로드될 때마다 이벤트를 걸어줄 필요 없이, 부모에 클릭 이벤트를 걸어주고, 클릭한 객체에 대해 이벤트가 발생







- **DOM Script** 조작

- data-로 시작하는 표준 커스텀 속성
  - data-index, data-id, data-role 등 data-의 형식으로 시작하면 어떤 속성이든 필요에 따라 동적으로 임의 추가 가능
  - .setAttribute('data-id', )
  - .getAttribute('data-id')
- .innerHTML = ' 내용 '
- .appendChild(const) - 수행한 객체의 마지막 자식으로 어펜드함
  - .removeChild도 참고
- .classList.add(class) - 기존의 것은 놔두고 추가
  - .classList.remove, .classList.toggle, classList.contains도 참고
  - .className는 기존의 것을 새로운 것으로 대체







### CSS

- background-size: contain;
  - 이미지가 잘리지 않고 틀에 꽉 차게 사이즈를 조절함
- background-size: cover;
  - 이미지가 틀에 완전히 차서 잘릴 수 있음
- Animation - alternate / reverse
- Animation - duration
- 배경에 overlow: hidden;
  - 애니메이션이 배경을 벗어날 경우 스크롤 x, 숨김처리 함

