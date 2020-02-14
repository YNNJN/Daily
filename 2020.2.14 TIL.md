## 2020. 2. 14 TIL



- D2 4871. 괄호검사

- 접근 1. top  안 쓰고 풀려 했던.
  top을 쓰는 이유를 깨달음
- stack.pop()을 비교 후 다시 팝하려했는데,
  이 함수는 아예 팝한 걸로 호출 없이 호출되니, 또다시 팝할 이유 없음

```python
def check():
    for i in range(len(case)):
        if case[i] != '{' or case[i] != '}' or case[i] != '(' or case[i] != ')':
            pass

        if case[i] == '{' or case[i] == '(':
            stack.append(case[i])
        elif case[i] == '}' or case[i] == ')':
            if len(stack) == 0:
                return 0

            elif [stack.pop(), case[i]] == standard1:
                pass
            elif [stack.pop(), case[i]] == standard2:
                pass

            else:
                return 0

    if len(stack) != 0:
        return 0
    else:
        return 1

t = int(input())
for tc in range(1, t+1):
    case = input()
    stack = []
    standard1 = ['{', '}']
    standard2 = ['(', ')']
    print('#{} {}'.format(tc, check()))
```





- 접근2. top을 쓰고
- standard1 = ['{', '}']가 얕은 복사가 됨을 확인하여 수정함

```python
def check():
    top = -1
    for i in range(len(case)):
        if case[i] == '{' or case[i] == '(':
            stack.append(case[i])
            top += 1

        elif case[i] == '}' or case[i] == ')':
            if top == -1:
                return 0
            else:
                if stack[top] == '{' and case[i] == '}':
                    stack.pop(top)
                    top -= 1
                elif stack[top] == '(' and case[i] == ')':
                    stack.pop(top)
                    top -= 1
                else:
                    return 0
    if top != -1:
        return 0
    else:
        return 1

t = int(input())
for tc in range(1, t+1):
    case = input()
    stack = []
    print('#{} {}'.format(tc, check()))
```



- 석우님은 충분한 배열 만든 후 인덱스에 아예 스택의 값을 추가하는 방식으로 풂. top만 조정하는 것이 아니라. 지금 리스트를 다루고 있으니 값은 빠지지 않고 top만 개념적으로 달라지는 거니까





- D2 4837. 반복문자 지우기
- 를 위의 석우님 아이디어를 이용해 풀어봄. top 인덱스만으로 조작할 경우 이 인덱스의 범위 제한 조건을 또다시 줘야하기 때문에 이 아이디어가 유리하다고 생각했기 때문

```python
t = int(input())
for tc in range(1, t+1):
    case = list(input())
    stack = [0]*1001
    top = -1
    top += 1
    stack[top] = case[0]
    cnt = 0

    for i in range(1,len(case)):

        if stack[top] == case[i]:
            stack[top] = 0
            top -= 1
        else:
            top += 1
            stack[top] = case[i]

    print('#{} {}'.format(tc, top + 1))
```



- 그런데 top을 안써도 풀 수 있는 방법이 있었음

```python
def find():
    s = []
    for i in range(len(str)):
        if len(s) != 0:
            ch = s.pop()
            if str[i] != ch:
                s.append(ch)
                s.append(str[i])
        else:
            s.append(str[i])
    return len(s)


T = int(input())
for tc in range(1, T + 1):
    str = input()
    print('#{} {}'.format(tc, find()))
```





- D2 4871. 그래프 경로
- 접근은 제대로 했는데 dfs 구현이 숙달되지 않아 어려움을 겪음
- 행에서 값이 1인 열을 모두 찾고 그 열의 인덱스를 행으로 하여 1인 값을 또 찾음. 반복 후 goal의 열의 인덱스에 있는 값이 1이면 경로가 있는 것
- 중간 단계의 반복이 몇 번 이뤄지는지 몰라 코드 작성에 어려움을 겪었고, 이에 스택의 이용이 꼭 필요함을 알게됨. 이 때 재귀를 사용할 수 있겠구나도 생각함

```python
def dfs(n, end):
    visited = [0] * (V + 1)
    stack = []
    stack.append(n)  #시작점을 스택에 넣고, 방문했다고 표시
    visited[n] = 1

    while stack:
        n = stack.pop(0)
        if n == end:
            return 1
        for i in range(1, V+1): #부가적으로 만들어준 가장자리 0은 취급x
            if adj[n][i] == 1 and visited[i] == 0:
                stack.append(i)
                visited[i] = 1
    return 0


T = int(input())
for tc in range(1, T + 1):
    V, E = map(int, input().split())
    adj = [[0] * (V + 1) for _ in range(V + 1)]
    for i in range(E):
        u, v = map(int, input().split())
        adj[u][v] = 1  # 방향그래프
    S, G = map(int, input().split())
    result = dfs(S, G)
    print("#{} {}".format(tc, result))
```



- 인접리스트, 즉 딕셔너리로 풀기
- 노드의 값을 키로 하여 간선이 밸류로 연결되는 딕셔너리로 구현함

```python
def dfs():
    visited = {i: 0 for i in range(V + 1)}
    stack = []
    stack.append(start)
    while len(stack) != 0:
        n = stack.pop(0)
        if n == end:
            return 1
        for t in adj[n]:
            if visited[t] == 0:
                stack.append(t)
                n = t
    return 0


T = int(input())
for tc in range(1, T + 1):
    V, E = map(int, input().split())
    adj = {i: [] for i in range(1, V + 1)}  # {정점:[인접정점들], 정점2:[인접정점들]}
    for i in range(E):
        u, v = map(int, input().split())
        adj[u].append(v) #인접행렬
    # print(adj)
    start, end = map(int, input().split())
    print("#{} {}".format(tc, dfs()))
```



- 재귀로 풀기
- 현재 상태를 바꾸며 같은 행동을 계속 반복하도록 하는 데 재귀를 이용

```python
def dfs(n):
    if n == end:
        return 1
    else:
        for t in adj[n]:
            if visited[t] == 0:
                visited[t] = 1  #방문표시
                if dfs(t) == 1: #나 자신을 호출
                    return 1
        return 0


T = int(input())
for tc in range(1, T + 1):
    V, E = map(int, input().split())
    visited = {i: 0 for i in range(V + 1)}  #방문 표시
    adj = {i: [] for i in range(1, V + 1)}  #{정점:[인접정점들], 정점2:[인접정점들]}
    for i in range(E):
        u, v = map(int, input().split())
        adj[u].append(v)
    # print(adj)
    start, end = map(int, input().split())
    print("#{} {}".format(tc, dfs(start)))
```



