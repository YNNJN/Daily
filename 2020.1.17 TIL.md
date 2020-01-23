## 2020. 1. 17 TIL



### 챗봇 프로젝트



웹은 브라우저를 통해 요청을 보내고

챗봇 프로그램에서는 브라우저가 아닌 채팅창을 통해 요청을 보냄

`텔레그램 앱 <-> 텔레그램 서버 <-> 플라스크(우리 서버)`

우리 서버와 텔레그램 서버가 소통할 수 있게 하는 것이 오늘의 목표

@botfather -> 명령어 알려줌





#### 1. 토큰 to access the HTTP API 제공받기:



(공식문서의 making requests 참고)

1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo

베이스 url:	(공식문서의 authorizing your bot 참고)

https://api.telegram.org/bot1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo/getMe

해당 페이지의 텍스트를 예쁘게 보이게 하는 플러그인:

크롬 웹스토어-**JSON** 설치 -> 딕셔너리 형태의 페이지가 출력됨



**JSON** (JavaScript Object Notation) 이란 자스에서 객체를 만들 때 사용하는 표현식을 의미

서버와 웹 응용 프로그램간에 구조화 된 데이터를 직렬화하고 전송하는 데 사용되는

텍스트 기반의 개방형 표준 형식. 사람이 읽고 쓰는 것이 쉽고 특정 언어에 종속 X

OPEN API 대부분 JSON을 활용하여 데이터를 주고 받음.





#### 2. 채팅방의 ID값 찾기:



(공식문서의 getting updates 참고)

https://api.telegram.org/bot1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo/getUpdates

**chat_id : 890267444**





#### 3. 챗봇이 메시지 보내기:



(공식문서의 available mothods 참고)

https://api.telegram.org/bot1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo/sendMessage?chat_id=890267444&text=heyhey

?chat_id=890267444&text=heyhey에서 물음표 뒤의 값은

-> **id**와 **text**(공식문서에서 requirement로 요구한 두 값)





#### 4. /ping /pong 방식 이용해서 파이썬 코딩:



3에서 웹브라우저가 하던 일을 파이썬이 할 수 있도록 함

구체적으로는 requests를 이용해서. requests.get(message_url) -> 브라우저로 코드를 입력하는 역할



파일 이름 app.py -> set Flask_APP의 명령어 두 줄 입력할 필요 없음. hello.py와 달리.

templates 폴더 만들어서 html 파일들이 폴더 하에 위치하도록 함

`윈도우` + `.` -> 이모지 입력 가능



#app.py

```python
from flask import Flask, render_template    #이렇게 한 줄로 쓰기도 가능
from flask import request
import requests
#from flask import render_template
app = Flask(__name__)

token = '1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo'
app_url = f'https://api.telegram.org/bot{token}'    #기니까, f스트링 사용해서 분리
chat_id = '890267444'


@app.route('/')
def hello():
    return 'Hello World!'


@app.route('/write')
def write():
    return render_template('write.html')


@app.route('/send')
def send():
    text = request.args.get('message')
    message_url = f'{app_url}/sendMessage?text={text}&chat_id={chat_id}'
    requests.get(message_url)
    return render_template('send.html')


if __name__== '__main__':
    app.run(debug=True)
```



#write.html

```html
<h1> Telegram </h1>

<form action = "/send">

    <input type = "text" name = "message">
    <input type = "submit" value = "메시지전!송!👏👏👏">

</form>
```



#send.html

```html
<h1> 메시지가 성공적으로 전송되었습니다 🙌 </h1>
<a href="/write"> 다시 보내기 </a>  <!--메시지 전송 후 다시 보내기 버튼 클릭하면 write 페이지로 돌아옴-->
```



---



##### 추천 툴

**slack** 채팅(코드입력 가능)

**trello** 태스크관리



---





#### + id 값을 코드로 찾아가는 과정



telegram api에서 바로 긁어오는 것은 개발자답지 않으니,

한꺼풀씩 벗겨오는 연습

'result-0-message-chat-id'의 순서로 타고 들어가 최종으로 id 값이 출력됨



#send_message.py

```python
import requests
import pprint

# 1. 기본 설정
token = '1011959547:AAH3fCkSL71ephoUVuRR6BWbvtGLDfYliBo'
app_url = f'https://api.telegram.org/bot{token}'

# 2. getUpdates 요청하기
update_url = f'{app_url}/getUpdates'
response = requests.get(update_url).json()           #text 대신 json 삽입. 후자에 따옴표가 있는 것이 차이

data = response['result'][0]['message']['chat']['id']        #첫 번째 값만 출력되니 cmd 출력값에 [ ]가 없어짐
text = 'Thank you'

#3. 텔레그램으로 메시지 보내기
message_url = f'{app_url}/sendMessage?text={text}&chat_id={data}'
requests.get(message_url)
```





