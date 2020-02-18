## 2020. 2. 18 TIL





### 퀵 정렬



- 주어진 배열을 두 개로 분할하고, 각각을 정렬함
- partitioning, 점점 쪼개가며 정렬하는 방식
- pivot, 기준점을 중심으로 작은 것은 왼 편, 큰 것은 오른편에 위치시킴
- 각 부분 정렬이 끝난 후, 합병정렬은 '합병'이란 후처리 작업이 필요하나, 퀵정렬은 필요x



```python
#중간값을 기준으로 양 옆을 다시 퀵솔팅함 (재귀)
#피봇의 설정 위치는 달라질 수 있음
```



```python
def partition(arr,low,high):
    pivot = (low+high)//2
    l = low #l,r의 초기값 설정
    r = high
    while l < r:
        while arr[l] < arr[pivot] and l < r: #l의 값이 pivot보다 작을 때까지
            l += 1 #오른쪽으로 이동
        while arr[r] >= arr[pivot] and l < r: #r의 값이 pivot보다 크거나 같을 때까지
            r -= 1 #왼쪽으로 이동
        if l < r:
            if l == pivot:
                pivot = r
            arr[l], arr[r] = arr[r], arr[l]
    arr[pivot], arr[r] = arr[r], arr[pivot]
    return r

def quicksort(arr, low, high):
    if low < high:
        p = partition(arr,low,high)

        quicksort(arr,low,p-1)
        quicksort(arr,p+1,high)

arr = [10, 7, 8, 9, 1, 5]
n = len(arr)
quicksort(arr, 0, n-1)
print(arr)
```







- D3 4874. Forth



```python
t = int(input())
for tc in range(1, t+1):
    code = input().split()
    stack = []
    operator = ['+', '-', '*', '/']
    flag = True

    for i in range(len(code)):
        if code[i] == '.':
            continue
        elif code[i] not in operator:
            stack.append(int(code[i]))
        elif code[i] in operator:
            if len(stack) < 2:
                flag = False
                break

            n1 = stack.pop()
            n2 = stack.pop()
            if code[i] == '+':
                ans = n2 + n1
            if code[i] == '-':
                ans = n2 - n1
            if code[i] == '*':
                ans = n2 * n1
            if code[i] == '/':
                ans = n2 // n1
            stack.append(ans)

    if len(stack) > 1:
        flag = False

    if flag == True:
        print('#{} {}'.format(tc, ans))

    if flag == False:
        print('#{} {}'.format(tc, 'error'))
```







- D3 4875. 미로



```python
def dfs(r,c,maze):
    dr = [-1, 0, 1, 0]
    dc = [0, -1, 0, 1]
    stack = []
    visited = [[0 for _ in range(n)] for _ in range(n)]
    stack.append([r,c])
    visited[r][c] = 1
    while stack:
        cur = stack.pop()
        for i in range(4):
            tr = cur[0] + dr[i]
            tc = cur[1] + dc[i]

            if tr < 0 or tc < 0 or tr > n-1 or tc > n-1:
                continue
            if maze[tr][tc] == 3:
                return 1
            elif maze[tr][tc] == 0 and visited[tr][tc] == 0:
                stack.append([tr,tc])
                visited[tr][tc] = 1
    return 0

t = int(input())
for tc in range(1, t+1):
    n = int(input())
    maze = [list(map(int, input())) for _ in range(n)]

    for i in range(n):
        for j in range(n):
            if maze[i][j] == 2:
                r,c = i,j
    print('#{} {}'.format(tc, dfs(r,c,maze)))
```







- BOJ 1012. 유기농 배추



- 스택 이용한 방법



```python
dr = [-1, 0, 1, 0]
dc = [0, 1, 0, -1]

def dfs(r, c):
    stack = []
    stack.append([r, c])
    arr[r][c] = 0  # 현재위치의 배추 없애기
    while stack:
        cur = stack.pop()
        for k in range(4):
            nr, nc = cur[0] + dr[k], cur[1] + dc[k]
            if arr[nr][nc] == 1:
                arr[nr][nc] = 0
                stack.append([nr, nc])

T = int(input())
for tc in range(1, T + 1):
    M, N, K = map(int, input().split())
    arr = [[0 for _ in range(M + 2)] for _ in range(N + 2)]  # 맵의 테두리를 0으로 채움
    for _ in range(K):
        x, y = map(int, input().split())
        arr[y + 1][x + 1] = 1
    cnt = 0
    for i in range(1, N + 1):
        for j in range(1, M + 1):
            if arr[i][j] == 1:
                dfs(i, j)
                cnt += 1
    print(cnt)
```



- 재귀 이용한 방법
  - 백준에 제출 시 재귀 깊이 없애는 구문?



```python
import sys
sys.setrecursionlimit(10**6)

def dfs(r,c):
    dr = [1, 0, -1, 0]
    dc = [0, 1, 0, -1]

    for i in range(4):
        tr = r + dr[i]
        tc = c + dc[i]

        if tr < 0 or tc < 0 or tr >= m or tc >= n:
            continue
        if ground[tr][tc] == 1 and visited[tr][tc] == 0:
            visited[tr][tc] = 1
            return dfs(tr,tc)

t = int(input())
for tc in range(1,t+1):
    m,n,k = map(int, input().split())
    ground = [[0 for _ in range(n)] for _ in range(m)]
    visited = [[0 for _ in range(n)] for _ in range(m)]
    for _ in range(k):
        i,j = map(int, input().split())
        ground[i][j] = 1

    cnt = 0
    r,c = 0,0
    for r in range(m):
        for c in range(n):
            if ground[r][c] == 1 and visited[r][c] == 0:
                cnt += 1
                visited[r][c] = 1
                dfs(r,c)
    print(cnt)
```



