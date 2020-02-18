## 2020. 2.17 TIL



- 배추 -> dfs가 몇 번 호출되었는지를 묻는 문제







### 중위 to 후위변환



- 컴퓨터를 위한 계산기
- 중위표기법 -> 후위표기법, 스택을 이용해 변환
  - 한 자 씩 읽어서 숫자면 그냥 출력
  - 연산자 우선순위에 따라 스택에 대한 연산 달라짐
    - 토큰이 연산자면 스택 top과 비교, 높으면 push, 여는 괄호면 push
    - 토큰이 닫는 괄호이면, 여는 괄호를 만날 때까지 모두 pop
    - 우선순위가 낮은 연산자를 만날 때까지 pop, 낮은 연산자일 경우push
    - 여는 괄호는 버리고, 스택이 비었으면 정상 종료
  - 괄호 또한, 스택 밖의 왼쪽 괄호는 우선순위가 가장 높고, 스택 안의 왼쪽 괄호는 우선순위가 가장 낮음
  - 중위표기법에 더 읽을 것이 없다면 중지, 있다면 1부터 다시 반복
  - 스택에 남아 있는 연산자를 모두 pop하여 출력



```python
def is_number(x):
    if x not in operator and x not in braket:
        return True
    else:
        return False

def isp(token):  # isp : 스택의 top연산자 우선순위
    if token == '*' or token == '/':
        return 2
    elif token == '+' or token == '-':
        return 1
    elif token == '(':
        return 0

def icp(token):  # icp : 스택으로 들어갈 연산자 우선순위
    if token == '*' or token == '/':
        return 2
    elif token == '+' or token == '-':
        return 1
    elif token == '(':
        return 3


T = 10
operator = ['*', '/', '-', '+']  # 연산자
braket = ['(', ')']  # 괄호

for tc in range(1, T + 1):
    N = int(input())
    infix = list(input())  # 중위표기법
    postfix = []  # 후위표기법
    stack = []  # 변환을 위한스택
    # 중위 -> 후위
    for c in infix:
        if is_number(c):  # 피연산자면 그냥 출력
            postfix.append(c)
        elif c == ')':  # 닫는 괄호면 -> 여는 괄호 만날때까지 출력
            while len(stack) > 0:
                top = stack.pop()
                if top == '(':
                    break
                postfix.append(top)
        else:  # 닫는 괄호를 제외한 연산자
            if len(stack) == 0:  # 스택이 비어있다면
                stack.append(c)  # 토큰을 스택에 push
            else:  # 스택 비어있지 않으면 우선순위 비교 icp > isp 일때 push 아니면 pop
                while len(stack) > 0:
                    top = stack[-1]
                    if icp(c) > isp(top):
                        stack.append(c)
                        break
                    postfix.append(stack.pop())
    while stack:
        postfix.append(stack.pop())

    # 후위 표기법 -> 스택을 이용해서 계산
    stack = []
    for c in postfix:
        if c not in operator:  # 피연산자라면 스택에 넣기
            stack.append(int(c))
        else:
            op1 = stack.pop()
            op2 = stack.pop()
            if c == '+':
                stack.append(op2 + op1)
            elif c == '*':
                stack.append(op2 * op1)
            elif c == '-':
                stack.append(op2 - op1)
            elif c == '/':
                stack.append(op2 / op1)
    result = stack.pop()
    print("#{} {}".format(tc, result))
```







### 후위계산



```python
postfix = list(input())
stack = []
operator = ['+', '-', '*', '/']  # 연산자 리스트

for c in postfix:
    if c not in operator:  # 피연산자라면 스택에 넣기
        stack.append(int(c))
    else:
        op1 = stack.pop()
        op2 = stack.pop()
        if c == '+':
            stack.append(op2 + op1) #스택에서 처음 뽑은 것이 뒤로 감
        elif c == '*':
            stack.append(op2 * op1)
        elif c == '-':
            stack.append(op2 - op1)
        elif c == '/':
            stack.append(op2 / op1)
result = stack.pop()
print(result)
```







### 백트래킹



- 해를 찾는 도중에 막히면(해가 아니면) 되돌아가서 다시 해를 찾아가는 기법
- 최적화 문제(최대 최소값)와 결정 문제(Y/N) 해결 가능

- if문이 추가된 dfs
  - 해가 아니면 경로 탐색을 중지하여 시도의 횟수를 줄임 (Prunning 가지치기)
  - dfs와 시간복잡도에 차이가 있는 것은 아님(최악의 경우 exponential time인 것은 동일)



- 방법
  - 상태 공간 트리(해를 찾기 위한 과정을 트리로 표현)의 dfs 실시
  - 각 노드가 유망한지를 점검
  - 그 노드가 유망하지 않다면, 그 노드의 부모 노드로 되돌아가 검색을 계속함