#### + 토큰을 비공개하는 방법



cmd에서 pip install python-decouple

민감한 정보들을 환경변수로 뺌

파일명 앞 '.'은 일반적으로 숨김 파일

.env 파일에서 띄어쓰기가 있으면 안됨

app.py 파일에서 from decouple import config 하면 -> config 함수가 변수명을 숨김파일을 포함해서 찾아서 변수로 넣어줌



그리하여 토큰을 숨긴 코드는 다음과 같음.

다시 #app.py

```python
from flask import Flask, render_template    #이렇게 한 줄로 쓰기도 가능
from flask import request
import requests
from decouple import config

#from flask import render_template
app = Flask(__name__)

token = config('TELEGRAM_BOT_TOKEN')
app_url = f'https://api.telegram.org/bot{token}'    #기니까, f스트링 사용해서 분리
chat_id = '890267444'


@app.route('/')
def hello():
    return 'Hello World!'


@app.route('/write')
def write():
    return render_template('write.html')


@app.route('/send')
def send():
    text = request.args.get('message')
    message_url = f'{app_url}/sendMessage?text={text}&chat_id={chat_id}'
    requests.get(message_url)
    return render_template('send.html')


if __name__== '__main__':
    app.run(debug=True)
```







#### 5. 텔레그램 웹훅 받기



`텔레그램 앱 <-> 텔레그램 서버 <-> 플라스크(우리 서버)`

지금은 봇에 빙의해서 메시지 보내는 중

webhook: 정방향 두 번 전달이 가능하게 하는 기술

​			텔레그램 서버에 메시지가 들어오면 플라스크 서버로 전달하라고 말하는 역할

외부사람이 로컬호스트에 접속할 수 있게 하여 텔레그램이 훅을 걸 수 있도록 할 것





챗봇과 메시지를 주고 받을 때보다 안그럴 때가 더 많다면 자원 낭비

그래서 **텔레그램**은 **웹훅**(webhook)이란 기능을 제공함



