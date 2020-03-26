### 웹 프레임워크, Django

- 웹 페이지를 개발하는 과정에서 겪는 어려움을 줄이는 것이 주 목적

  - 기능은 다음과 같음
  - 데이터 베이스 연동
  - 템플릿 형태의 표준
  - 세션 관리
  - 코드 재사용

- Django

  - 파이썬 기반의 웹 프레임워크
  - 스포티파이, 인스타, 드롭박스, 딜리버리 히어로
  - 대용량 처리 가능, 안정적

- 웹의 프로토콜

  - 클라이언트 <-> 서버
  - 요청 <-> 응답

- 장고를 통해 응답도 해보자

  - HTML 문서를 전달하는 것
  - 사용자의 요청을 받아서 

- 장고는 어떻게 동작?

  - 모델 - 뷰 - 컨트롤러 모델 패턴(MVC)을 따름
    - 소프트웨어의 디자인 패턴
    - 소프트웨어 설계 방법과 관련
    - M (DB의 설계 조작을 담당)

  - 장고는 Model-데이터 관리 Template-인터페이스(화면) View-중간관리(상호동작)
    - Template은 플라스크 사용하며 웹 페이지 저장했던 Template 폴더와 같은 역할

  <img src="/Users/myung/Desktop/basic-django.png" alt="basic-django" style="zoom:70%;" />

- AWS Cloud9

  - 브라우저에서 직접 코드를 작성, 실행 및 디버깅할 수 있는 클라우드 기반 IDE
  - 클라우드 기반의 아이디
  - 우분투(18.04.4 LTS), 파이썬(3.7.6) 설치되어있음
  - 개별 로컬 환경에 영향이 없음
  - 추후 로컬 개발 환경 설정도 진행할 예정

- 파일 디렉토리 - 파일 편집기 - 터미널

- 프로젝트 생성

  ```bash
  django-admin startproject {프로젝트명}
  ```

  

- allowed_hosts = ['*'], 모든 호스트에 대해 열어주겠다

  ```python
  #settings.py
  ALLOWED_HOSTS = ['*']
  ```

  

- 8080은 포트 번호, 실행 위한

  ```bash
  python manage.py runserver 8080
  ```



- 실행된 서버는 우측 영역의 url을 클릭함

- https://b10a069894e74a3b963d7e37a0bc0163.vfs.cloud9.us-west-2.amazonaws.com



- 리눅스 basic

  ```bash
  ls #현재 디렉토리의 list
  python manage.py runserver #서버 실행시 ls 명령어를 통해 파일의 존재 여부를 확인할 것
  cd.. #change directory, 상위 디렉토리로 이동
  git add . #.은 현재 디렉토리를 의미, ..은 상위
  cd ~ #최상위 디렉토리로 이동 (home)
  cd - #방금 있었던 디렉토리로 이동
  cd (space) (tab) #갈 수 있는 항목들 보여짐
  pwd #print working directory, 작업 중인 디렉토리의 절대 경로를 출력함
  pip list #현재 환경에 설치된 패키지 목록을 확인함
  mkdir #디렉토리를 만듦
  touch #폴더에 파일을 만듦
  ```











### App 생성

- 앱이란
  - app은 장고 프로젝트 내에서 사용하는 python 패키지
  - 하나의 app은 자신만의 독자적인 M, T, V를 포함하고 있음
  - 장고 프로젝트는 모듈화된 여러 개의 앱들로 구성됨
  - 앱 단위로 모듈화하여 개발 및 유지 보수가 효율적이고, 다른 프로젝트에서 재활용도 가능

- Django는 여러개의 앱을 가진 하나의 프로젝트로 구성됨

  - 커뮤니티 만들 때
    - 회원과 관련된 app - accounts
    - 게시글과 관련된 app - posts

  ```bash
  python manage.py startapp {app 이름}
  ```

- app을 생성하고 반드시 settings.py의 installed_apps에 등록할 것



