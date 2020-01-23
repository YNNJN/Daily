## 2020. 1. 23 TIL



### SCOPE

- 빈 프린트 print() : 개행 역할 해줌
- 파이썬의 함수들은 1급 객체. 함수에 함수를 넘길 수 있음. 

```python
def baby(buddy):
    pacifier = '파란색'
    name = buddy()
    return f'{name}야, 여기 {pacifier} 가져가!'

def dinosaur():
    name = '공룡친구'
    return name

def rabbit():
    name = '토끼친구'
    return name

print(baby(dinosaur))
print(baby(rabbit))
```



- 정의된 함수. 함수 내부에 있는 변수는 외부에서 접근할 수 없음

- 상위함수. 함수 안에서 함수를 또 정의. 함수에서 변수가 없으면 바로 위에 있는 함수에서 변수를 찾아서 출력함
- 전역. 글로벌 스코프. 함수에 변수가 없으면 전역에 있는 변수를 갖다가 쓰게 됨. 가능은 한데 좋은 practice가 아님.

- `L`ocal scope
- `E`nclosed scope
- `G`lobal scope
- `B`uilt-in scope

- global 변수명은 해당 변수를 전역 변수의 값을 가져와서 쓰겟다는 말을 의미
  -> 알고리즘 문제 풀이에서 많이 활용함





### 재귀함수



- 재귀함수는 무한히 돌기 때문에 종료 조건이 필요함 (base case)

  pytutor, 코드를 짜면 시각화를 해줌

- 컴퓨터 내부에 스택이란 공간에, 함수를 호출할 때마다 쌓임 (파이썬은 맥스 3000)

- 이게 넘칠 때 스택 오버플로우 현상이 발생

- ```
  RecursionError: maximum recursion depth exceeded while calling a Python object
  ```

- stackoverflow

- reddit, what is recursion?











#### 문제 0.



총 카테고리의 개수

```python
print(len(development['category']))
```

python standard library에 'requests'가 있는지 여부를 tf로 출력

```python
'requests' in development['language']['python']'['python standard library']
```

bts 리더 이름 출력

```python
print(idols['group']['bts']['leader'])
```

language 를 모두 출력 --- 오답

```python
print(development['language'].keys())
```

```python
for key in development['language'].keys():
	print(key)
```

아이돌 그룹의 멤버들을 모두 출력

```python
for members in idols['groups'].value():
	for member in members['members']:
	    print(member)
```

프레임웤들의 이름과 설명을 출력

flask는 micro이다.

django는 full-functioning이다.

```python
for key, value in development['language']['python']['frameworks'].items()
	print(f'{key}는 {value}이다.')
```

오늘의 솔로 아이돌을 랜덤으로 한명만 뽑아주세요

```python
import rancom
print(random.choice(idols['solo'])
```







#### 문제1.



양수/음수/0의 비율을 각각 순서대로 출력

```python
numbers = input()
cnt_plus, cnt_minus, cnt_zero = 0, 0, 0
number = list(map(int, numbers.split(' ')))
for num in number:
	if num > 0:
		cnt_plus += 1
	elif num < 0:
		cnt_minus += 1
	elif num == 0:
		cnt_zero += 1
print(cnt_plus/len(number), cnt_minus/len(number), cnt_zero/len(number))
```







#### 문제 2.

 

justin과 neo의 카드게임. 예시 값은 카드를 낸 순서.

숫자를 비교해서 같으면 0점, 숫자가 더 크면 1점.

justin과 neo의 점수를 순서대로 출력

```python
j_grade, n_grade = 0, 0
for i, j in zip(justin, neo):
    if i == j:
        pass
    elif i > j:
        j_grade += 1
    elif i < j:
        n_grade += 1
     
print(j_grade, n_grade)

```

- *zip*(*iterable) 은 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수







#### 문제 3.



두 단어 중 중복된 알파벳의 여부를 판단하여 tf 반환하는 함수 작성

```python
def is_contain_same_alphabet(a, b):
	for i in a:
		if i in b:
			return True
		return Flase
```

