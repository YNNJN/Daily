## 2020.2.19 TIL







### 딕셔너리 메소드

- .pop(key[, default])

- .update()

- .get(key[, default])



- Dictionary comprehension까지 가능함

```python
dusts = {'서울': 72, '대전': 82, '구미': 29, '광주': 45, '중국': 200}
result = {key: value for key, value in dusts.items() if value > 80}
print(result)
```

- if else

```python
result = {key: '나쁨' if value > 80 else '보통' for key, value in dusts.items()}
print(result)
```







### 세트 메소드

- add(elem)
- .update(*others)
  - 반드시 이터러블한 값을 넣어야
- .remove(elem)
  - 값이 세트에 없으면 키에러가 발생
- .discard(elem)
  - 값이 없어도 에러가 발생하지 않음
- pop()
  - 임의의 원소를 제거해 반환







### map(function, iterable)

- 리스트의 값을 스트링으로

```python
#리스트 내포 
new_numbers = ''.join([str(num) for num in numbers])
print(new_numbers)

#맵 이용
new_numbers = ''.join(map(str, numbers))
print(new_numbers)
```



- 리스트 안의 스트링 값을 인트로

```python
#리스트 내포
new_numbers = [int(num) for num in numbers]
print(new_numbers)

new_numbers = sum([10**idx * int(num) for idx, num in enumerate(numbers[::-1])])
print(new_numbers)

#맵 이용
new_numbers = list(map(int, numbers))
print(new_numbers)

#맵에 int, str 아닌 내가 정의한 함수도 인자로 사용 가능
```







### zip(*iterables)

- 짝지어주기

```python
#딕셔너리 내포

{girl: boy for girl in girls for boy in boys}
#마지막 보이가 덮어씌워짐. 아래의 반복문과 동일한 표현

#집 이용

pair = {girl: boy for girl, boy in zip(girls, boys)}
print(pair)
```

```python
a = '123'
b = '567'
for digit_a, digit_b in zip(a,b): #두 시퀀스의 길이가 같아야 사용 가능
    print(digit_a, digit_b)
    
num1 = [1,2,3,]
num2 = ['1', '2']
list(zip(num1, num2))
```







### filter(function, iterable)

- iterable에서 함수의 반환 결과가 참이 것만 구성하여 반환

```python
#리스트 내포

[x for x in numbers if odd(x)]
[x for x in numbers if x % 2]

#filter 이용

def odd(n):
    return n % 2
numbers = [1,2,3]
result = list(filter(odd, numbers)) #맵과 사용 방법 유사
print(result)
```









### 모듈

- 파이썬 정의와 문장들을 담고 있는 파일



```python
#이 폴더를 모듈로 쓰겠다

myPackage/
    __init__.py
    math/
        __init__.py
        formula.py
    web/
        __init__.py
        url.py
```

```
#터미널에서 모듈 만들기

ls
cd myPackage
touch __init__.py #파일 만듦
cd math
touch __init__.py
touch formula.py
cd..
cd web
touch __init__.py
touch url.py
```





- from~ import 하나만 가져옴, 특정 함수 혹은 어트리뷰트만 활용하고 싶을 때

- import random 난수 <- 메르센 트위스터 알고리즘으로 구현 (유사난수생성기)

- is it christmas 크롤링

- divmod() -> 튜플로 몫과 나머지 반환

- 모듈이 다른 모듈에게 임포트되어 사용되면, 그것은 더이상 메인이 아니게 됨

```python
if __name__ == '__main__': #모듈의 이름을 담는 변수
    print('직접 실행할 경우만 실행됩니다')
    print(__name__)
    my_max(3,5)

#__name__ 모듈의 이름, 실행시 name이 main이 됨
```







### 패키지

- 패키지는 '점으로 구분된 모듈 이름' 을 써서 파이썬의 모듈 이름 공간을 구조화하는 방법. 예를 들어, 모듈 이름 `myPackage.math`는 `myPackage`라는 이름의 패키지에 있는 `math`라는 이름의 서브 모듈을 가리킴
- 단, 파이썬이 디렉터리를 패키지로 취급하게 만들기 위해서 `__init__.py` 파일이 필요함. 이렇게 하는 이유는 string 처럼 흔히 쓰는 이름의 디렉터리가, 의도하지 않게 모듈 검색 경로의 뒤에 등장하는 올바른 모듈들을 가리는 일을 방지하기 위함







