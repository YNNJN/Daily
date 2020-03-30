### DTL, Template extends



- MTV 패턴에서 Template은 실제 반환할 html 파일을 구성하는 역할
- 이때 활용되는 언어는 DTL(Django Template Language)이며, 기초적인 태그와 필터(|)로 구성되어 있음
- 기초적인 태그들은, 조건/반복문과 같은 기능, 주석/block 등
- 필터들은 HTML 문서의 출력 형식을 바꾸기 위한 기능들로 구성됨
  - 문자열 관련 : 길이(length), 줄이기(truncate)





### Template 확장

```html
{% extends 'base.html' %} <!--상속을 위해 제일 상단에 작성해야 하는 코드-->

{% block css %} <!--block 다음은 변수명과 같이 사용함, CSS 속성 관련-->
<style>
    h1 {
        color: blue;
    }
</style>
{% endblock %}

{% block body %} <!--block 다음은 변수명과 같이 사용함, body 관련-->
    {# 주석 #} <!--주석은 이 방식으로 작성-->
    <h1>{{ id }}번째 글입니다. </h1>
    <p>{{ content }}</p>
    <p>{{ content|length }}글자</p> <!--length-->
    <p>{{ content|truncatechars:10 }}</p> <!--10글자 맞춰 ... 말 줄임이 붙음-->
    <hr>
    <!--댓글 출력 반복-->
    <h2>댓글</h2>
    <ul>
    {% for reply in replies %}
        <li>{{ reply }}</li>
    {% endfor %}
    </ul>
    <ul>
    {% for reply in replies %}
        <li>댓글 {{ forloop.counter }}: {{ reply }}</li>
    {% endfor %}
    </ul>
    <ul>
    {% for reply in no_replies %}
        <li>댓글 {{ forloop.counter }}: {{ reply }}</li> <!--반복횟수 출력-->
        {% empty %} <!--비어있을 경우-->
        <p>댓글이 없습니다. 작성해주세요</p>
    {% endfor %}
    </ul>
    {% if user == 'admin' %}
        <p>수정, 삭제</p>
    {% else %}
        <p>관리자 권한이 없습니다</p>
    {% endif %}
{% endblock %}

```







- picsum 이미지를 다 다르게 주기 위해 ?random을 덧붙임
  - src="http://picsum.photos/200/300?random={{ article.0 }}"
- 반복 횟수를 카운트하는 다음의 코드는 동일한 의미를 가짐
  - {% if forloop.counter0 == 0%}
  - {% if forloop.counter == 1 %}







```html
<!--M1. tbody가 계속 생성되는 방식 - 지양-->
{% extends 'base.html' %}

{% block content %}


<table class="table">
  {% for article in articles %}

    {% if forloop.counter == 1 %}
    <thead>
      <tr>
        <th scope="col">{{ article.0 }}</th>
        <th scope="col">{{ article.1 }}</th>
        <th scope="col">{{ article.2 }}</th>
        <th scope="col">{{ article.3 }}</th>
      </tr>
    </thead>
    {% else %}
    <tbody>
      <tr>
        <th scope="row"> {{ forloop.counter0 }}</th>
        <td>{{ article.0 }} </td>
        <td>{{ article.1 }} </td>
        <td>{{ article.2 }} </td>
      </tr>
    </tbody>
    {% endif %}
  {% endfor %}
</table>


{% endblock %}
```



```html
<!--M2. tbody 하나로 만드는 방식 - 지향-->
{% extends 'base.html' %}

{% block content %}


<table class="table">
    <thead>
      <tr>
        <th scope="col">{{ articles.0.0 }}</th>
        <th scope="col">{{ articles.0.1 }}</th>
        <th scope="col">{{ articles.0.2 }}</th>
        <th scope="col">{{ articles.0.3 }}</th>
      </tr>
    </thead>

    <tbody>
      {% for article in articles %}
      {% if forloop.counter0 > 0 %}
      <tr>
        <th scope="row"> {{ forloop.counter0 }}</th>
        <td>{{ article.0 }} </td>
        <td>{{ article.1 }} </td>
        <td>{{ article.2 }} </td>
      </tr>

    {% endif %}
    {% endfor %}
    </tbody>
</table>

{% endblock %}
```













### Template 설정

