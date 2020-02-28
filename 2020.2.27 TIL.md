## 2020.2.27 TIL



- D4 1486. 장훈이의 높은 선반



- 부분집합의 합 복습문제

```python
t = int(input())
for tc in range(1, t+1):
    n, b = map(int, input().split())
    s = list(map(int, input().split()))
    result = []
    min_value = 10000 * n
    for i in range(1 << n):
        value = 0
        for j in range(n):
            if i & (1 << j):
                value += s[j]
        if value >= b:
            if value < min_value:
                min_value = value
                result.append(min_value - b)
    print('#{} {}'.format(tc, result[-1]))
```



- 는 dfs로도 풀 수 있음
- 값을 더하거나 / 더하지 않거나, 두 가지 경우로 나누어 마지막까지 더함

```python
total = 0
def dfs(a, k, n):
    global total
    if k == n:
        sum = 0
        for j in range(n):
            if a[j]:
                sum += data[j]
        if sum >= b:
            total = 0
            for j in range(n):
                if a[j]:
                    total += data[j]
            result.append(total)
    else:
        a[k] = 1
        dfs(a, k+1, n)
        a[k] = 0
        dfs(a, k+1, n)

for i in range(int(input())):
    n, b = map(int, input().split())
    data = list(map(int, input().split()))

    result = []
    a = [0] * b
    dfs(a, 0, n)
    print('#{} {}'.format(i + 1, min(result) - b))
```









- D4 1258. 행렬 찾기



- 가로, 세로로 나아가는 칸의 개수를 세어가며 순차적으로 풂
- [참고_다중조건의 정렬](https://dailyheumsi.tistory.com/67) 방법을 배움

```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    lab = [list(map(int, input().split())) for _ in range(n)]
    info = []
    for i in range(n):
        for j in range(n):
            garo, sero = 0,0
            if lab[i][j] != 0:
                garo += 1
                sero += 1
                k = 1
                while j+k < n:
                    if lab[i][j+k] != 0:
                        garo += 1
                        k += 1
                    else:
                        break
                p = 1
                while i+p < n:
                    if lab[i+p][j] != 0:
                        sero += 1
                        p += 1
                    else:
                        break
                info.append([sero, garo, sero*garo])
                for q in range(i,i+p):
                    for qq in range(j,j+k):
                        lab[q][qq] = 0
    #key 인자에 함수를 넘겨주면 해당 함수의 반환값을 비교하여 순서대로 정렬함
    l = sorted(info, key = lambda x: (x[2], x[0]))
    for li in range(len(l)):
        del l[li][2]
    print('#{}'.format(tc), end=' ')
    print(len(l), end=' ')
    l2 = []
    for ele in range(len(l)):
        for el in range(2):
            l2.append(l[ele][el])
    print(' '.join(map(str, l2)))
```



- 이것도 역시 dfs로 풀 수 있는 문제. 다중 조건의 정렬 없이 찬찬히 구현하면 이렇게

```python
def dfs(r, c):
    cnt, row_cnt = 1, 1
    stack = []
    if (r, c) in visited:
        return
    visited.append((r, c))
    stack.append((r, c))
    delta = [(0, 1), (1, 0)]
    while stack:
        r, c = stack.pop()
        for d in range(2):
            nr = r + delta[d][0]
            nc = c + delta[d][1]
            if -1 < nr < n and -1 < nc < n and arr[nr][nc] != 0 and (nr, nc) not in visited:
                if d == 1:
                    row_cnt += 1
                stack.append((nr, nc))
                visited.append((nr, nc))
                cnt += 1
    return cnt, row_cnt


t = int(input())
for tc in range(1, t + 1):
    n = int(input())
    arr = [list(map(int, input().split())) for _ in range(n)]
    visited = []
    sub_arr = []
    for i in range(n):
        for j in range(n):
            if arr[i][j] != 0:
                sub_arr.append(dfs(i, j))
    ans_list = []
    for i in sub_arr:
        if i:
            ans_list.append(i)
    ans_list.sort()
    result = []
    for i in ans_list:
        result.append(str(i[1]))
        result.append(str(i[0]//i[1]))
    print('#{} {}'.format(tc, len(ans_list)), end=' ')
    print(' '.join(result))
```







- D3 3456. 직사각형 길이 찾기



- 변의 길이가 같은 쌍이 하나 또는 둘 존재함에 유의하여 간단하게 풂

```python
t = int(input())
for tc in range(1, t+1):
    side = list(map(int, input().split()))
    l = []
    for ele in side:
        if ele in l:
            l.remove(ele)
        else:
            l.append(ele)
    print('#{} {}'.format(tc, ''.join(map(str, l))))
```





- D3 3499. 퍼펙트 셔플



- 홀수 개 카드일 경우의 처리가 필요했음

```python
def shuffle(n):
    if n % 2 == 0:
        l = []
        for i in range(n//2):
            l.append(card[:n//2][i])
            l.append(card[n//2:][i])
        return l
    else:
        l2 = []
        for i in range(n//2):
            l2.append(card[:n//2+1][i])
            l2.append(card[n//2+1:][i])
        l2.append(card[:n//2+1][n//2])
        return l2

t = int(input())
for tc in range(1, t+1):
    n = int(input())
    card = list(input().split())
    print('#{} {}'.format(tc, ' '.join(map(str, shuffle(n)))))
```



