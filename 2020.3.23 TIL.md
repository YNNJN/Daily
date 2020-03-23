### review

- 왼쪽 위에 쌓인다

- 블록 레벨은 전체 너비를 가져가고

- 인라인은 컨텐츠 너비의 영역만큼만 가져감

- flex 이전에는 배치를 위해 float, position를 지정해야 했음

- flex
  - container, item

  - main axis, cross axis

  - 즉 각 축을 기준으로 정렬 가능한 유연한 박스의 개념

    - 1. flex 지정하는 순간 row를 기준으로 배치 

      2. 메인 축의 처음부터 배치

      3. 컨텐츠의 크기 / 너비만큼 영역을 가지게 됨 (더 작을 수도 있음)

      4. 모든 영역은 cross axis를 모두 채움

    - 4, 기본값이 no wrap -> 흘러넘치지 않게 한 줄에 배치

    - flex-wrap: wrap; 각각의 너비만큼 가지고, 자리 가 없어 밀려나가면 줄바꿈되어 아래 배치











### flex 속성

- 1. flex-grow

     >  남은 너비를 각각 비율로 나눠서 가져감, 기본값 0

- 2. justify-content

     >  main 축을 기준으로 정렬함

     - 기본값 flex-start
     - flex-start, flex-end, center, space-around, space-between, space-evenly

- 3. align-items

     > cross 축을 기준으로 정렬함

     - 기본값 stretch
     - stretch, flex-start, flex-end, baseline, center

- 4. order

     > 아이템의 순서를 정의할 수 있음, 기본값 0, 음수값도 가능

- 5. align-self

     > 아이템에 직접 align을 지정할 수 있음













### Advanced

- flex-grow가 남은 너비를 가져간다면, flex-shrink는 넘치는 너비를 가져감
  - 컨테이너를 아이템의 너비들의 합이 초과할 때, 그 넘치는 것을 어떤 비율로 가져갈 것인가
- flex-basis
  - 기준 너비
- flex는 margin-top: auto;가 가능
- Flex - 1차원
- Grid - 2차원 - flex보다 조금 더 유연
- Justify-content-between / around 요소의 차이
  - between: 주축 방향의 공간을 flex 항목 사이의 공간에 균등 배분, 양쪽에 붙이고 정렬함
  - around:  시작선, 끝선과 flex 항목 사이의 공간도 균등 배분, 양쪽 공간도 같이 정렬함
- fixed-bottom / stickty-top 요소의 차이
  - fixed-bottom: 항상 고정된 위치에 표시됨 
  - sticky-top: 스크롤을 내리다 요소가 상단에 위치할 때 고정함
- sticky는 자기 높이만큼 자기 공간을 차지, 자기 부모 높이 안에서만 붙는 성질
- fixed는 자기 높이를 버리고 공간 차지 x, 떠있음













### FlexboxFroggy

- https://flexboxfroggy.com/#ko
- ![스크린샷 2020-03-23 오후 12.27.41](/Users/myung/Desktop/스크린샷 2020-03-23 오후 12.27.41.png)
  - flex-flow: direction wrap;
    - flex-direction과 flex-wrap의 숏핸드



- ![스크린샷 2020-03-23 오후 12.54.18](/Users/myung/Desktop/스크린샷 2020-03-23 오후 12.54.18.png)
  
  - align-content - 부모요소에서 사용, 부모 요소와 자식 요소의 세로 사이즈가 정해진 상태에서 자식 요소의 수직에 대한 정렬을 진행할 때 사용. 부모 요소에는 flex-warp: wrap; 상태여야
  
    - 두 줄 이상일 때, 두 줄을 한꺼번에 옮겨버리는
  
    - align-items vs align-content



- ![스크린샷 2020-03-23 오후 12.53.30](/Users/myung/Desktop/스크린샷 2020-03-23 오후 12.53.30.png)











### Bootstrap

- 구글웹스토어 - wappalyzer 설치 -> 각 웹 사이트에 어떤 기술들이 적용되었는지 알 수 있음

- 반응형, 모바일 우선이 가능한 형식으로 웹사이트 만들 수 있게 하는 FE component library

- 이미 만들어진 좋은 HTML, CSS, JS 코드를 클래스의 형태로 가져다 쓸 수 있는 라이브러리

