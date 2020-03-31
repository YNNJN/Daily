### Intro

- 모델을, db를 사용한다는 것은 이 세상의 정보들을 표를 통해 표현하겠다-의 의미
  - 게시글, 포스트, 유저 관련 기능
  - 게시글 테이블 - id, 제목, 내용, 사진, 좋아요 개수, 덧글개수
- db를 디자인 할 때
  - 열에 들어올 수 있는 데이터 타입을 지정 (CharField, TextField, )
- SQL - 데이터 조작 언어 (데이터를 crud)
- ORM - 파이썬 코드로 db 조작 (장고가 파이썬의 코드를 sql로 번역함)











### Django CRUD

### 프로젝트 및 app 설정





#### 1. 프로젝트 생성 

- django-admin startproject crud
- cd crud
- python manage.py startapp articles



#### 2. 프로젝트 설정(settings.py)

- Settings.py
  - allowed host
  - installed apps



#### 3. app 생성(articles)

- app 등록
- urls.py 생성











### Model 활용





#### 1. model 정의

- models.py (파이썬의 클래스를 이용해서 모델을 정의)

  ```python
  from django.db import models
  
  # Create your models here.
  class Article(models.Model): #framework의 지정 규칙
    title = models.CharField(max_length=140) #max_length 옵션 가짐 #sqlite는 255자(db마다 다름)
    content = models.TextField() #text 길이에 제한 x
    created_at = models.DateTimeField(auto_now_add = True) #게시글 생성될 때마다 생성 날짜, 수정 날짜 저장
    updated_at = models.DateTimeField(auto_now = True)
  ```

  - `id` 필드는 자동적으로 `pk` 값으로 생성됨



#### 2. 마이그레이션

- 마이그레이션은 django에서 모델의 변경 사항을 데이터베이스 스키마에 반영하기 위한 방법

- 정의된 모델을 DB에 반영하기 위해 명령어를 통해 마이그레이션 파일을 생성 (설계도를 파일로 만들어놓음)
  - python manage.py makemigrations
    - migration 파일이 보고 새로운 db 파일을 만들어줌
- 생성된 마이그레이션 파일을 DB에 반영하기 위한 명령어
  - python manage.py migrate
- 확인
  - python manage.py showmigrations











### Admin 페이지 활용

- 관리자 계정 생성

  - python manage.py createsuperuser

- admin 등록

  - admin 페이지를 활용하기 위해서는 app별로 있는 admin.py에 정의되어야

  ```python
  # admin.py
  from django.contrib import admin
  
  # Register your models here.
  from .models import Article
  admin.site.register(Article)
  
  ```

- 확인

  - `/admin/` url로 접속하여, 관리자 계정으로 로그인 가능











### Django ORM

- django shell
  - python interactive interpreter를 django 프로젝트에 맞게 쓰기 위한 기능
  - python manage.py shell (처음)
  - python manage.py shell_plus (이후)
    - pip install ipython
    - pip install django_extensions
    - 이후 settings.py installed-apps에 'django_extensions' 추가 ('articles' 위에, 직접 만든 앱들은 아래에 배치 권장)
    - 쉘 종료 명령어는 `ctrl+d`

- **CREATE** (데이터를 만들기, 세가지 방법 (주피터))

  - 1. article = Article()
  - article.title = 'first'
  - article.content = 'Django!'

  - article.save()

  - 2. article2 = Article(title='second', content='second content')로 코드 한 줄로 테이블에 값 추가 가능

  - Article 테이블 값 중 모두를 불러옴

    - Article.objects.all()

  - 3. Article.objects.create(title='third', content='third content') - 만드는 동시에 저장, save 필요 없음

    - 변수에 저장하여 불러올 수 있음
    - article4 = Article.objects.create(title='fourth', content='fourth content')

- **READ** (데이터 불러오기)

  - Article.objects.all()
  - article3 = Article.objects.get(id=3)

- **UPDATE**

  - article3.title = 'thirdthirdthird'
  - article3.save()
  - article3.title - 확인

- **DELETE**
  - a1 = Article.objects.get(id=1)
  - a1
  - a1.delete() - 지워진 값이 결과로 뜸
  - Article.objects.get(id=1) - 확인(error)
- 저장한 내용으로 접근
  - Article.objects.get(title='fourth') - 내용으로도 가져올 수는 있는데 id 값으로 접근 권장
    - 이유는 title은 중복되니까
  - a = Article.objects.get(title='fourth', content='fourth content')
    - title content 둘 다 일치하는 것 가져올 수 있긴 있네
  - 중복되는 값을 가져오면 리스트로 반환되는지?
    - X, get은 가장 먼저 일치하는 것 딱 하나만 반환함
    - 여러 개 반환할 때는 filter 사용
  - article[]
    - 리스트처럼 조작 가능한데, 음수 인덱스는 x
- [field-types](https://docs.djangoproject.com/ko/2.1/ref/models/fields/#field-types)

