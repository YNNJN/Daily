## 2020.1.16 TIL



#### 예제1_지원자 파일 이름 앞에 삼성 붙이기



1. import os
2. 해당 폴더로 들어가서
3. for rename



작업하고 있는 위치에서 우클릭-VS코드->해당 위치에 파이썬 파일 생성





#### 예제2_삼성을 싸피로 대체하기(replace)



```python
import os

os.chdir(r'C:\Users\multicampus\Desktop\startcamp\day2\dummy')           #change directory, r은 뭘 의미하지

filenames = os.listdir('.')             #현재 위치를 의미하는 .

for filename in filenames:
    os.rename(filename, filename.replace('SAMSUNG', 'SSAFY'))
```





## html



웹은 요청(url)과 응답(문서, html)



<html>이 가장 최상위의 부모 > head > body

클릭 블록-`shift` `tab`--> 들여쓰기 취소 한꺼번에

마크다운과 비슷하게, h1 h2로 글자 사이즈 조절

**p** 는 구역 지정 위해 사용함. 글씨 크기 변화는 X

**a** 는 앵커

**a href**로 링크 태그함

**li, ol**, 순서가 없고 있는 리스트

**input**은 닫는 태그 없음

form > action, input > type, name, placeholder, value 검색 창 만듦

name 파이썬 코드에서 사용하기 위한 이름



```html
<!-- markup.html -->
<html>
<head>
    <title>안녕하세요!!!</title>>

</head>
<body>
    <!--제목 및 본문-->
    <h1> I'm a h1 tag! </h1>
    <h2> I'm a h2 tag! </h2>
    <P> I'm a paragraph! </P>

    <!--링크태그-->
    <a href="https://www.naver.com"> naver로 가기 </a>

    <!--리스트태그-->
    <ul>
        <li> 순서가 없는 리스트1 </li>
        <li> 순서가 없는 리스트2 </li>
    </ul>
    <ol>
        <li>순서가 있는 리스트1</li>
        <li>순서가 있는 리스트2</li>
    </ol>

    <!--사용자 입력을 받기 위한 태그-->
    <form action="https://www.google.com/search">
        <input type="text" name="query" placeholder="검색어를 입력해주세요">
        <input type="submit" value="검색검색">
    </form>
</body>
</html>
```





### Flask



웹은 요청(url)과 응답(문서, html)

naver가 서버를 갖고 있고, 서버가 요청을 인식해서 처리하고 응답하기 때문에 해당 과정 작동

서버를 만들기 위한 프레임워크, 사용자 입장->서버를 제공하는 입장이 되어보자

서버를 개발한다=메뉴판을 만든다



- pip install Flask

- 서버실행

  - cmd에서 실행

    C:\Users\multicampus\Desktop\startcamp\day2>set FLASK_APP=hello.py

    C:\Users\multicampus\Desktop\startcamp\day2>flask run

  - cmd의 응답

    Running on http://127.0.0.1:5000/

    이것이 '루트주소'

    플라스크가 루트 뒤 주소를 알기 위해서는 브라우저 재시작해야

    (cmd 에서 컨C로 끄고 다시 런)



```python
from flask import Flask
from datetime import datetime       #모듈을 불러오는 건 제일 위에 적는 것이 관리의 컨벤션을 위한
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'          #사용자가 요청할 수 있는 것을 요청함


@app.route('/ssafy')
def ssafy():
    return '짜잔!'


@app.route('/dday')
def dday():
    today = datetime.now()
    endgame = datetime(2020, 5, 29)
    td = endgame-today
    return f'{td.days}일 남았습니다!'
```





#### 예제4_리턴 시 html 코드를 보여줌



```python
@app.route('/html')                 #리턴시  html 코드를 보여줌
def html():
    return '<h1>안녕하세요!!!</h1>'


@app.route('/html_lines')
def html_lines():
    return """
    <h1> 여러줄을 보내봅시다 </h1>
    <ul>
        <li>1번</li>
        <li>2번</li>
    </ul>
    """
```





#### 예제5_Variable Routing



```python
@app.route('/greeting/<string:name>')
def greeting(name):
    return f'반갑습니다! {name}님!'


    
@app.route('/cube/<int:number>')
def cube(number):
    return f'{number}의 세제곱은 {number**3}입니당'
```



