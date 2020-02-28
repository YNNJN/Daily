## 2020.2.28 TIL



D3 중반부에 진입하니 '제한시간 초과'에 걸리는 문제들이 많아졌다. 코드 최적화를 노력해봐야지. 아래의 문제들은 재귀로 풀려고 시도했다가~ 제한시간 초과에 걸리고, 방법을 바꾸어 풀어낸 문제들.



- D3 3750. digit sum



- M1. 재귀로 시도 - 제한시간 초과

```python
def digit_sum(n):
    s = 0
    for i in range(len(n)):
        s += int(n[i])
    if len(str(s)) == 1:
        return s
    else:
        n = str(s)
        return digit_sum(n)

t = int(input())
for tc in range(1, t+1):
    n = input()
    print('#{} {}'.format(tc, digit_sum(n)))
```



- M2. 같은 접근인데  while True를 시도함 - 성공

```python
ans = []
for tc in range(int(input())):
    n = input()

    while True:
        if len(n) == 1:
            ans.append(n)
            break
        else:
            result = []
            for i in n:
                result.append(int(i))
            n = str(sum(result))
j = 1
for i in ans:
    print('#{} {}'.format(j, i))
    j += 1
```





- M3. 수학적 아이디어로, 조건문으로 처리하는 방법도 시도함 - 성공

```python
ans = []
for tc in range(int(input())):
    nums = input()
    l = list(range(1, 10))
    if int(nums) < 10:
        ans.append(int(nums))
    else:
        sum = 0
        for i in range(len(nums)):
            sum += int(nums[i])
        if sum >= 10:
            result = l[(sum % 9) - 1]
            ans.append(result)
        else:
            result = sum
            ans.append(result)
j = 1
for i in ans:
    print('#{} {}'.format(j,i))
    j += 1
```







- D3 3408. 세가지 합 구하기



- M1. 노멀하게 풀었다고 생각했는데 - 제한시간 초과

```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    s1, s2, s3 = 0, 0, 0
    for i in range(1, 2*n+1):
        if i < n+1:
            s1 += i
        if i % 2:
            s2 += i
        else:
            s3 += i
    print('#{} {} {} {}'.format(tc, s1, s2, s3))
```



- M2. 반복문 아예 없이 풀어야 했음을.. - 성공

```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    s1 = (n+1)*n//2
    s2 = n**2
    s3 = 2*s1
    print('#{} {} {} {}'.format(tc, s1, s2, s3))
```







- D3 3376. 파도반수열



- M1. 재귀로 시도 - 제한시간 초과

```python
def sequence(n):
    if n <= 2:
        return 1
    else:
        return sequence(n-3) + sequence(n-2)

t = int(input())
for tc in range(1, t+1):
    n = int(input())-1
    print('#{} {}'.format(tc, sequence(n)))
```



- M2. 수열을 미리 만들고 참조하여 출력함 - 성공

```python
n = 100
s = [0 for _ in range(n + 1)]
for i in range(1, n+1):
    if i < 4:
        s[i] = 1
    else:
        s[i] = s[i - 3] + s[i - 2]

t = int(input())
for tc in range(1, t + 1):
    n = int(input())
    print('#{} {}'.format(tc, s[n]))
```







- D3 3975. 승률 구하기



- M1. 깔끔하게 푼 것 같았지만 - 제한시간 초과

```python
t = int(input())
for tc in range(1, t+1):
    case = list(map(int, input().split()))
    a = case[0]/case[1]
    b = case[2]/case[3]
    if a == b:
        print('#{} {}'.format(tc, 'DRAW'))
        continue
    win = 'ALICE' if (a > b) else 'BOB'
    print('#{} {}'.format(tc, win))
```



- M2. 삼항연산자에 조건문을 두 개 두는 방법을 익힘 - 성공

```python
ans = []
t = int(input())
for _ in range(t):
    a,b,c,d = map(int, input().split())
    ans.append('ALICE' if a/b>c/d else 'DRAW' if a/b==c/d else 'BOB')
for i in range(t):
    print(f'#{i+1} {ans[i]}')
```







- D3 1225. 암호생성기



- M1. 조건의 섬세한 처리가 필요했던 방법 - 성공

```python
n = 8
for t in range(1, 11):
    tc = int(input())
    nums = list(map(int, input().split()))
    flag = 1
    while flag:
        for i in range(1, 6):
            tmp = nums[0] #이동시키고 난 다음의 처리를 해줘야
            for j in range(1, n):
                nums[j-1] = nums[j]
            nums[-1] = tmp - i
            if nums[-1] < 1:
                nums[-1] = 0
                flag = 0
                break
    print('#{0}'.format(t), end=' ')
    for num in nums:
        print(num, end=' ')
```



- M2. list.count() 로 0의 개수를 세서 풀면 접근이 더욱 간단함 - 성공

```python
for t in range(10):
    n = int(input())
    data = list(map(int, input().split()))

    while data.count(0) != 1:
        for i in range(1, 6):
            a = data.pop(0) - i
            if a <= 0:
                a = 0
            data.append(a)
            if data.count(0) >= 1:
                break

    print('#{} {}'.format(t+1, ' '.join(list(map(str, data)))))
```





