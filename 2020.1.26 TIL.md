### 자료형 맞추기



- set과 int는 덧셈을 지원 안 하니, result.add() 써야 함
- 여러 개의 숫자가 같은 용도로 쓰일 땐 각각 선언하기 보다, 리스트로 만들어줄 것
  - 1285번 문제에서는 리스트 만들 때 split()을 이용해서 풀이함. split()은 잘린 스트링을 리스트로 반환하니까
- += 연산자에서 원칙적으로는 좌변과 우변의 타입이 같아야.
  - 몇 가지 다른 타입에 대해 덧셈 연산이 가능한 경우가 있는데 dict와 int(not iterable)는 절대 안 됨
  - 기존 타입에 맞추는 방향으로 연습할 것

- map()은 결과로 맵 객체를 반환하니, list 등으로 자료형을 변환해줄 것
- 계산 과정에서의 자료형과, 리스트 안의 자료형까지 꼼꼼하게 확인할 것





### set 선언



- {}로 선언하면 dict가 기본값이니, set()으로 선언할 것

```python
d={}
print(type(d))
s=set()
print(type(s))
```









- D2, 1285. 아름이의 돌 던지기 문제 (python)

```python
t = int(input())

for i in range(1, t + 1):
    mem = int(input())
    d = input().replace('-', '')
    print(d)
    d_list = d.split(' ')

    d_list = list(map(int, d_list))

    m = min(d_list)
    count = 0
    for num in d_list:
        if num == m: count += 1

    print(f'#{i} {m} {count}')
```



- D2, 1288. 새로운 불면증 치료법 문제 (python)

```python
t = int(input())

for i in range(1, t + 1):
    result = set()
    n = int(input())
    k = 1


    while result != {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'}:
        m = k * n
        m = str(m)

        for j in range(len(m)):
            result.add(m[j])

        k += 1

    print(f'#{i} {m}')
```