```python
#settings.py
TEMPLATES = [
    {
        #BACKEND: 어떤 엔진을 쓰는지, 현재 DTL 엔진을 사용, jinja2 등으로 변경 가능
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        #DIR: app 내에 있는 폴더가 아닌 추가로 템플릿으로 활용하고 싶은 경로 의미 (추가경로 정의)
      	#경로 정의는 폴더 구조를 통해 확인할 것
      
        'DIRS': [
            os.path.join(BASE_DIR, 'django_intro', 'templates') #가장 상위 단계부터 단계적으로 콤마로 구분하여 인자 작성
        ],
        #APP_DIRS: True인 경우, 등록된 app(INSTALLED_APPS)의 디렉토리에 있는 templates 폴더를 템플릿 폴더로 활용함
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

```



- DIR에서 경로의 우선순위는
  - DIR을 먼저 탐색한 후 각 앱의 템플릿 폴더를 탐색하는 순서
  -  DIRS에 해당 경로를 지정해 두었다면, 지정된 경로에 존재하는 base.html을 우선 탐색
  - app templates 에서 다시 app 이름의 폴더를 생성했듯이 같은 이름의 base.html 이라도 경로로 구분할 수 있게 됨











### Multiple apps

- 앱이 여러개일 때 -> 앱 별로 url 설정을 분리함

```
app1/
	templates/
		app1/
			index.html
			a.thml
    urls.py
    views.py
    ...

app2/
	templates/
		app2/
			index.html
			b.thml
    urls.py
    views.py
    ...

```





#### 1. url 설정 분리

- 각각의 app 별로 url을 관리함
  - from django.urls import path, include
  - 앱마다 urls.py를 만듦, `include함수`를 통해 가져옴
- 각 프로젝트 별로 urls.py 정의
  - from . import views
  - 현재 디렉토리에 있는 views를 가지고오겠다고 명시적으로 선언





#### 2. templates 폴더 구조

- template 파일을 반환하기 위해 장고는 다음의 순서로 폴더를 탐색함

  (각각의 파일을 모듈로 생각하기 때문에) 

  - `DIRS` 에 정의된 경로의 하위 디렉토리
  - `INSTALLED_APPS` 디렉토리의 `templates` 폴더의 하위 디렉토리 탐색

- 중복된 파일이 있는 경우 충돌이 일어날 수 있음

  - 따라서 templates 폴더를 구조화해야

    1. 앞에 이름을 붙이는 방법 (boards_index)

    2. 폴더 구조를 바꾸어 다중화하는 방법 (boards/index)
       - 아래의 구조로 폴더 구조를 유지할 것

    ```
    app1/
    	templates/
    		app1/
    		
    app2/
    	templates/
    		app2/
    
    ```

    









### Form을 통한 요청 처리

- 과정
  1. 사용자들로부터 값을 받아서(boards/new/)
  2. 이를 단순 출력하는 페이지 구성(boards/complete/)





#### 1. 사용자에게 form 양식 제공

  		1. url 지정
  		2. view 함수 생성
  		3. template

- `form tag`의 `input`과 `url`로 **요청**이 만들어짐

  - form 태그에는 `action` 속성을 정의한다.
  - 사용자로부터 내용을 받아서 처리하는 url
  - input 태그에는 `name` 속성을 통해 사용자가 입력한 내용을 담을 변수 이름을 지정한다.
  - url 예시 :  /boards/complete/?title=제목

  

  - 요청을 딕셔너리로 관리함 QueryDict

    ```
    #쿼리딕트의 내용을 뽑아
    title = request.GET.get('content')
    context = request.GET.get('content')
    context = {
    
    }
    ```

    

  - request는 요청과 관련된 정보들이 담겨있는 객체, 확인은 아래의 메서드로

    - request.GET
    - request.method
    - request.path
    - request.META





#### 2. 사용자 요청 처리

1. urls.py 정의
2. views.py

```python
# boards/views.py
def complete(request):
    title = request.GET.get('title')
    context = {
		'title': title
    }
    return render(request, 'boards/complete.html', context)

```

- `request`에는 요청과 관련된 정보들이 담긴 객체가 저장되어 있음



3. template













### +

- 연산은 view에서만
  - built-in으로는 add만 지원함
  - 다른 연산을 위해서는 외부 라이브러리를 설치해야

- 앱은 구현하고자 하는 기능들의 집합으로 구분함
  - boards - 게시판 기능
  - account - 유저 관리 기능



- 절대경로를 다 작성하는 오늘의 방식 -> 개선해야

- pages/gallery/
  - urls.py의, 기본 주소가 root 주소
  - 현재 위치부터 붙이겠다, 즉 (기본주소) /pages/gallery/

- /pages/gallery/
  - form태그의
  - 현재 위치가 어디든 상관 없이 무조건 root주소/pages/gallery/



