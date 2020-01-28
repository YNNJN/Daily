### memory error



- map()이란 리스트의 요소를 지정된 함수로 처리해주는 함수
  - 원본 리스트를 변경하지 않고 새 리스트를 생성함

- 메모리 map() > for ????

  - map을 이용했던 해당 코드를

  ```python
  date_int = list(map(int, date_list))
  ```

  - for로 대체하여 메모리 에러를 해결할 수 있었음

  ```python
  date_int = [int(date) for date in date_list]
  ```

- split() 또한 한 번에 읽어들여 스플릿 하니 메모리 필요량이 크다는 사실을 이전에 학습했음







### attribute error



- AttributeError: 'map' object has no attribute 'split'

- ```python
  date = map(int, input().split(' '))
  date_list = date.split(' ')
  ```

  이렇게 하려고 했었음 쩜쩜,,,,

- In python 3, map doesn't return a list

- int() 함수를 쓴다고 해도 list를 int로 변환할 수는 없음











[코딩테스트 준비에 있어 유의할 점](https://www.acmicpc.net/blog/view/70)





- 1926 간단한 369 게임

```python
num = input()
n_three = ['3', '6', '9']

for j in range(1, int(num)):
    cnt = 0
    current_num = str(j)

    for i in range(len(current_num)):

        if current_num[i] in n_three:
            cnt += 1

    if cnt > 0:
        print(cnt * '-', end=' ')

    else:
        print(current_num, end=' ')

print(num)
```







- 1940 알씨카

```python
t = int(input())

for i in range(1, t+1):
    n = int(input())
    v = 0
    d = 0

    for j in range(n):
        info = input()
        if info[0] == '1':
            a = int(info[2])
            v += a

        if info[0] == '2':
            a = int(info[2])
            v -= a
            if v < 0:
                v = 0

        d += v
    print(f'#{i} {d}')
```



- 위 아래 로직이 같은 부분은 동일하게 써서 모듈화 하고 (함수로 묶을 수도 있음),
  다른 부분만 추가되는 부분 변경해줄것







- 1945 간단한 소인수 분해

```python
t = int(input())

for i in range(1, t + 1):
    n = int(input())
    a, b, c, d, e = 0, 0, 0, 0, 0

    while n % 2 == 0:
        a += 1
        n = n / 2

    while n % 3 == 0:
        b += 1
        n = n / 3

    while n % 5 == 0:
        c += 1
        n = n / 5

    while n % 7 == 0:
        d += 1
        n = n / 7

    while n % 11 == 0:
        e += 1
        n = n / 11

    print(f'#{i} {a} {b} {c} {d} {e}')
```





- 1946 간단한 압축 풀기

```python
t = int(input())

for case in range(1, t+1):
    index = 0
    print(f'#{case}')
    tuples=[]
    for i in range(int(input())):
        alpha, num = input().split(' ')
        tuples.append((alpha,int(num)))

    for alpha,num in tuples:
        for j in range(num):
            if index < 10:
                print(alpha, end='')
                index += 1
            else:
                index = 0
                print()
                print(alpha, end='')
                index += 1
    print()

```







- 날짜 계산기

```python
t = int(input())

for i in range(1, t+1):
    date_list = input().split(' ') #월 일 월 일 str
    date_int = [int(date) for date in date_list]#월 일 월 일 int
    first = date_int[:2] #처음 월 일 int
    second = date_int[2:] #나중 월 일 int
    calendar = {1: 31, 2: 28, 3: 31, 4: 30, 5: 31, 6: 30, 7: 31, 8: 31, 9: 30, 10: 31, 11: 30, 12: 31}

    if first[0]==second[0]: #같은 월
        nth_day = second[1] - first[1] + 1

    else:
        start_month = calendar[first[0]] - first[1] #첫 월에 남은 일수
        days = start_month # 첫 월 일수

        month = second[0]-1

        while date_int[0] < month:
            days += calendar[month]
            month -= 1 # 마지막 달 까지의 일수

        final_month = second[1]

        nth_day = days + final_month +1

    print(f'#{i} {nth_day}')

```



- 캘리브레이션 값에 연연하지 말고 큰 틀부터 짤 것 