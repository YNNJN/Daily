## 2020. 2. 6 TIL

- D2 2005. 파스칼의 삼각형 문제



- 2차원 배열 풀이 - 가장 처음 열을 안 쓰지만 만들어둠
  -> 인덱스를 다루는 문제에서 0과 1의 캘리브레이션 없이 문제 풀이 가능
- 문제풀이 후 결과가 0이 아닐 때만 선택해서 출력



```python
t = int(input())
for tc in range(1, t+1):
    n = int(input())
    arr = [[0 for _ in range(n+1)] for _ in range(n)]
    arr[0][1] = 1 #첫째줄은 1로 초기화
    for i in range(1, n):
        for j in range(1,i+2):
            arr[i][j] = arr[i-1][j-1] + arr[i-1][j]

    print('#{}'.format(tc))
    for i in range(len(arr)):
        for j in range(len(arr[i])):
            if arr[i][j]: #결과가 0이 아닐 때
                print(arr[i][j], end=' ')
        print()
```







- D2 2001. 파리퇴치 문제



- 기존에는 슬라이싱으로 풀었었는데, 포문 이용해서만도 전체의 부분을 선택할 수 있음



```python
t = int(input())
for tc in range(1, t+1):
    n, m = [list(map(int, input().split()))]
    arr = [list(map(int, input().split())) for _ in range(n)]

    max_V = 0
    for i in range(n-m+1):
        for j in range(n-m+1):
            for ii in range(m):
                for jj in range(m):
                    print(arr[i+ii][j+jj], end=' ')

        if maxV < sum:
            maxV = sum

    print('#{} {}',format(tc, maxV))
```







- D3 4615. 재미있는 오셀로 게임 문제



- 사방만 확인하는 것이 아닌, 대각까지 모든 방향을 확인해서 돌의 색을 바꿀 수 있는지 확인해야

- 탐색을 하면서 조건을 검색하고 조건을 만족할 때와 아닐 떄의 수행을 다룸(시뮬레이션)
- 문제를 풀면 풀수록 꼬이고 디버깅도 어려워서,,... 부끄럽지만 SWEA 질문 게시판에 누군가가 '여기까지 짰는데 안돼요' 하며 올려놓은 코드를 돌아가게끔 고쳐서,,, 제출했다.



```python
# 가로,세로, 대각선을 탐색해야하므로 델타를 이용해서 이웃 탐색
dr = [-1, -1, 0, 1, 1, 1, 0, -1]
dc = [0, 1, 1, 1, 0, -1, -1, -1]

def check(i, j, color):
    for k in range(8):
        ni, nj = i + dr[k], j + dc[k]  # 탐색할 좌표
        changeList = []  # 변경대상 모아놓을 리스트
        needtoChange = False  # 변경여부 저장 #flag

        while ni >= 0 and ni < N and nj >= 0 and nj < N:
            if board[ni][nj] == 0:  # 새로 탐색하는 부분에 돌이 없으면
                break
            if board[ni][nj] == color:  # 새로놓은돌과 색이 같으면
                needtoChange = True  # 돌을 변경할 필요 있음
                break  # 빠져나옴
            else:
                changeList.append([ni, nj])  # 변경대상 리스트에 좌표 저장
                ni = ni + dr[k]  # 좌표갱신
                nj = nj + dc[k]
        if needtoChange and changeList:  # 바꿔야할 필요가 있고, 리스트에 값이 있으면
            for c in changeList:  # [1,1]
                board[c[0]][c[1]] = color

T = int(input())
for tc in range(1, T + 1):
    N, M = map(int, input().split())  # M : 돌놓기 횟수
    board = [[0 for _ in range(N)] for _ in range(N)]
    center = N // 2
    # 초기 바둑알 세팅
    board[center - 1][center - 1] = 2
    board[center][center] = 2
    board[center][center - 1] = 1
    board[center - 1][center] = 1

    for k in range(M):
        j, i, color = map(int, input().split())
        board[i - 1][j - 1] = color  # 좌표위치에 돌 놓기
        check(i - 1, j - 1, color)  # 새로놓은 돌에의한 변화 확인

    # 게임 종료후 흑/백 돌 세기
    cnt_b = 0
    cnt_w = 0
    for i in range(len(board)):
        for j in range(len(board[i])):
            if board[i][j] == 1:
                cnt_b += 1
            elif board[i][j] == 2:
                cnt_w += 1
    print('#{} {} {}'.format(tc, cnt_b, cnt_w))
```







- D3.5356. 의석이의 세로로 말해요 문제



```python
t = int(input())
for tc in range(1, t+1):
    words = [list(input()) for _ in range(5)]
    col_words = []

    for j in range(15):
        for i in range(5):
            if len(words[i]) > j: #len은 언제나 index보다 1크기 때문에, 이 때의 값만 col_words에 더함
                col_words.append(words[i][j])

    print('#{0} {1}'.format(tc, ''.join(map(str, col_words))))
```







- D4 1211. ladder2 문제



현재 위치에서 갈 수 있는 선택지는 왼, 오, 아래

왼, 오가 선택되면 아래는 생각 안해도 됨 (따라서 아래 코드와 같이, 왼 오 우선조건)



```python
dr = [0, 0, 1]
dc = [1, -1, 0]
```



지나온 길의 조건은 제해줘야됨 (사방탐색, 와일문 돌릴 때 유의할 점)



```python
def search(r, c, arr):
    dr = [0, 0, 1]
    dc = [1, -1, 0]
    direc = ["l","r","d"]
    cnt = 1
    now_r, now_c = r, c
    visited = [] # 지나온 (r,c) 저장
    while now_r < 99:
        for i in range(3):  #새로운 좌표를 계산함
            tr = now_r + dr[i]
            tc = now_c + dc[i]

            if tr < 0 or tc < 0 or tr > n-1 or tc > n-1:  #범위 안인지
                pass
            elif arr[tr][tc] == 0:  #사다리 위인지
                pass
            elif (tr,tc) in visited :  #이미 지나온 곳인지
                pass

            else: #갈 수 있다면
                visited.append( (tr,tc) )
                cnt += 1
                now_r = tr
                now_c = tc
                #print(direc[i],now_r,now_c, cnt)
                break
    return cnt

for tc in range(1, 11):
    t = int(input())
    n = 100
    arr = [list(map(int, input().split())) for _ in range(n)]
    ans = 100 * 100  #최대값으로 미리 설정
    minIdx = 0

    for j in range(n):
        if arr[0][j] == 1:  #i는 시작점
            cnt = search(0, j, arr)
            if ans > cnt:
                ans = cnt
                minIdx = j

    print('#{} {}'.format(tc, minIdx))
```