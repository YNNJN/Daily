## 2020.1.21 TIL



- 'num % 2 ==1' 이 더 명확해보이지만, 개발자들은 '==1' 생략을 선호
  - 1이 참을 의미하니까, 조건문을 참으로 하는 조건의 생략이 가능하다.

```python
if num % 2:                            #if num % 2==1과 같다
    print('홀수입니다.')
else:
    print('짝수입니다.')
```





- 조건 표현식
  - 조건에 따라 값을 정할 때 많이 활용함

```python
true_value if <조건식> else false_value
```





- 사용자가 "안녕"이라고 입력할 때까지 인사하는 코드를 작성

1.

```python
greeting = ''
    
while greeting != '안녕':
    print('안녕. 그렇지만 다시 인사해주세요')
    greeting = input('말해봐:  ')
```

2.

```python
while input()[0:2] != '안녕':
    print('다시 말해주세요')
print('안녕')
```





- `for` 문에서 요소 값에 다른 값을 할당해도 다음 반복구문에 영향을 주지 않음
- 즉 덮어씌워지지 않음





- `enumerate()`를 활용하면, 추가적인 변수를 활용할 수 있음

1. list(enumerate())

```python
classroom = ['kwon', 'kim', 'jung']
class_list = list(enumerate(classroom))
print(class_list)
```

-> 짝이 지어져서 튜플로 반환됨 [(0, 'kwon'), (1, 'kim'), (2, 'jung')]



2. for idx, in enumerate()

```python
lunch = ['짜장면', '초밥']
for idx, menu in enumerate(lunch, start = 1):
    print(idx, menu)
```

-> 1 짜장면 2초밥



​	3. for idx, name in enumerate(names):

​	아래 알고리즘 풀이 참고





- dictionary에서 `for` 활용하는 4가지 방법 정리

```python
#0. dictionary (key 반복)
for key in dict:
	print(key)
	
#1. key 반복
for key in dict.keys():
	print(key)
	
#2. value 반복
for val in dict.values():
	print(val)
	
#3. key와 value 반복
for key, val in dict.items():
    print(key, val)
```





- 이 꼴에 익숙해지고 싶다 for char in chars:

```python
chars = input('문자를 입력하세요 : ')

for char in chars:
    print(char)
```





- `range()` 가 돌려준 객체(iterable)는 리스트인 것 같지만, 리스트가 아니다.

  input: print(range(10)), 	output: range(0, 10)
  input: list(range(10)), 	output: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

  



- `continue`와 `pass`

  - continue는 loop에서 현재 행 이하의 구문은 실행 하지 않고 loop의 시작지점으로 돌아갈 경우 사용.

  - pass는 단순히 특별한 소스코드가 없고 지나갈 때 사용한다.

  

  -> continue는 실제로 코드에 영향을 줌

  ```python
  for i in range(5):
      if i == 3:
          continue
      print(i)
  ```

  - output: 0 1 2 4

  

  -> pass 가 없으면 에러가 뜸. 실행에서는 아무것도 하지 않지만. 문법적으로 문장이 필요한 경우에 사용

  ```python
  for i in range(5):
      if i == 3:
          pass
      print(i)
  ```

  - output: 0 1 2 3 4

  

  

  

  

  http://localhost:8890/notebooks/02_control_of_flow_00.ipynb

  

  1. 상승장 문제

  data는 딕셔너리, opening_price는 키 값인 경우

  data['opening_price'] 딕셔너리에서 키 값의 밸류 가져오기

  

  2. 모음 빼고 출력하기 문제

  문자열 내에서만 비교 연산 카운트 처리하고 싶을 때는 굳이 리스트 만들 것 없이 

  빈 스트링을 초기값으로 주면 됨

  

  3. 과일 개수 골라내기 문제

  basket_items는 딕셔너리, fruits는 리스트로 주어졌을 때

  basket_item, fruit을 새로운 변수로 설정 <- 이 꼴과 친해지고 싶다

  ```python
  basket_items = {'apples': 4, 'oranges': 19, 'kites': 3, 'sandwiches': 8}
  fruits = ['apples', 'oranges', 'pears', 'peaches', 'grapes', 'bananas']
  
  fruit, no_fruit = 0, 0
  
  for basket_item in basket_items:	#딕셔너리의 키 값
      if basket_item in fruits:		#리스트 값과 딕셔너리 키 값이 같은 것이 있는지
          fruit += basket_items[basket_item]	#딕셔너리[키값]=밸류 값을 fruit 수에 더함
      else:
          no_fruit += basket_items[basket_item]	#fruit에 포함되지 않은 수는 no_fruit에 더함
          
  print(f'과일은 {fruit}개 이고, {no_fruit}개는 과일이 아닙니다.')
  ```

  

  4. 영어 이름 출력하기 문제

  enumerate 사용과 조건 가지치기 방식에 유의

  ```python
  for idx, name in enumerate(names):
      if idx == 0:
          print(name, end=' ')
      elif idx == len(names) - 1:
          print(name)
      else:
          print(name[0], end='.')
  ```

  

  

  

