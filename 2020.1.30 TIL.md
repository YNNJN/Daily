## 2020. 1. 30 TIL





- 팰린드롬

```python
def palindrome(word):
    for i in range(len(word)//2):
        if word[i] != word[-i-1]:
            return false
        elif i == len(word)//2:
            break

    result = True
    return result



#M2 함수를 return word == word[::-1]
```

- [slice notation](https://stackoverflow.com/questions/509211/understanding-slice-notation)

```python
a[::-1]    # all items in the array, reversed
```









### 메소드

- 어떤 객체에서만 사용할 수 있는 함수 (리스트의~, 문자열의~ )
- 그 앞의 자료형 파악이 먼저





### 문자열 메소드



#### 변형

- 문자열에 대한, ~로 만들어 반환하는 메소드
- ~로 만들어 반환한다 <- 반환값을 저장하지 않으면 원본이 변하지 않음
  <- 결과 값을 저장할 변수가 필요. 함수의 호출만이 아닌 실행이 필요
- 혹은 원본 자체를 바꾸는 메소드도 있음
- .capitalize(), .title(), .upper(),
- .lower(), .swapcase()
- .join(iterable),  .replace(old, new[,count])

- strip([chars])

  - rstrip(), 우측부터 읽어들여서 () 안의 스트링으로 조합 가능하면 삭제

  ```python
  'coding....is.......fun'.rstrip('codeisfun.')
  'mississippi'.rstrip('pis')
  ```



#### 탐색 및 검증

- .find(x), .index(x)
  - 둘 모두 x의 첫 번째 위치를 반환. 없을 경우 find는 -1을 반환, index는 오류가 발생

- split()
  - 안에 있는 값을 기준으로 문자열을 잘라서 반환



#### 메소드 확인

- 문자열에서 쓸 수 있는 모든 메소드를 알 수 있음

```python
dir('string')
```

- 메소드가 어떻게 동작하는지 출력해줌

```python
'string'.join.__doc__
```



#### 판별

- .isalpha()
  - 안에 담긴 값이 모두 알파벳인지를 판별하는 메소드
- .isdecimal()
  - 안에 담긴 값이 10진수로 표현되어 있는지를 판별하는 메소드
- .isdigit()
  - 안에 담긴 값이 모두 숫자인지를 판별하는 메소드

- .isnumeric()
  - 안에 담긴 값이 모두 숫자인지를 판별하는데, .isdigit에서 추가로 ½와 같은 유니코드까지 판별해줌
- .isupper()







### 리스트 메소드



#### 값 추가 및 삭제

- .append(x), .extend(iterable)

  - append는 list로 인자를 줄 때 리스트를 통째로 추가, extend는 개별적으로 추가
  - list concatenate로 extend와 동일한 작업 수행 가능

  ```python
  cafe += ['tera', '빽']
  print(cafe)
  ```

- 문자열도 반복을 돌릴 수 있으니, extend의 인자로 starbucks를 주면 알파벳 각각이 리스트의 원소로 추가됨



- insert(i, x)

```python
#가장 뒤가 아님. i값 전에 insert가 되니까
cafe.insert(-1, 'bye')
print(cafe)

#가장 뒤는 이 방법으로
cafe.insert(len(cafe), 'bye')
print(cafe)
```

```python
# 리스트의 길이를 넘어서는 인덱스는 마지막에 아이템이 추가됨
cafe.insert(100, '!')
print(cafe)
```



- .remove(x)
  - 좌측부터 한 번에 하나 씩만 삭제가 됨
  - 값이 없으면 오류가 발생
- .pop(i)
  - 값이 return이 된다는 것은 별도의 변수에 저장할 수 있다는 것
- .clear(), .index(x), .count(x)

- .sort()

```python
#내림차순으로 정렬
lotto.sort(reverse = True)
print(lotto)
```

- sort와 sorted
  - .sort()는 내장함수 sorted()와는 달리 메소드로서 원본 list를 변형시키고, None을 리턴함
  - 원래 있는 값을 정렬시켰기 때문에, 어떤 값도 반환하지 않음

```python
result = lotto.sort()
print(result)

# output : None
```

- reverse()
  - 반대로 뒤집음. 정렬해주진 않음





#### 복사

- 리스트와 딕셔너리의 경우 새로운 리스트에 리스트를 대체 시 id값이 같음

- 숫자의 경우 인덱스 값이 다름



- original_list와 copy_list의 프레임이 같은 리스트(객체)를 가르키고 있기 때문에,
  copy_list의 값을 바꾼다는 것은 original_list의 값을 바꾸는 것을 의미

```python
original_list = [1, 2, 3]

copy_list = original_list
print(copy_list)

#output: [1, 2, 3]

copy_list[0] = 5
print(original_list)

#output: [5, 2, 3]
```



- copy의 값을 바꾸지 않고 복사하기 위해서는 다음의 방법으로 시도(**shallow copy**)

```python
#안바뀜
a = [1, 2, 3]
b = a[:]

b[0] = 5
print(a)

#output: [1, 2, 3]

#안바뀜
a = [1, 2, 3]
b = list(a)

b[0] = 5
print(a)

#output: [1, 2, 3]
```



- 위와 같은 방법이지만 2차원 배열을 copy할 경우

```python
#바뀌어버림
a = [1, 2, [1, 2]]
b = a[:] #[1, 2, [1, 2]]

b[2] # [1, 2]
b[2][0] = 3
print(a)

#output: [1, 2, [3, 2]]
```



- 이렇듯 중첩된 상황에서 복사를 하고싶다면 다음의 방법으로 시도(**deep copy**)
  - 즉  내부에 있는 모든 객체까지 새롭게 값이 변경됨
  - deep copy는 아예 원본을 건들지 않음

```python
#안바뀜
import copy

a = [1, 2, [1, 2]]
b = copy.deepcopy(a)

b[2][0] = 3
print(a)

#output: [1, 2, [1, 2]]
```









#### list comprehension

- 코드를 파이써닉하게 짤 수 있는 방법

- 조건문에 참인 식으로 리스트를 생성함

  - ```python
    [식 for 변수 in iterable if 조건식]
    ```

  - ```python
    [식 if 조건식 else 식 for 변수 in iterable]
    ```

- elife는 이렇게

  - ```python
    [식 if 조건식 else 식 if 조건식 else 식 if ... else ... for 변수 in iterable]
    ```





- (1~10까지의 숫자로 만든 세제곱이 담긴 리스트)

```python
cubic_list = []

for i in a:
    cubic_list.append(i**3)
print(cubic_list)
```

```python
cubic_list = [x**3 for x in a]
print(cubic_list)
```



- 조건은 뒤에 걸면 됨

```python
even_list = []
for i in range(1, 11):
    if i % 2==0:
        even_list.append(i)
    
print(even_list)
```

```python
even_list = [x for x in range(1, 11) if x % 2 == 0]
print(even_list)
```







- 곱집합 -> append를 튜플로 받아서 pair 리스트를 작성할 수 있음



- 반복문을 이용

```python
member = []

for boy in boys:
    for girl in girls:
        member.append((boy, girl))
        
print(member)
```

- list comprehension 이용

```python
member = [(boy, girl) for boy in boys for girl in girls]
print(member)
```

-> list comprehension이 조금 더 빠름









- 모음 제거하기
- M1

```python
vowel = ['a', 'e', 'i', 'o', 'u']
l = []
for i in words:
    if i not in vowel:
        l.append(i)
    
print(''.join(l))
```

- M2

```python
words = list(words)
vowel = ['a', 'e', 'i', 'o', 'u']

for vow in vowel:                #for는 vowel의 길이인 5번만 반복됨. words에는 모음이 5번 이상 있으므로 원하는 결과를 얻을 수 없음
    if vow in words:
        words.remove(vow)
        
print(''.join(words))
```

- M3

```python
result = []
vowels = ''
for x in words:
    if x in vowels:
        continue
        #result += ''
    else:
        result.append(x)
        
print(''.join(result))
```

- list comprehension

```python
vowels = 'aeiou'
result = [x for x in words if x not in vowels]
print(''.join(result))
```









오늘의 뿌듯함

- 연속적인 숫자 제거 짧게 풀었당

```python
def lonely(nums):
    result = [0]
    
    for num in nums:
        if num != result[-1]:
            result.append(num)
    
    result.pop(0)
    
    return result
```



- 까리한 코드, for~else

```python
checks = ['s', 'a', 'f', 'y']
for word in words:
	if word in checks:
		return True
else:
	return False
```





- list에 int를 넣지 못하는 문제는 append 를 이용해 해결

- *= 도 쓸 수 있구나
- %10 하면 각 자리마다 꺼낼 수 있으니

- 가변인자로 받은 값의 형태는 튜플

- 마지막 조건을 만족할 때까지~ ->재귀의 향기