- HTML vs bootstrap

  - 태그가 보이는 모습부터 다름

  - 브라우저마다 값이 다르니 => 표준화 하자
    - reset css vs nomalize css 요소로 같은 규격을 가져가려 함 (과거)

- Bootstrap reboot.css
  - 모든 브라우저에서 똑같이 보이도록 초기화함
  - 모든 가상으로 만들어지는 요소를 (::before, ::after) box-sizing: border-box;로 지정
  - 시맨틱 태그들 적용 안되는 브라우저에 대해~ 블록으로 정의하자
  - 폰트패밀리, 사이즈 지정
  - ol ul은 마진 탑을 없애자
  - a태그 색, hover 시 색 바꿈
- 크롬의 기본 폰트사이즈 16px
- 크롬의 기본 바디 마진 8px
- BootstrapCDN(Content Delivery Network)을 통해 CSS, JS를 활용
  - 컨텐츠를 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템
  - 가장 가까운 서버를 통해 빠르게 전달 가능하도록, 빠른 로딩 가능
  - 즉 특정 소스코드, 파일을 온라인 상에서 빠르게 가져다 쓸 수 있음
  -  -> CSS를 헤드에, js를 바디의 닫는 태그 안에 입력

- BootStrap4부터 CSS의 flex 도입 (Documentation 참조)

- Flex-direction의 네 가지 요소와 대응하는 bootstrap 클래스

  - row: flex-row
  - row-reverse: flex-row-reverse
  - column: flex-column
  - column-reverse: flex-column-reverse

  









### Utilities

- spacing

  - .m-0 (마진 0)
  - .mr-0 (마진 오른쪽 0)
  - .mx-0 (마진 오른, 왼 0)
  - .py-0 (패딩 탑바텀 0)
  - .mt-1 (마진탑 0.25rem) - 4px
    - .mt-2 0rem.5 8px
    - .mt-3 1rem 16px
    - .mt-4 1.5rem 24px
    - .mt-5 3rem 48px
  - 음수도 가능
    - .my-n0 (마진만 가능, 패딩은 불가)
  - .mx-auto
    - margin-left: auto; margin-right: auto;
  - 마진값과 패딩값을 클래스를 주는 형식으로 부여 가능

- color

  - 색상 이름으로 지정하는 것보다 어떠한 곳에 사용될 것인지를 class 이름으로 지정했다고 생각
  -  bootstrap 에서는 primary를 파란색으로 지정했지만, 다른 색으로 색상을 바꿔서 사용 할 수도 있고, 직관성을 위한 네이밍이라고 생각할 것
    - .bg-primary (백그라운드)
    - .text-success (컬러)
    - .alert-warning (경고창)
    - .btn-secondary (버튼)

- border

  - .border. border-success (앞은 보더 정의, 뒤는 보더 색상)
  - .border-radius도 지정 가능

- display

  - .d-block (display: block;)

  - d-(sm, ml, lg, xl)-none
    - .d-sm-none (특정 너비가 넘어가면 display: none; 하겠다)
    - 기기의 브라우저 너비에 따라 다른 반응형 디자인 가능
    - 반응형으로 디스플레이 크기에 따른 변화는 CSS에서 미디어쿼리로. js보다는

- position

  - .position-static
  - .fixed-top, .fixed-bottom
  - 브라우저를 기준으로 left: 0; right: 0; -> 너비를 100% 채움
  - 과거 IE6이전에서는 절대위치인 요소에서 width:100%가 제대로 적용되지 않는 현상이 존재
    - 이를 해결하고자 left:0, right:0 으로 부모 요소의 너비를 가득 채울 수 있도록 사용함
    - 지금은 모든 브라우저에서 문제 없이 작동하므로 width:100%를 사용하여도 문제 x
    - 그러나 width:100% 인 상태에서 padding 값을 추가하게 된다면 padding 값을 준 만큼 요소의 너비가 커져서 원하지 않는 형태가 될 수 있음
    - 이를 해결 하기 위해서 calc()를 사용 하는 방법이 있지만, 안정적인 레이아웃과 CSS를 위해 left:0, right:0 사용 권장

- text

  - text.center
  - .font-weight-bold