\#경로의 특정 부분이 계속해서 바뀌길 원함. 사용자의 이름에 따라 다르게 출력. 해당 부분을 변수화

#주소에 변수를 받았으니, 함수에 변수 넣어줘야. 꼭!!!

#indentation에 유의





#### 예제6_랜덤 점심메뉴 추출



```python
import random
    
@app.route('/lunch/<int:people>')
def lunch(people):
    menu = ['짜장면', '햄버거', '파스타', '불고기']
    select = random.sample(menu, people)
    return f'{people}명의 점심 메뉴는 {select}입니다.'
```



people 수를 메뉴 수보다 많이 입력할 경우

```python
import random
    
@app.route('/lunch/<int:people>')
def lunch(people):
    menu = ['짜장면', '햄버거', '파스타', '불고기']
    #select = random.sample(menu, people)
    select = random.choices(menu, k=people)                         
    return f'{people}명의 점심 메뉴는 {select}입니다.'
```

---





#### Debug mode: on



변경사항이 있을 때마다 flask가 변동사항을 반영하여 출력

```python
if __name__ == '__main__':
    app.run(debug = True)                                          
```





#### render_template



- [ ] templates 아래 항목에 있는 html 문서를 확인하고

파일을 그려주는 역할이 render_template

```python
@app.route('/ssafy5')
def ssafy5():
    return render_template('ssafy5.html')
```



- [ ] Variable Routing 부분에서

왼쪽은 html 파일에서 사용할 이름, 오른쪽은 파이썬 내에서의 변수명

(보통 같은 이름으로 사용함. 아래처럼)

```python
@app.route('/greeting2/<string:name>')
def greeting2(name):
        return render_template('greeting2.html', html_name=name)
```



- [ ] Variable Routing , 변수 둘을 한 번에 넘기고 싶을 때

```python
@app.route('/cube2/<int:number>')
def cube2(number):
    result = number**3                                              
    return render_template('cube2.html', number=number, result=result)
```



html에서 {{ }} 출력으로 간단한 조건문 반복문 출력이 가능하게 되는 이유는

flask에서 jinja가 그것을 가능하게 하는 역할을 하기 때문



즉, 아래의 것이 가능함

```html
{% if html_name == '김윤진' %} 
    <h2> {{ html_name }} 왔니??? </h2>
{% else %}
    <h2> {{ html_name }}님 오셨어요??? </h2>
{% endif %}
```



추후 쟝고에서도 비슷한 꼴의 문법을 쓰게 됨. 예제 10번에서도 이용함.





#### 예제7_영화목록출력



```python
@app.route('/movie')
def movie():
    movies = ['겨울왕국', '포드앤페라리', '나이브스아웃']
    return render_template('movie.html', movies = movies)
```



```html
<h1> 영화목록 </h1>
{% for movie in movies %}
    <li> {{ movie }} </li>
{% endfor %}
```





### /ping /pong



사용자와 서버 간 요청-응답 구조를 2번 왕복->핑퐁

http://127.0.0.1:5000/ 의 플라스크 서버가 요청을 보내고 있음

요청1(/ping), 응답1(form)

요청2(/pong), 응답2()



form action = /pong, 우리 서버로 다시 보내벌임

```html
<form action = "/pong">
  <input type = "text" name = "name">
  <input type = "submit">
</form>
```



---

(flask의 공식 문서 참조)  뽑아낼 때. ping.html의 "name"을 함수의 변수에 넣음

```python
@app.route('/pong')
def pong():
    name = request.args.get("name") 
    return render_template('pong.html', name_in_html = name)
```





#### 예제8_네이버 검색창으로 연결



```python
@app.route('/naver')
def naver():
    return render_template('naver.html')
```



```html
<h1> 네이버 검색 </h1>
<form action = "https://search.naver.com/search.naver">
  <input type = "text" name = "query">
  <input type = "submit">

</form>
```



덧, 구글에서 검색할 경우

```python
@app.route('/google')
def google():
    return render_template('google.html')
```



