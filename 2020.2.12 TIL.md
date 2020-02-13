## 2020. 2. 12 TIL



- 자료구조: 가지고 있는 데이터를 어떻게 저장해야 효율적일지에 대한 고민으로 시작







## stack



#### 특성

- 선형구조
  - 선형구조란 자료 간의 관계가 1대 1
  - 비선형구조란 자료 간의 관계가 1대 N
- 스택에 자료 삽입 또는 꺼낼 수 있음
- 후입선출
- 주로 대칭적 자료를 판단할 때 이용 (괄호검사, 회문)





#### 스택의 구현을 위한 자료구조와 연산

- 스택의 자료구조는 자료를 선형으로 저장할 저장소를 의미, 즉 list
- 마지막 삽입 원소 위치를 top이라고 함
- 연산에는 push, pop, isEmpty, peek(top에 있는 원소를 반환)가 있음





#### 스택의 연산 과정

- top은 -1로 초기화, 인덱스 0에 첫 자료를 삽입하고, top += 1
  - top의 값(-1)만 확인하면 isEmpty를 확인 가능
- pop으로 꺼낸다는 것은, top을 하나 줄이는 것
- push로 꺼낸다는 것은, top을 하나 늘리고 stack의 top 인덱스에 원소를 삽입하는 것

- 모든 원소를 꺼내는 연산은, 스택이 비어있지 않으면 스택의 원소를 꺼내 리턴





#### 괄호검사

```python
def find_match():
    txt = input()
    s = list() #스택 생성
    for i in range(len(txt)):
        if txt[i] == '(':
            s.append(txt[i])
        elif txt[i] == ')':
            if len(s) == 0: #스택이 비어있다면
                return 0
            else:
                s.pop() #스택에서 괄호 하나를 꺼내서 버림
    #모든 반복 완료 후
    if len(s) != 0:
        return 0
    else:
        return 1

print(find_match())
```







## 재귀함수



- 아래 둘의 흐름 차이를 구분해서 알기

```python
def list_sum(k, total):
    if k < 0:
        print(total)
        return
    else:
        list_sum(k-1, total+k)

list_sum(10,0)


def list_sum2(k):
    if k == 0:
        return 0
    else:
        return k + list_sum2(k-1) #함수가 먼저 실행됨, k+와 리턴은 이후 실행
        
print(list_sum2(10))
```





- 정해진 횟수만큼 호출하기

```python
#일반적 의미상 M1이 맞고
def f(n,k):
    if k == 0:
        return
    else:
        print(n)
        return f(n+1, k-1)

f(0,5) #n:변하는 숫자, k: 지정한 횟수


#n=0일 때 아래의 형태로도 쓸 수 있음
def f(n,k):
    if n == k:
        return
    else:
        print(n)
        return f(n+1, k)

f(0,5)
```



- 정해진 조건을 만족하는지 여부 판단

```python
a = [3,7,6,2,1,4,8,5]
v = 2
def find(n,k,v): #n: 인덱스, k: 배열길이, v:찾아야하는 수
    if n == k:
        return 0
    if a[n] == v:
        return 1
    return find(n+1,k,v)
print(find(0,len(a),v))
```









- D2 1974. 스도쿠 검증 문제



- 슬라이싱을 많이 쓰는 것이 실행 시간을 늘리는 것 같아서
  슬라이싱으로 풀었던 문제를 반복문을 이용해서 자르는 방법으로 다시 풂
-  두 개 이상의 반복문을 break 해야할 땐 flag 이용할 것



```python
def sudoku_tf(a):
    standard = set(range(1, 10))
    if a != standard:
        return 0
    return 1

t = int(input())
for tc in range(1, t+1):
    arr = [list(map(int, input().split())) for _ in range(9)]

    flag = 1
    if flag:
        for i in range(9):
            row = set()
            for j in range(9):
                row.add(arr[i][j])
            if sudoku_tf(row):
                pass
            else:
                flag = 0
    if flag:
        for j in range(9):
            col = set()
            for i in range(9):
                col.add(arr[i][j])
            if sudoku_tf(col):
                pass
            else:
                flag = 0
    if flag:
        for i in range(9):
            for j in range(9):
                square = set()
                for ii in range(3):
                    for jj in range(3):
                        square.add(arr[ii][jj])
                if sudoku_tf(square):
                    pass
                else:
                    flag = 0
    if flag:
        print('#{} {}'.format(tc, 1))
    else:
        print('#{} {}'.format(tc, 0))
```





- D2 1954. 달팽이 숫자



- 또한 델타를 이용한 방법으로 다시 풀 수 있었음



```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    arr = [[0 for _ in range(n)] for _ in range(n)]

    d1 = [-1, 0, 1, 0]
    d2 = [0, 1, 0, -1]
    d = 0

    num = 1
    nr = nc = 0
    
    while num < n**2+1:
        arr[nr][nc] = num
        if nr + d1[d%4] == n or nr + d1[d%4] < 0 or nc + d2[d%4] == n or nc + d2[d%4] < 0:
            d += 1
        elif arr[nr+d1[d%4]][nc+d2[d%4]] != 0:
            d += 1
        nr += d1[d%4]
        nc += d2[d%4]
        num += 1

    print('#{0}'.format(tc))
    for ele in arr:
        print(' '.join(map(str, ele)))
```

