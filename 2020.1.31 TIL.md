## 2020. 1. 31 TIL



- while에 for문과 if가 중첩되어 있는 경우에서, break를 if문에 줄 경우, for문만 종료됨
- 이를 방지하기 위해 while문 이전에 is_while_over = False의 함수를 이용해서 해결함(에릭의 도움!)



중간부터만 가져오자면

```python
is_while_over = False
while k_scr in totalscr_list:
    if is_while_over == True:
        break

    for i in range(len(degree)):
        if k_scr in totalscr_list[:proportion]:

            print(f'#{tc} {degree[i]}')
            is_while_over = True
            break
        else:
            totalscr_list = totalscr_list[proportion:]
```





- int, round, 주의할 것
- 점수 비교 시 소수 몇 째자리까지 같은 것들이 있음에 유의하여 판별 전까지는 float로 전체를 받는 것이 좋을 것



- [TypeError: 'int' object is not subsciptable](https://stackoverflow.com/questions/9054854/typeerror-int-object-is-not-subscriptable)

```python
arr[i][j] = arr[i-1][j-1]

```

이런 식으로 값을 대체하고 싶었는데, 좌변과 우변 모두 인트이므로 타입에러가 남





오늘 재밌게 푼 문제들

왠지 문자열 슬라이싱을 열심히 써서 풀었다



- D2 1983. 조교의 성적 매기기

```python
t = int(input())

for tc in range(1, t+1): #테스트케이스 t회 반복
    N, k = map(int, input().split()) #학생 수와 학점을 알고 싶은 학생의 번호 k 입력
    totalscr_list = []  #전체 점수를 담을 리스트 초기화

    for n in range(N): #학생 수 만큼에 대해
        scr_mid, scr_fin, scr_ass = map(int, input().split()) #점수를 입력받음
        scr_total = 0.35*scr_mid + 0.45*scr_fin + 0.2*scr_ass #반영 비율 고려한 총 점수 계산
        totalscr_list.append(scr_total) #각 학생의 점수를 리스트에 더함
        # print(totalscr_list)

    k_scr = totalscr_list[k - 1] #k번째 학생의 점수를 변수에 저장
    totalscr_list.sort(reverse=True) #전체 점수를 내림차순으로 정렬함
    proportion = int(N / 10) #학점 별 비율 변수 지정
    degree = ['A+', 'A0', 'A-', 'B+', 'B0', 'B-', 'C+', 'C0', 'C-', 'D0'] #학점 리스트

    is_while_over = False
    while k_scr in totalscr_list: #k의 점수가 전체 리스트에 존재하는 조건에서
        if is_while_over == True:
            break

        for i in range(len(degree)): #각 학점에 대해 반복
            if k_scr in totalscr_list[:proportion]: #k의 점수가 전체 리스트 중 최대 성적의 비율 안에 있으면

                print(f'#{tc} {degree[i]}') #테스트케이스 회차와 학점의 종류를 출력
                is_while_over = True
                break #출력했으면 조건문 끝냄
            else:
                totalscr_list = totalscr_list[proportion:] #k의 점수가 비율 안에 없으면, 전체 리스트에서 해당 비율의 부분을 제외함
```





- D2 2007. 패턴 마디의 길이

```python
t = int(input())

for tc in range(1, t+1):
    words = input()

    for len_node in range(1, 11):
        if words[:len_node] == words[len_node:(2*len_node)]:
            node = words[:len_node]
            num = len(node)

            if node[:int(len(node) / 2)] == node[int(len(node)/2):]:
                node = node[:int(len(node)/2)]
                num = len(node)

            if node[:int(len(node) / 3)] == node[int(2*len(node) / 3):]:
                node = node[:int(len(node)/3)]
                num = len(node)

    print(f'#{tc} {len(node)}')




'''
마디의 길이를 출력하는 문제
len(words) = 30
마디의 최대 길이는 10이라고 했어
그럼 최소한 워즈에서 마디가 세 번은 나올거야
그럼 노드의 길이를 1부터 10까지 준 다음
길이를 1씩 늘려가면서 바로 다음에 오는 것들이 이전에 반복한 것들과 일치하는 지를 확인하면 되겠네

두 번씩 출력하는 것이 있어서 조건을 추가해야할 것 같아
두 번씩 출력하는 이유는 주어진 워즈 내에서 짝수 개만큼, 그리고 워즈의 완전 끝까지 마디로 끊어지기 때문
노드를 중간에서 끊은 것의 앞과 뒤가 일치한다면
그것의 반절만큼이 노드인 조건을 주면 됨

아 엑소는 세 번 반복되는구나, 그럼 세 번 조건 추가
'''
```





- D2 1989. 초심자의 회문 검사

```python
def palin(word):
    if word == word[::-1]:
        return 1
    return 0

t = int(input())
for i in range(1, t+1):
    word = input()
    print(f'#{i} {palin(word)}')
```