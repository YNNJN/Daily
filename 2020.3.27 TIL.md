### Django 파일 구조

- **프로젝트**

- Django_intro - 루트 디렉토리로 이름 변경 가능
  - manage.py - runserver 등 웹 서버를 실행하고 관리하는 기능을 수행, 명령어를 실행할 수 있도록 함 (수정 x)
  - Django_intro - 이름 바꾸면 여러 설정들을 많이 바꿔야 (수정 x)
    - init.py - 해당 디렉토리가 파이썬 모듈로 작동 가능하도록 함 (디폴트 빈 파일, 삭제 x)
    - settings.py - 설정을 기록해놓은 파일
      - SECRET_KEY - 패스워드 암호화할 때 사용하는 키
      - Debug = True - 디버그 가능한 상태, 배포할 때는 False로 설정
      - ALLOWED_HOSTS = ['*'] - 도메인 주소 뒤에 다른 값의 입력도 허용됨
      - LANGUAGE_CODE = 'ko-KR' - 언어 코드, 한글 설정
      - TIME_ZONE = 'Asia/Seoul' - 서버 시간, 서울 설정
    - urls.py - 루트 url 설정 파일, 배포 시 수정이 필요함
    - wsgi - web server gateway interface, 웹 서버에 배포할 때 설정 파일들을 연결해주는 파이썬 파일
- **앱**
- pages/ - 루트 디렉토리
  - migrations/ - 파이썬 모듀류로 작동하는 폴더, 데이터 베이스 스키마 관련 역할을 수행함
  - Init.py - 해당 폴더가 파이썬 모듈로 작동 가능하도록 함 (디폴트 빈 파일, 삭제 x)
    - 모듈 관련 파일, 이것이 하나의 모듈이다 -의 의미
  - admin.py - 관리자가 접속하면 보이는 화면, 내장되어있음
  - app.py - 앱을 설정함
  - models.py - 장고 DB 관련 파일 / DB 사용 계획, 정의, 연결 등의 다양한 설정 가능
    - from django.db import models
      - django 폴더 안에 db 폴더 안에 있는 models에 접근
  - tests.py - 테스트를 위한 파이썬 파일로, 테스트 코드를 작성함
  - views.py - 관리자 뷰, 화면 구성을 위한 파일
    - from pages import views











### DTL

> 템플릿파일(html)은 django template language를 통해 구성 가능

- DTL (장고 템플릿 랭귀지)에서는 괄호 표현 {}, ()을 못 씀

  - DCL??

- 100% 파이썬이 아닌, 템플릿을 그리기 위한 메뉴가 존재

- 인덱스 접근은 `.0` 으로 대신함

- 문법은 `%%`로 감싸고 있음

  ```html
  <!--인덱스 접근-->
  <li>{{ menupan.0 }}</li>
  <!--for문-->
  {% for men in menupan %}
  <li> {{ menu }}</li>
  {% endfor %}
  ```

  - if문도 같은 방식으로, {% endif %}

- 출력하고 싶은 내용들은 중괄호 두 개 `{{ }}`로 표현











### Variable Routing

- URL 자체를 변수처럼 사용해서 동적으로 주소로 만드는 것

- url의 특정한 값을 변수로 받겠다

  ```python
  #urls.py
  path('hi/<str:name>/', views.hi),
  #views.py
  def hi(request, name): #name, url과 항상 같은 값 #request는 컨벤션 상 사용, 변경 지양
      context = {
          'name': name
      }
      return render(request, 'hi.html', context)
  #templates/hi.html
  <h1> 안녕, {{ name }} </h1>
  ```

  - views 함수에서 받는 name과 url의 <str: name>이 같아야
  - html 문서의 이름과 render 함수 내부의 인자가 같아야

- 주소가 담고있는 기능에 주목

  - 이름 넘겨주는 hi page
  - 계산하는 add page 만들어봄

  ``` python
  #urls.py
  path('add/<int:a>/<int:b>/', views.add), #슬래쉬는 항상 닫아주는 습관
  #views.py
  def add(request, a, b):
      result = a+b
      context = {
          'result': result
      }
      return render(request, 'add.html', context)
  #templates/add.html
  <h1> {{ result }} </h1>
  ```

- url.py에서 정규표현식 쓰려면 import re 이용











- 장고 실제 코드를 깃헙에서 확인하며 공부하기

- 크롬 웹스토어 - octotree
  - 해당 저장소의 폴더 구조를 바로 보여줌
  - 깃헙에서 탐색할 때 편리
- [MDN 참조](https://developer.mozilla.org/ko/docs/Learn/Server-side/Django/skeleton_website)