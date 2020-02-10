## 2020.2.9 TIL



### 버블솔트, 카운팅솔트 정리

(백준 2750번 문제 풀이)



- 버블솔트 이용



```python
def bubble_sort(numbers):
    for i in range(len(numbers)):
        for j in range(len(numbers)):
            if numbers[i] < numbers[j]:
                numbers[i], numbers[j] = numbers[j], numbers[i]
    return numbers

n = int(input())
numbers = [int(input()) for _ in range(n)]
print('\n'.join(map(str, bubble_sort(numbers))))
```



- 카운팅솔트 이용



```python
def counting_sort(numbers):
    cnt = [0] * (max(numbers)+1)
    for i in numbers:
        cnt[i] += 1
    ndx = 0
    for i in range(len(cnt)):
        while 0 < cnt[i]:
            numbers[ndx] = i
            ndx += 1
            cnt[i] -= 1
    return numbers

n = int(input())
numbers = [int(input()) for i in range(n)]
print('\n'.join(map(str, counting_sort(numbers))))
```



- 버블솔트 활용 문제

(백준 2947번 문제 풀이)



```python
numbers = list(map(int, input().split()))
while numbers != [1, 2, 3, 4, 5]:
    for i in range(5):
        if i+1 < 5:
            if numbers[i] > numbers[i+1]:
                numbers[i], numbers[i+1] = numbers[i+1], numbers[i]
                print(' '.join(map(str, numbers)))
```





#### 2차원 배열 연습



- D3 2805. 농작물 수확하기



```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    value = [list(map(int, input())) for _ in range(n)]
    profit = []

    for i in range(n//2+1):
        mid = value[i][n//2-i:n//2+i+1]
        profit.append(sum(mid))

    for m in range(n-1, n//2, -1):
        mid = value[m][n//2-(n-1-m):n//2+(n-1-m)+1]
        profit.append(sum(mid))

    s = sum(profit)
    print('#{} {}'.format(tc, s))
```







#### 부분집합 연습



- D3 5948. 새샘이의 7-3-5 게임
- 문제 풀이 후 생각난 M2를 주석으로 기록



```python
t = int(input())
#idxes = [(0,1,2),(0,1,3),....]

for tc in range(1, t+1):
    numbers = list(map(int, input().split()))
    s = []

    parts = []
    for i in range(1<<7):
        part = []
        for j in range(7):
            if i&(1<<j):
                part.append(numbers[j])
        parts.append(part)

    # for idx in idxes :
        # idx = (idx1, idx2, idx3)
        # s.append(sum(numbers[idx[0]],numbers[idx[1]],numbers[idx[2]]))

    for ele in parts:
        if len(ele) == 3:
            s.append(sum(ele))
    s = list(set(s))
    s = sorted(s)
    print('#{} {}'.format(tc, s[-5]))
```







#### 출력 방법 연습



- D3 5789. 현주의 상자 바꾸기



```python
t = int(input())
for tc in range(1, t+1):
    n,q = map(int, input().split())

    fst = [0 for _ in range(n)]
    for i in range(1,q+1):
        l, r = map(int, input().split())

        for j in range(l-1, r):
            fst[j] = i

    print('#{} {}'.format(tc, ' '.join(map(str, fst))))
```



