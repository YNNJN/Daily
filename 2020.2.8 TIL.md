## 2020.2.8 TIL



아래는 모두 시간 초과에 걸린 코드들,,...,,

백준 문제가 유난히 시간 및 메모리 초과 기준이 엄격한 것 같다. 해결 방법 찾아봐야지



- BOJ 1244. 스위치 켜고 끄기



```python
sch_n = int(input())
sch_info = list(map(int, input().split()))
std_n = int(input())
std_info = [list(map(int, input().split())) for _ in range(std_n)]

for i in range(std_n):
    if std_info[i][0] == 1: #남학생
        n = 1
        num1 = std_info[i][1]
        while n * num1 <= sch_n:
            sch_info[n*num1-1] = abs(sch_info[n*num1-1]-1)
            n += 1

    if std_info[i][0] == 2: #여학생
        m = 0
        num2 = std_info[i][1]
        while sch_info[num2 -1 - m] == sch_info[num2 -1 + m]:
            print(m, num2)
            if m != 0:
                sch_info[num2-1 - m] = abs(sch_info[num2 - m -1] - 1)
            sch_info[num2-1 + m] = abs(sch_info[num2 + m -1] - 1)
            m += 1
            if 0 > (num2 - 1 - m) or sch_n < (num2 + m -1):
                break

print(sch_info)
```







- BOJ 1929. 소수구하기



```python
def is_prime(number):
    if number != 1:
        for i in range(2, number):
            if number % i == 0:
                return False
    else:
        return False
    return number

n,m = map(int, input().split())
l = []
for i in range(n,m+1):
    if is_prime(i):
        l.append(i)
for el in l:
    print(el)
```







- BOJ 2869. 달팽이는 올라가고 싶다



```python
,b,v = map(int, input().split())
h, day = 0, 0

while h != v:
    h += a
    if h == v:
        pass
    else:
        h -= b
    day +=1
print(day)
```

