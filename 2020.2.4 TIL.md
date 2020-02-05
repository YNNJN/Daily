## 2020.2.4 TIL



```python
arr = [[1, 2, 3]]*3 #얕은 복사
arr = [[1, 2, 3]  for _ in range(3)] #깊은 복사, 문제 풀이 시 이것 이용
```





- 4896_색칠하기



```python
def coloring(arr, r1, c1, r2, c2, c):

    for i in range(r1, r2+1):
        for j in range(c1, c2+1):
            if arr[i][j] == 0 or arr[i][j] == c: #아무것도 칠해져 있지 않거나, 칠하려는 색인 c로 칠해져있는 조건
                arr[i][j] = c
            else:
                arr[i][j] = 3

t = int(input())
for tc in range(1, t+1):
    n = int(input())
    arr = [[0 for _ in range(10)] for _ in range(10)] #0을 채운 10*10 배열로 초기화
    for i in range(n):
        info = list(map(int, input().split()))

        coloring(arr, info[0], info[1], info[2], info[3], info[4])

        cnt = 0
        for r in range(len(arr)):
            for c in range(len(arr[r])):
                if arr[r][c] == 3:
                    cnt += 1
    print('#{} {}'.format(tc, cnt))
```



- 범위와 너비 -> 카운팅하는 아이디어







- D3 4839. 이진탐색



```python
def binary_search(arr, key):
    l = 1
    r = info[0]
    cnt = 0

    while l < r:
        c = int((l + r) / 2)
        if arr[c] == key:
            cnt += 1
            return cnt

        elif arr[c] > key:
            cnt += 1
            r = c

        else:
            cnt += 1
            l = c

    return cnt


t = int(input())

for tc in range(1, t+1):
    info = list(map(int, input().split())) #0번째는 전체 쪽 수, 1번째는 a의 키, 2번째는 b의 키
    arr = list(range(info[0])) #전체 쪽 수로 배열을 만듦

    if binary_search(arr, info[1]) < binary_search(arr, info[2]): #검색까지의 횟수를 비교
        print('#{} {}'.format(tc, 'A'))
    elif binary_search(arr, info[1]) > binary_search(arr, info[2]): #검색까지의 횟수를 비교
        print('#{} {}'.format(tc, 'B'))
    else:
        print('#{} {}'.format(tc, 0))
```



- 이진 탐색 구현을 숙달하기







- D3 4837. 부분집합의 합



```python
def subset(n, k):
    a = list(range(1, 13))

    parts = []
    for i in range(1<<12):
        part = []
        for j in range(12):
            if i&(1<<j):
                part.append(a[j])
        parts.append(part)

    cnt = 0
    for ele in parts:
        if sum(ele) == k:
            if len(ele) == n:
                cnt += 1

    return cnt

t = int(input())

for tc in range(1, t+1):
    n, k = map(int, input().split())

    print('#{} {}'.format(tc, subset(n,k)))
```



bit mask의 방법 참조



```python
    for ele in parts:
        if sum(ele) == n:
            if len(ele) == k:
                cnt += 1
    #실행시간 0.155~
                
    for ele in parts:
        if len(ele) == n:
            if sum(ele) == k:
                cnt += 1
    #실행시간 0.156~
```



- if문의 중첩에서 경우의 수가 적은 것을 바깥 if 문에 작성했더니 확실히 실행이 빨랐음







- D3 4843. 특별한 정렬



```python
def find():
    for i in range(10):
        midx = i #최대일 때 인덱스
        if i % 2 == 0: #짝수인덱스 ->최대값
            for j in range(i+1, n):
                if v[midx] < v[j]:
                    midx = j
        else: #홀수인덱스 ->최소값
            for j in range(i+1, n):
                if v[midx] > v[i]:
                    midx = j
        t = v[i] #자리를 서로 바꾸는 코드
        v[i] = v[midx]
        v[midx] = t

t = int(input())
for tc in range(1, t+1):
    n = int(input())
    v = list(map(int, input().split()))
    find()
    print('#{}'.format(tc), end=' ')
    for j in range(10):
        print(v[j], end=' ')
    print()
```







- D5 1259. 금속막대
- (모든 나사가 연결되어있다는 가정 하에 풀었음)



```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    n_list = list(map(int, input().split()))
    result = []
    even = [n_list[i] for i in range(2*n) if i % 2 == 0] #짝수번째의 수나사 굵기 리스트
    odd = [n_list[i] for i in range(2*n) if i % 2 == 1] #홀수번째의 암나사 굵기 리스트

    for i in range(n):
        if even[i] not in odd: #수나사 값이 암나사 리스트에 없다면 (모든 나사가 연결되어있으므로 가장 처음값)
            result.append(even[i]) #해당 암나사 값을 결과리스트에 더함
            result.append(odd[i]) #같은 인덱스의 수나사 값을 결과리스트에 더함


    while len(result) < 2*n: #전체 범위에서
        for i in range(n):
            if result[-1] == even[i]: #결과리스트의 끝 값이 수나사의 값이라면
                result.append(even[i]) #수나사의 값을 더하고
                result.append(odd[i]) #암나사의 값을 더함

    print('#{}'.format(tc), end=' ')
    [print(ele, end=' ') for ele in result[:-1]]
    print(result[-1])
```



- 리스트에서 대괄호 없이 값만 출력하는 또다른 방법

```python
print('#{0} {1}'.format(t, " ".join(map(str, result))))
```