```html
<h1> 구글 검색 </h1>
<form action = "https://www.google.com/search">
  <input type = "text" name = "q">
  <input type = "submit" value = "구글검색!!!">

</form>
```





#### 예제9_vonvon



```python
@app.route('/vonvon')
def vonvon():
    return render_template('vonvon.html')

@app.route('/godmademe')
def godmademe():
    name = request.args.get("name")
    feature = ['유능함', '쿨함', '멋짐', '럭키', '머니']
    select = random.choice(feature)
    return render_template('godmademe.html', name_in_html = name, select_in_html = select)
```



**/ping** 

```html
<form action = "/godmademe">
    <input type = "text" name = "name">
    <input type = "submit">
  </form>
```



**/pong** 

```html
<h1>  {{ name_in_html }} 님을 만들 때는 {{ select_in_html }}를 넣었습니다! -신 </h1>
```



---

덧, feature를 더 많이 넣어볼까 (random.sample 사용)

유능함 몇 퍼, 쿨함 몇 퍼,,,, 로 발전시킬 방법은?





#### 예제10_오늘이 생일인지 판단



파이썬 시간관리 모듈 datetime이용->구글링

```python
@app.route('/bday')
def is_bday():
    today = datetime.now()
    if today.month == 10 and today.day == 14:
        result = True
    else:
        result = False
    return render_template('is_bday.html', result = result)
```



```html
{% if result == True %}
    <h1> 생일 축하드려요 !! </h1>
{% else %}
    <h1> 오늘은 생일이 아니네요 ㅎㅎ </h1>
{% endif %}
```





#### 예제11_미세미세



API란 상호작용할 수 있는 수단, 인터페이스

#대기오염정보 공공데이터 #공식문서



미세먼지 api_key

~~18sdqPnoqMEjN5FERbhv5tqJ%2BJzN7VX%2FMWseSnqgnxjcMc6rqTp%2FJZnI%2ByGiQo5ep9WI6%2F9oVMoqrMhvlHyCdA%3D%3D~~

url(요청) end point

~~http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey={api_key}&numOfRows=40&pageNo=1&startPage=3&sidoName=서울&ver=1.6~~



requests.get() 코드로 요청을 보냄 -> 200을 받으면 정상적으로 요청된 것

items->list로 값이 담겨져 옴

강남구 미세먼지 정보를 찾기 위해 -> 27번 인덱스 검색



```python
@app.route('/dust')
def dust():


    api_key = '18sdqPnoqMEjN5FERbhv5tqJ%2BJzN7VX%2FMWseSnqgnxjcMc6rqTp%2FJZnI%2ByGiQo5ep9WI6%2F9oVMoqrMhvlHyCdA%3D%3D'
    url = f'http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey={api_key}&numOfRows=40&pageNo=1&startPage=3&sidoName=서울&ver=1.6'

    response = requests.get(url).text
    data = BeautifulSoup(response, 'html.parser')

    items = data.find_all('item')
    location = items[27]

    gangnam_dust = location.pm10value.text
    gangnam_dust = int(gangnam_dust)

    if gangnam_dust > 150:
        dust_rate = '매우나쁨'
    elif 80 < gangnam_dust <= 150:
        dust_rate = '나쁨'
    elif 30 < gangnam_dust and gangnam_dust <= 80:
        dust_rate = '보통'
    else:
        dust_rate = '매우좋음'

    today = datetime.now()

    return render_template('dust.html', dust_rate = dust_rate, today = today)

```



```html
<h1> {{ today.month }}월 {{ today.day }}일 {{ today.hour }}시, </h1>
<h1> 강남구 미세먼지 농도는 {{ dust_rate }} 입니다!</h1>
```



---

template 안에는 html 파일만 들어있어야

파이썬 파일(api_practice.py)은 상위 카테고리에 있어야  render_template 작동함



#### 예제12_



http://127.0.0.1:5000/ 

127.0.0.1 : localhost(내 컴퓨터)

배포, deploy : 상대 컴퓨터로 옮겨놓는 작업



pythonanywhere

ynjn

14





### 문서화

잘 만든 API는 문서화가 잘 되어있음

공식 문서를 읽고 스스로 학습하는 능력이 중요

tensor flow 문서화 굿굿