- 미로찾기 문제도 스택에 방향을 저장하고, 막힌 경우 다시 이전의 노드로 돌아오는 방법으로 풀이 가능
- (이전에 풀었던 visited 방식 아닌)





- 완전탐색 이용한 부분집합의 합

```python
#원소의 합이 10인 부분집합의 개수 출력
#완전탐색
def f(i,n,k): #i번째 원소를 포함하는 경우/포함하지 않는 경우->재귀호출
    global bit
    global cnt
    if i == n: #base case: bit의 모든 칸이 결정됨
        #print(bit) #모든 경우의 수
        s = 0
        for j in range(n):
            if bit[j] == 1:
                s += j+1
        if s == k:
            cnt += 1
        return
    else:
        bit[i] = 1 #i번째 원소가 선택된 경우
        f(i+1,n,k)
        bit[i] = 0 #선택되지 않은 경우
        f(i+1,n,k)

n = 10 #원소의 수
k = 10 #부분집합의 합
bit = [0] * n #원소의 포함여부 저장
cnt = 0 #조건 만족하는 부분집합 개수
f(0,n,k) #부분집합을 구하고 -> 총합이 10인 부분집합 개수 세기
print(cnt)
```





- 백트래킹 이용한 부분집합의 합

```python
def f(i,n,k,s,r): #s:선택된 원소들의 합, r: 남은 원소들의 합(선택 가능한 후보 중)
    global cnt

    # base case:
    if s == k: #나머지 원소 하나라도 더 선택하면 k보다 커지니, 더 탐색할 이유x
        cnt += 1
        return
    elif i == n: #모든 원소를 고려했는데, 합이 k가 되는 경우가 없음
        return
    elif s > k: #현재까지의 누적합이 k보다 크면 더 탐색할 이유x
        return
    elif s + r < k: #현재까지의 합 + 후보군의 합이 k보다 작다면 정답이 될 가능성x
        return #back tracking, 가지치기
    else:
        # i번째 요소가 선택된 경우
        f(i+1, n, k, s+i+1, r-(i+1))
        # i번째 요소가 선택되지 않은 경우
        f(i+1, n, k, s, r-(i+1))

n = 20 #1부터 n까지가 집합의 원소
k = 10 #부분집합의 합
cnt = 0

f(0,n,k,0,(1+n)*n//2) #원소의 위치(i), 부분집합의 합, 선택 후보들의 합
print(cnt)
```







### n-queen

- n*n 체스판에  n개의 queen을 서로 위협하지 않도록 배치하는 문제
- 같은 행, 같은 열, 같은 대각선 공격



```python
def promising(level):
    for i in range(1, level):  # 기존 말 cols[i], 현재 말 cols[level]
        if cols[i] == cols[level] or (level - i) == abs(cols[i] - cols[level]):
            return False
    return True

def queen(level):
    global cnt
    if promising(level) == False:
        return
    elif level == n:
        cnt = cnt + 1
        return
    else:
        for i in range(1, n + 1):
            cols[level + 1] = i
            queen(level + 1)
        return

t = int(input())
for tc in range(1, t + 1):
    n = int(input())
    cols = [0] * (n + 1)
    cnt = 0
    queen(0)
    print("#{} {}".format(tc, cnt))
```







### Divide and Conquer

- 분할(Divide):  해결할 문제를 여러 개의 작은 부분으로 나눔
- 정복(Conquer): 나눈 작은 문제를 각각 해결함
- 통합(Combine): (필요하다면) 해결된 해답을 모음



```python
#분할정복
'''
홀/짝 경우 나눠 생각
c^8 = c^4 * c^4
c^9 = c^4 * c^4 * c
'''

def power2(base,exponent):
    if exponent == 0 or base == 0:
        return 1
    if exponent % 2 == 0:
        newbase = power2(base, exponent/2)
        return newbase * newbase
    else:
        newbase = power2(base, (exponent-1)/2)
        return newbase * newbase * base
print(power2(2,10))
```



- D2 4880. 토너먼트 카드게임



```python
def find(l,r): #l:왼쪽, r:오른쪽 -> 카드리스트 범위
    if l == r: #카드가 한 장일 떄
        return l
    else:

        result1 = find(l,(l+r)//2) #카드를 반으로 나눠 재귀호출
        result2 = find((l+r)//2+1, r)
        if card[result1] == card[result2]: #카드가 서로 같으면
            return result1
        else:
            #가위바위보
            if card[result1] == 1 and card[result2] == 2:
                return result2
            if card[result1] == 1 and card[result2] == 3:
                return result1
            if card[result1] == 2 and card[result2] == 1:
                return result1
            if card[result1] == 2 and card[result2] == 3:
                return result2
            if card[result1] == 3 and card[result2] == 1:
                return result2
            if card[result1] == 3 and card[result2] == 2:
                return result1

t = int(input())
for tc in range(1, t+1):
    n = int(input())
    card = [0] + list(map(int, input().split()))
    print('#{} {}'.format(tc, find(1,n)))
```




