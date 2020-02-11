## 2020. 2. 10 TIL



### string

ASCHII (American Standard)

- 48번: 0~
- 65번: A~
- 97번: a~

-> 다국어처리를 위한 코드, 유니코드(Universal Code)

- 웹 (UTF-8)
  - min: 8bit, max: 32bit(1byte * 4)



- 문자열은 튜플과 같이 요소값을 변경할 수 없음(immutable)
- +를 이용한 concatenation은 새로운 열을 더해서 넣는 것, 즉 요소값 변경이 아님







- 문자열 뒤집기



```python
#M1
s = 'Reverse this string'
s_rev = ''
for ch in s: #문자열은 시퀀스형 -> 반복문 적용 가능
    s_rev = ch + s_rev
print(s_rev)

#M2
s_list = list(s) #문자열을 리스트로
s_list.reverse() #자기 자신을 받아서 백업, 즉 따로 호출할 필요x
# print(s_list)
print(''.join(s_list)) #리스트를 문자열로 출력

#M3
print(''.join(reversed(s)))

#슬라이싱 이용
# print(s[:]) #모든 문자열
print(s[::-1]) #모든 구간에 대해서 거꾸로 돌아옴
```







- 문자열 비교



```python
s1 = input()
s2 = input()
print(f(s1, s2))

def f1(s1, s2):
    s = len(s1) if len(s1) >= len(s2) else len(s2)
    for i in range(s):
        if s1[i] != s2[i]:
            return 0
    return 1
```







- 앞 뒤 글자 바꾸기



```python
s = list(input())
# print(s)

'''
a <-> d, b <-> c
'''
for i in range(len(s)//2):
    s[i], s[len(s)-1-i] = s[len(s)-1-i], s[i]
for i in range(len(s)):
    print(s[i], end='')
```







- 문자 <-> 숫자 변환



```python
def atoi(s): #숫자로 생긴 문자 -> 숫자로 변경하는 함수
    n = 0
    for i in range(len(s)):
        #0->0, 1->10, 2->20
        n = n*10
        n += (ord(s[i])-ord('0')) #n += int(s[i])와 동일 의미 #shifting
    return n

s = input()
print(type(s))
r = atoi(s) #문자를 입력받아서 int형으로 변환해서 리턴
print(r)
```







- 패턴 매칭



```python
p = 'is'
t = 'This is a book'
m = len(p) #찾을 패턴의 길이
n = len(t) #전체 텍스트의 길이

def bruteForce(p,t):
    i = 0 #t의 인덱스
    j = 0 #p의 인덱스
    while j < m and i < n: #패턴 길이, 전체 텍스트 길이만큼 반복
        if t[i] != p[j]: #글자가 다를 때 
            i = i-j
            j = -1 #j ->0으로 (아래에서 +1이라서 -1이 상쇄됨)
        i = i+1 #옆 칸 검사
        j = j+1
    if j == m: return i - m #검색 성공
    else: return -1 #검색 실패

print(bruteForce(p,t))
```







- D3 1221. GNS
- List rule의 인덱스가 그대로 요소가 됨을 이용해서 간단하게 풀 수 있었음



```python
t = int(input())
for tc in range(1, t+1):
    n = input().split()
    numbers = input().split()
    rule = ['ZRO', 'ONE', 'TWO', 'THR', 'FOR', 'FIV', 'SIX', 'SVN', 'EGT', 'NIN']

    l = []
    for i in range(len(rule)):
        for number in numbers:
            if number == rule[i]:
                l.append(number)

    print('#{} {}'.format(tc, ' '.join(map(str, l))))
```

