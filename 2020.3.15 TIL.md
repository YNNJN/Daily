## Web Project Review



- navigation, footer, home, community를 요소로 하는 홈페이지를 만들었음
- 요소 각각을 차례로 만들어나가며 구현의 흐름을 일단 익힐 수 있었음
- 정확한 명세를 토대로하니, 내가 어떤 작업을 하고 있는지 무엇이 되지 않고 있는지를 확실하게 알 수 있었음
- 충분한 복습 후에 프로젝트에 착수했다면 더 깔끔하게 구현할 수 있었으리라 생각되지만, 구글 선생님께 물어가며 우당탕탕 일단 만들어낸 것만으로 재밌고 신났음
- 그럴싸하게 만들어지긴 했는데 원하는대로 구현된 이유를 알 수 없는 부분도 많은 군데 있음
  - community에서
    - main class의 윗 부분에 공백을 줄 때 margin-top은 적용이 안 되고 padding-top은 적용이 되는 이유를 모르겠음
    - article에서 h2와 span을 하위 항목으로 갖는 div에 float: left;하는 클래스를 적용했을 때 전체 적용이 안 되고 span에 left를 번복해서 적용해주니 원하는대로 구현이 된 이유를 모르겠음
  - home에서
    - flex를 이용한 조작에서 justify-content가 기준으로 하는 100% 너비가 무엇을 기준으로 하는지 알고싶음
    - 좌우로 스크롤하면 Justify-content: around와 between, 어떤 것으로 지정하는 지에 따라 오른쪽 여백이 생기고 - 생기지 않고의 여부가 계속 바뀌었음
    - 이것이 header 배경이미지의 크기를 %로 조작하지 않은 것에서 기인한다고 생각하여 해당 이미지를 width: 100%로 설정해보았으나, 원하는 결과를 얻지 못했음
- 더 발전시킬 수 있는 부분은
  - nav에서
    - text-decoration: none;을 불필요하게 중복하여 css에 적용한 부분
- 알아볼 부분은
  - 반응형까지 고려한 설계
  - 그리고 박스의 정렬에 대한 복습이 꼭 필요.....
- 배운 부분은
  - 세로 정렬에 있어서 table, table-cell 이용한 방법, padding 이용한 방법을 모두 시도해봤던 것
  - position: fixed;로 상단과 하단에 navigation과 footer를 고정시켰던 것
  - position: sticky;는 위의 영역 바로 다음을 위치로 함(nav 바로 다음부터를 header 영역으로 할 수 있음)
  - line-height의 높이가 정해져있는 상태에서 다른 개체를 정렬하려 할 때엔 vertical-align: middle; 사용이 가능
  - css의 flex와 button에 대해 더 많은 정보를 검색해보았던 것
    - display: flex, flex-direction: column or row; (정렬의 흐름)
    - main축(세로)은 justify-contents로 정렬, cross(가로) 축은 align-items로 정렬
  - 페이지도 넘어가고 마우스 오버에 따른 효과도 만들 수 있다!
  - 개발자 도구의 효용을 실감한 것. 막히는 부분에서 나를 여러번 구제해주셨음