- [webhook](https://core.telegram.org/bots/api#making-requests) 에 요청을 하면 True를 보내줌

훅을 걸어서 /telegram으로 다 보내줘

HTTP response code -> 숫자에 따라 누가 잘못했는지 알 수 있음



- [ngrok](https://ngrok.com/)

ngrok 설치, 압축 푼 파일 위치에서, cmd에 'ngrok http 5000' 입력

forwarding: 직접 못 전달하니까 ~~어떤~~ 사이트를 경유해서 로컬호스트로 '전달해줘'를 말함

이 때 계속 주소가 바뀌는 ~~어떤~~ 사이트가 존재함

https://761b070a.ngrok.io





##### setWebhook

> Use this method to specify a url and receive incoming updates via an outgoing webhook. Whenever there is an update for the bot, we will send an HTTPS POST request to the specified url, containing a JSON-serialized [Update](https://core.telegram.org/bots/api#update). In case of an unsuccessful request, we will give up after a reasonable amount of attempts. Returns *True* on success.
>
> If you'd like to make sure that the Webhook request comes from Telegram, we recommend using a secret path in the URL, e.g. `https://www.example.com/`. Since nobody else knows your bot‘s token, you can be pretty sure it’s us.

*methods = ['POST']의 의미 추후 공부하기





웹훅이 잘 걸렸는지, 응답을 프린트해서 확인

```python
from decouple import config
import requests

token = config('TELEGRAM_BOT_TOKEN')
app_url = f'https://api.telegram.org/bot{token}'
ngrok_url = 'https://761b070a.ngrok.io'

set_webhook_url = f'{app_url}/setwebhook?url={ngrok_url}/telegram'              #app.py에 있는 바로 그 경로 /telegram

response = requests.get(set_webhook_url)
print(response)
```

> "ok":true,"result":true,"description":"Webhook is already set"





---

**request**와 **requests**

- 둘 다 모듈은 맞음
- request는 플라스크에서 제공해주는 모듈. 요청에 대한 정보들이 담겨져서 옴.
- requests는 브라우저에서 검색과 엔터를 대신해주던 모듈. 다른 사람이 만듦.







#### 6. echo-echo 실습



아래 코드에서 텔레그램에 메시지를 입력하면

-> json에서의 값을 cmd창에 정리(pprint)해서 보여줌

#app.py

```python
import pprint

@app.route('/telegram', methods = ['POST'])
def telegram():
    print(request.get_json())                       #안에 담긴 내용 확인
    pprint.pprint(request.get_json())

    return '', 200
```



##### text만 추출

가장 상단의 message를 먼저 뽑아봤더니 나머지 다섯 개 딕셔너리가 같은 선상에 위치하니

이후 text를 바로 뽑을 수 있음

```python
@app.route('/telegram', methods = ['POST'])
def telegram():

    response = request.get_json()
    text = response['message']['text']
    pprint.pprint(text)

    return '', 200
```



##### from-id 추출

```python
@app.route('/telegram', methods = ['POST'])
def telegram():

    response = request.get_json()
    chat_id = response['message']['from']['id']

    pprint.pprint(chat_id)

    return '', 200
```



##### 텔레그램이 내 말 따라하게 하기

```python
@app.route('/telegram', methods = ['POST'])
def telegram():

    response = request.get_json()
    text = response['message']['text']
    chat_id = response['message']['from']['id']

    echo_url = f'{app_url}/sendMessage?chat_id={chat_id}&text={text}'
    requests.get(echo_url)                  #메시지를 보낼 때마다 이 url로 텔레그램으로 메시지를 전달해줌

    return '', 200
```



---

메시지를 보낼 때마다 이 url로 텔레그램으로 메시지를 전달해줌

내가 쓴 text를 내 서버 chat_id로 가져다주니까.

text = {text}, 중괄호 안의 값을 다른 값으로 바꾸면? 







#### 7. 파파고 실습



1. 애플리케이션 다운

파파고 api-네이버 개발자 센터-파파고 api 다운-애플리케이션 등록

naver_id: vLvurpWWM1MwRksmocX1

naver_secret: 3lVfqI2W2l



2. 명세대로 요청

[파파고명세](https://developers.naver.com/docs/nmt/reference/)

source, target, text 담아서 보내기 (대상, 결과, 텍스트)

[파파고API예제코드파이썬](https://developers.naver.com/docs/nmt/examples/#python)

은 import urllib.request를 사용하니, 해당 코드를 직접 사용하지는 않음

 import urllib보다는 import requests 사용을 권장함



API기본 정보:

https://openapi.naver.com/v1/papago/n2mt



**requests.get**과 **requests.post**

- get은 어떤 정보를 받고 싶을때

- post는 내가 정보를 보낼테니 처리해줘



3. 텔레그램에 메시지 보내서 /번역



cmd 창의 출력값인 translatedText 변수 뽑아오기

#app.py

```python
@app.route('/telegram', methods = ['POST'])
def telegram():

    response = request.get_json()
    text = response['message']['text']
    chat_id = response['message']['from']['id']

    if response.get('message') is not None:            #키 에러에 대한 예외처리 위해

        if text[0:4] == '/번역 ':                       #슬라이싱
            papago_url = 'https://openapi.naver.com/v1/papago/n2mt'
            data = {'source': 'ko', 'target': 'en', 'text': text[4:]}
            headers = {
                'X-Naver-Client-ID': naver_client_id,             #요청예시 참고
                'X-Naver-Client-Secret': naver_client_secret
            }
            response = requests.post(papago_url, headers = headers, data = data).json()       
            text = response['message']['result']['translatedText']

        send_url = f'{app_url}/sendMessage?chat_id={chat_id}&text={text}'
        requests.get(send_url)

    return '', 200
```





**키 에러에 대한 예외 처리 -> 키가 없어도 에러가 발생하진 않을 것**

딕셔너리에 키 값이 없으면 key error 남

딕셔너리에서 값을 가져오는 방법 1. [ ] 	2. response.get() 

response['message']

response.get('message').get('from').get('id')

이 둘이 같은 의미래. 이해는 못했음



---

- response[' '] [' '] [' ']에서 json의 카테고리들을 계속 타고들어갈 수 있는 이유?
  아 딕셔너리에서 키 값을 저렇게 뽑아주지 참

- text 변수를 두 번 지정해도 되는 이유? 후에 저장된 값이 꺼가 최종이니까





아래 코드 추가해서 로또 번호 텔레그램이 보내주는 코드도 작성해봄

```python
if text[0:3] == '/로또':
	lotto = random.sample(range(46),6)
    text = f'이번 주 행운의 번호는 {lotto}입니다!!'
```



변수 text 역할:

text에 저장한 변수 값이 텍스트로 함수 telegram을 통해 바로  출력됨







#### 8.미세미세



어제 만든 미세미세도 옮겨줌

```python
if text[0:5] == '/미세먼지':

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
            text = f'오늘의 미세먼지 수치는 {dust_rate}입니다!!!'



        send_url = f'{app_url}/sendMessage?chat_id={chat_id}&text={text}'
        requests.get(send_url)
```



코드 그대로 옮겨주되, 사용한 모듈 모두 import 해주고, text로 f스트링 챗봇 형식에 맞게 바꿔줄 것







#### 9. 배포



배포하면서 플라스크 서버의 주소가 바뀌었기 때문에 훅을 다시 걸어줘야



#set_webhook.py에서 배포한 주소로 훅 변경

```python
python_anywhere_url = 'ynjn.pythonanywhere.com'
set_webhook_url = f'{app_url}/setwebhook?url={python_anywhere_url}/telegram'
```







---

다른 봇으로 응용해보기(if 형식으로 추가 가능)