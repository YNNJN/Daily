### 정적 파일 관리

- 정적 파일(Js, css, img) 관리

  - style.css

  - css 파일을 templates 폴더에서 관리할 수는 x

  - `static/`로 정적 파일 관리하는 폴더를 앱 내부에 만들어야 (지정된 이름)

    - 하위에 stylesheet/, image/ 등..

    - base.html도 DTL로 링크를 수정해줌

      - 최상단에 {% load static %}
      - 경로 <link rel="stylesheet" href "{% static 'stylesheets/style.css' %}">

    - {% block %}으로 분리한 html 파일에 css를 적용하려면?

      ```html
      {% extends 'base.html' %} <!--항상 최상단-->
      {% load static %}
      
      <link rel="stylesheet" href"{% static 'stylesheets/form.css' %}>
      <img src="{% static 'image/bonobono.jpg' %}">
      ```

    - app이 여러개 있을 경우?

      - static도 templates와 마찬가지로 django는 하나로 모아서 보기 때문에
      - static 폴더 이후에 app 이름의 폴더를 하나 생성하여 분류할 것

    - 다른 위치의 static 폴더를 불러오려면

      - STATICFILES_DIRS라는 변수를 만들고 설정해야 (공식문서 참조)









### 질문들

- charField vs testField
  - 받으려는 문자열의 길이에 따라 취사 선택
  - 제목은 길 필요가 없으니 - `charField`, 본문은 내용이 길 수 있으니 - `textField`
- render vs redirect
  - `render` 는 템플릿을 불러오고, `redirect` 는 단순히 URL로 이동만 함

- gitignore
  - gitignore.io에서 ignore해도 되는 파일들 확인
  - .git/과 같은 선상에 생성할 것

- 오류 발생 상황과 해결 방법 정리
  - Settings.py, No module error -> installed_apps에서 콤마 빠뜨렸는지 확인 
  - TemplateDoesNotExist, Template-loader postmortem -> 경로 확인
  - TemplateSyntaxError, static(tag) -> static(tag) load 했는지 확인
  - No module -> 앱 내에도 urls.py 만들어줬는지 확인
  - TypeError, unexpected keyword argument -> url variable routing, view 함수와 url 인자의 일치 여부 확인
  - IntegrityError, Not NULL -> 값이 Null로 들어오고 있는 지점을 확인











### pjt

- MTV를 모두 활용하여 게시판 서버를 구현해봄

- form의 action 속성의 장고 서버에서의 이해
  - 요청 -> 폼을 보여줌
  - 값을 입력 -> 어떤 경로로 요청
  - 어떤 경로의 함수에서 요청을 받아 -> 폼의 내용을 디비에 저장
- 루트 슬래쉬의 여부에 따른 차이를 직접 경험
  - 붙으면 - 주소가 루트 주소부터 시작함
  - 붙지 않으면 - 주소가 현재 경로부터 시작함
- 디테일 페이지는 하나의 게시글만 보여주기 때문에
  - 반복문 없이 reviews가 아닌 review를 넘겨줘야

