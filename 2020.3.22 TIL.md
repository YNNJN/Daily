### CSS & JavaScript Animation

- transform: translate3d(0px, -10px, 0px);
  - y축만 값이 변경되지만 translateY보다 translate3d 사용 권장
  - 후자는 하드웨어 가속을 사용하여(GPU 사용), 성능이 더 좋기 때문
- translate에서의 %는 object의 크기를 100%로 함
- 3d 효과는 공간 자체를 3d 공간으로 만들어줘야, 혹은 오브젝트 자체에 3d 속성을 부여해줘야 (persepective)
- 시점을 균일하게 하기 위해 -> 회전체 자체에 perspective 부여
  - transform: perspective(500px) rotateY(-100deg);
- 기준점 변경 -> transform-origin: left;
- transition 축약형
  - transition = transition-duration
  - transition: _s _s; (duration과 delay)
    - delay는 몇 초 후에 시작하세요의 의미









### JavaScript Refactoring 1

- 스크립트 처리 중 돔에 접근하는 방식은 연산 처리가 가장 느린 방식

- 범용적이고 빠른 연산을 지향하기 위해서는 구체적인 클래스를 이용하는 방식은 바람직 x

- **여러 요소 중 하나만 활성화하는 패턴**을 아래의 방식으로 개선할 수 있음

  1. 현재 활성화된 아이템을 저장할 변수를 만들어둠

  2. 변수를 체크해서 비활성화 시키고

  3. 현재 선택한 것을 활성화 시키고 (변수를 갱신, 부모 노드로)



### JavaScript Refactoring 2

- 위의 활성화 - 비활성화 코드는 한 함수에 둘 모두를 담고 있어 바람직 x

- 이벤트 핸들러는 최대한 간단하게 작성
  - 기능을 잘게 쪼개면, 분리하면 코드가 유연해짐
- function activate(), function inactivate()로 쪼개는 방법으로 개선할 수 있음









### JavaScript Object

- JavaScript의 this는 메서드를 실행할 주체 객체를 가리킴
- 실행되는 환경에 따라 값이 바뀜
- 전역 영역에 정의된 함수 안에서의 this는 -> window 객체를 가리킴
- 생성자(constructor), 객체를 생성해내는 역할을 하는 함수는 관례적으로 첫 글자를 대문자를 씀
  - 매개변수 넣어서 호출
  - 함수가 생성자로서 호출하게 하려면, 앞에 new라는 키워드를 붙임
  - 이로써 전역 영역에 정의된 함수 안에서의 this가 window 아닌 개별 객체를 가리키게 됨
- 생성자 함수로 생성해낸 개별 객체를 인스턴스라 함
- 인스턴스가 공통으로 사용하는 메서드와 속성은 공유하는 형태로 코드 작성을 권장 -> prototype 객체 이용
  - Prototype 객체는 생성자 함수와 한 쌍, 함수 하나 당 하나, 개별 인스턴스가 메서드와 속성을 공유함
  - 객체가, 인스턴스가 늘어나도 메서드와 속성이 늘어나지 x, 메모리 측면에서 유리
- 정리하면
  - 개별적으로 가져야하는 값 -> this
  - 공유하는 값 -> prototype