- app 등록

  - 흐름: Url -> 처리할 함수 만들고 -> html을 보내줌

  ```python
  #urls.py
  from django.contrib import admin
  from django.urls import path
  from pages import views
  
  urlpatterns = [
      path('index/', views.index), #path의 url은 항상 /로 닫아줌
      path('admin/', admin.site.urls),
  ]
  ```

  ```python
  #views.py
  from django.shortcuts import render
  
  def index(request): #뷰에서 함수를 정의하는 경우 첫 번째 인자는 항상 request, 사용자의 요청정보가 들어있는 객체를 의미
      return render(request, 'index.html') #render 함수를 통해 html 파일의 정보를 반환함
  ```

  ```html
  <!--index.html-->
  <h1>사용자가 들어올 수 있는 길 url-pass,
  view에 있는 함수로 넘겨줘,
  views의 함수가 처리하여 index 파일을 넘겨줌</h1>
  ```







- 장고에서는 모든 폴더들이 파이썬의 모듈로서 기능함
  - 따라서 다음의 from __ import __의 꼴에 유의

- 1. 사용자가 요청을 보낼 경로를 정의함 (**url** 정의)
  2. **view**에서 앞으로 해야하는 동작 정의함 (함수로)
  3. **HTML**에서 반환할 파일 만듦 (**templates**에서)
- Url - view - HTML을 기억
- render는 from django.shortcuts import render에서 불러온 함수
- template이 lotto.html과 context(딕셔너리)를 가지고 새로운 Template을 만듦
- {{ pick }}에서 pick은 키 값 의미
- 경로 지정 시
  - 'lotto' - 현재 경로부터
    - www.mysite.com/index/lotto
  - '/lotto' - 루트를 기준으로
    - www.mysite.com/index
    - www.mysite.com/lotto











### 비교

- **Flask vs Django**
  - 두 개의 프레임워크 모두 웹을 만들기 위한 도구인 것은 동일
  - flask는 바닥부터 하나하나 만들고, django는 MTV 패턴을 이용하여 어느정도 뼈대를 잡은 상태로 개발을 시작할 수 있음, 즉 개발자의 자유도가 높음
    - 어떤 확장 모듈을 사용할 것인지 개발자가 취사선택 가능, 그만큼 많은 종류유ㅢ 모듈을 직접 구분하고 분석하는 노력이 필요
  - flask는 마이크로프레임워크를 표방해서 만들어졌고, django는 풀스택 프레임워크라 부름. 개발자의 자유도가 낮지만 생산성과 안정성 등 다른 측면에서 장점이 있음
-  **프레임워크 vs 라이브러리**
  - 프레임워크는 말그대로 하나의 기반 구조, application 개발 시 필수적인 코드, 알고리즘, 데이터베이스 연동 같은 기능들을 위해 어느정도 뼈대를 제공함
  - 반면 라이브러리는 특정 기능에 대한 도구 또는 함수들을 모은 집합임
- **Static web vs Dynamic web**
  - Static web
    - 서버에 미리 저장된 파일이 그대로 전달되는 웹 페이지
    - 서버는 사용자의 요청에 해당하는 저장된 웹 페이지를 보냄
    - 사용자는 서버에 저장된 데이터가 변경되지 않는 한 고정된 웹페이지를 보게됨
  - Dynamic web
    - 서버에 있는 데이터들을 스크립트에 의해 가공처리한 후 생성되어 전달되는 웹페이지
    - 서버는 사용자의 요청을 해석하여 데이터를 가공한 후 생성되는 웹 페이지를 보냄
    - 사용자는 상황, 시간, 요청에 따라 달라지는 웹 페이지를 보게됨
    - url.py가 마중 나옴 -> 사용자의 요청 -> 파일이 있으면 view.py가 전달받아 -> template에서 자료를 꺼내와 -> view가 사용자에게 보여줌, 이 때 model.py가 database로서 view와 상호작용