### Errors

- KeyboardInterrupt: 프로그램이 돌아가고 있는데 내가 개입을 해서 껐을 때 발생하는 오류

- Traceback: 에러를 저장하는 파이썬의 객체

```python
import sys
import traceback

tb = sys.last_traceback
traceback.print_tb(tb)
print(tb)
```

-> (위에서 떴던 에러가 저장되어있음)







### Except

- **에러가 순차적으로 수행되**므로, 가장 작은 범주부터 시작해야

- raise는 예외를 강제로 발생시킴







### assert

- 조건이 거짓일 경우 예외를 발생시킴
- 코드를 테스트 할 때 많이 사용

```python
username = ''
password = ''

def signup_test(username, password):
    assert username != password, '아이디와 비밀번호가 달라야 합니다'
    print('회원가입완료')
    return username, password
username, password = signup_test('YNNJN', 'YNNJN')
```





### csv

- comma-separated values
- 몇 가지 필드를 쉼표로 구분한 텍스트 데이터 및 텍스트 파일. 확장자는 .csv
- 스프레드시트나 데이터베이스 소프트웨어에서 많이 쓰였으나, 세부 구현은 소프트웨어에 따라 다름



``` python
#lunch.py
#csv open/close

import csv

lunch = {
    '양자강': '02-557-4211',
    '세븐브릭스': '02-488-4744',
    '멀캠': '02-0000-2424'
}

with open('lunch.csv', 'w', encoding = 'utf-8', newline = '') as csvfile:
    csv_writer = csv.writer(csvfile)
    for item, number in lunch.items():
        csv_writer.writerow([item, number])
        
# #open/close는 번거로우니
# csvfile = open('lunch.csv', 'w', encoding = 'utf-8', newline = '') #파일이 자동 생성됨
# csv_writter = csv.writer(csvfile)

# for item, number in lunch.items():
#     csv_writter.writerow([item, number])

# csvfile.close()
```



- import module - requests와 Beautifulsoup

- parsing 구문분석, 파이썬이 알아듣기 쉽도록 구조를 바꿔주는 것 -> bs

- 크롤링 시 개발자도구-선택-copy-copy selector

- 태그에는 계층관계가 존재 - 들여쓰기로 구분



``` python
#daum_ranking.py

import requests
from bs4 import BeautifulSoup
from pprint import pprint
import csv

url = 'https://www.daum.net'

response = requests.get(url)
response = response.text
data = BeautifulSoup(response, 'html.parser')

result = data.select('#mArticle > div.cmain_tmp > div.section_media > div.hotissue_builtin > div.realtime_part > ol > li > div > div > span') #실행시 리스트에 태그가 담겨서 보여짐
# print(result[0].text)

# result_dict = {}
result_list = []
for i in range(0, len(result), 4):
    rank = result[i].text
    keyword = result[i+1].text
    
    result_dict = {'rank': rank, 'ranker': keyword} #rank와 ranker가 테이블의 헤더가 됨
    result_list.append(result_dict)
    # result_dict[rank] = keyword #rank를 키로, keyword를 밸류로 하는 딕셔너리 출력

with open('daum_rank.csv', 'w', encoding='utf-8', newline='') as csvfile:
    fieldnames = ('rank', 'ranker')
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()
    for item in result_list:
        writer.writerow(item)


    # csv_writer = csv.writer(csvfile)
    # for item, value in result_dict.items():
    #     csv_writer.writerow([item,value])
```



``` python
#daum_read.py

import csv

with open('daum_rank.csv', 'r', encoding = 'utf-8', newline = '') as csvfile:
    reader = csv.DictReader(csvfile) #DictReader라는 객체를 만드는 행
    for row in reader: #각각의 row가 딕셔너리 형태로 오기 때문에 키로 접근해서 읽을 수 있는 것
        print(row['rank'], row['ranker'])
```



- JSON 배열: 가장 바깥에 리스트, 그 안에 딕셔너리, 그 안에 키와 밸류가 있는 구조



- 파일 쓰고 읽고, DictWriter / DictReader

- HW) 멜론차트 - 순위, 노래제목, 가수이름 -> csv 파일로 저장