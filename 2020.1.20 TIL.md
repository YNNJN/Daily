## 2020. 1. 20 TIL



### git



#### (분산)버전관리시스템

로그를 남길 수 있고, 과거의 이력으로 돌아갈 수 있음

1. Working directory: 작업(수정)한 파일 [TIL]
2. INDEX(staging area): 커밋할 목록
   사진을 찍으면 -> 커밋이란 이름으로 기록이 남음
3. HEAD: 쌓인 커밋들
4. github



git은 코드를 관리하는 도구(내 컴퓨터를 벗어나지 않음)

github 협업을 위해 원격 저장소에 코드 이동 가능



CLI: Command Line Interface

GUI: Graphic User Interface

GUI로 해도 되는 거 CLI로 해보면서 익히기



#### gitbash 설치

git-scm에서 다운로드

git bash here -> cmd(윈도우용)창 같은 것 나타남

- 커서 깜빡: 내 명령어 받아들일 준비가 되었다

- 내가 어떤 위치에 있는지를 항상 확인해야

education -> student benefit 받기



#### 명령어

- **pwd** 내가 지금 있는 위치의 전체 경로
- **ls** 경로에 어떤 파일이 있는지를 확인
- **clear** 화면 청소
- **mkdir test** test란 이름의 폴더 생성 -> ls로 확인
- **touch a.txt** 파일 생성
- **echo "hi"** 화면에 문자열을 출력
- echo "hi" **> a.txt** 폴더에 넣음
- **cat a.txt** 안의 내용이 죽 출력이 됨
- echo 뒤에 부등호(>) 하나만 쓰면 그걸로 덮어써지니,
  이전 것과 함께 출력하고 싶으면 **>>** 이용
- **cd**(change directory) 현재위치 이동
- 만든 폴더인 te 입력하고 tab 누르면 자동완성
- **cd..** 한 단계 윗 폴더로 가는 명령어
- **cp**(copy) 명령어를 통해 파일을 복사
  - cp a.txt test/ test란 폴더에 a 파일을 복사



#### 1. add



- **git init** 폴더를 git으로 관리할게
  - master: 모든 변경 사항을 git이 관리하고 있음을 의미. 항상 확인할 것
- **git status** red text로 git의 추적 여부 알려줌
  - **git add a.txt** git이 파일의 변경 사항을 추적하도록
    (working directory -> staging area 으로 파일 이동)
  - 폴더명 뒤에는 '/'붙여서 써줘야 함



#### 2. commit



- **git commit -m "Initial commit"** commit(변경 사항에 대해 사진 찍기) -> commits
  커밋이란 변경사항에 대한 기록, 로그
  - git config --global user.email " "
  - git config --global user.name " "

> $ git commit -m "Initial commit"
> [master (root-commit) f5fc006] Initial commit
>  1 file changed, 0 insertions(+), 0 deletions(-)
>  create mode 100644 a.txt

-> 위의 인용처럼 뜨면 정상적으로 커밋된 것

-> 원격에 있는 폴더를 만들었으니, 로컬에 있는 폴더와 연결시키는 과정만 남음



#### 3. push



- **git remote add origin** https://github.com/YNNJN/TIL.git
  - 원격저장소에 추가(origin은 별명)
  - `shift` + `insert` 로 주소 복사함
- **git remote -v** TIL에 연결된 원격저장소가 있는지를 확인
- **git push origin master** 원격저장소로 TIL에 있는 친구들을 보냄





#### add-commit-push

- add-commit-push의 단계를 기억하기
- 정리하자면

![image-20200120103358280](C:\Users\multicampus\Desktop\YNNJN\TIL\image-20200120103358280.png)

- 타이포라로 read me 만들 수 있음
- git commit -m "Add b. txt" -> convention은 명령어로 해석을 하니, added 아닌 add
- 저장소를 설명하는 문서를 README로 추가함





#### 집에서(원격으로 싸피에서 작업한 코드 공유)

- **git clone** https://github.com/YNNJN/TIL.git
- git init 해줄 필요 없음. 알아서 들어와있으니

![image-20200120103724354](C:\Users\multicampus\Desktop\YNNJN\TIL\image-20200120103724354.png)



- **git pull origin master** 변경된 것만 가져옴
  - 작업 전에 반드시 pull 후 작업할 것





#### 실습(원격으로 집에서 작업한 코드 공유)

c.txt

![image-20200120104601250](C:\Users\multicampus\Desktop\YNNJN\TIL\image-20200120104601250.png)



Q. 변경사항이 생길 때마다(커밋할 때마다) 푸쉬를 해야하는가?

A. 필요할 때만 한번에 깃헙에 올리면(푸쉬) 됨 





#### jupyter notebook



#### 설치

- pip install jupyter

https://drive.google.com/file/d/116kzGvcD08y065F8XOSD1J2h8-k4LtIz/view?usp=sharing

pip: 파이썬에서 사용하는 패키지 관리자

- bash에 jupyter notebook 입력해서 실행

- `shift` + `enter` 하면 실행됨 or 다음 단락으로 넘어감

- 코드 블록을 작성해서 실행시키면 -> In[숫자] 생기는데, 이를 통해 몇 번째 코드를 실행시켰는지 알 수 있음

- `Alt`+ `enter` 새로운 블록이 생김



#### 설치가 매번 귀찮다면

jupyternotebook 항상 실행시키기 귀찮으니

vi ~./bashrc

alias jn"jupyter notebook"

wq

source ~/. bashrc



#### python 문법

- 아래의 예약어는 실행 불가. 변수 함수 만들 때 쓰면 안됨

  False, None, True, and, as, assert, break, class, continue, def, del, elif, else, except, finally, for, from, global, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, with, yield

- = 는 넣는 행위(==와 구분)

- 버전 3부터는 인코딩 선언이 디폴트로 되어있음. 안해도 됨

- 리스트 마지막 값 뒤에 ',' 찍어도 기능함

- 대괄호는 맨 앞에 넣거나, 또는  ' 시작 위치에 넣음
- x, y = y, x -> 값이 바뀜..... 파이썬.... 미친문법....
- 다른 언어의 경우 특정 수를 넘어버리면(overflow) -로 표기됨
- 파이썬은 정수 자료형에서 오버플로우가 없다 -> 빅데이터 등의 수를 다루는 분야에서 파이썬을 활용하는 이유 중 하나

- 컴퓨터식 지수 표현 방식 314e-2 => 3.14
- 실수의 뺄셈 -> 딱 떨어지지 않음 -> (round(3.5-3.12, 2) 함수로 출력)
- 근데 또 3.5-3.12 == 0.38는 False임
- 비어있지 않은 문자열, 리스트는 참임
- None의 타입은 Nonetype
- 특수문자를 사용하기 위해서는 \ 사용
- 'py' 'thon' 이것도 붙어서 출력됨
- 우리가 보통 알고 있는 & |은 파이썬에서 비트 연산자임
- 단축평가 : 첫 번째 값이 확실할 때, 두 번째 값은 확인 하지 않음
- 기초 형 변환 -> 변환 안 되는 것 위주로 기억할 것
- 딕셔너리는 박스에 번호가 아닌 이름이 붙어있는 것이 리스트와의 차이













## Git 기초

> Git은 분산형 버전 관리 시스템(DVCS)이다.
>
> 소스코드의 이력을 관리하고, 협업 단계에서 활용 가능하다.



#### 0. 기본 설정

윈도우에서 git을 활용하기 위해서는 `git bash`가 필요하다.

설치 이후에 `commit`을 작성하는 `author` 설정이 필요하다.

```
$ git config --global user.email "github email"
$ git config --global user.name "github username"
```

설정 내용을 확인하기 위해서는 아래의 명령어를 입력한다.

```
$ git config --global -l			#내가 잘 설정했는지 값이 나옴
```



### gitignore

프로젝트를 진행할 때, `git`으로 관리하지 않을 파일 혹은 폴더들을 설정할 수 있다.

```
*.xlsx					# 확장자가 xlsx인 모든 파일
a.txt					# a.txt 파일
.ipynb_checkpoints/		#ipynb_checkpoints 폴더
```

프로젝트 시작시 어떤 내용을 담아야할지 모르겠다면, gitignore에서 검색한다.

ex) `python`, `jupyter notebook`





## 로컬 저장소에서 활용하기



### 1. git 저장소 설정

특정 프로젝트 폴더에서 git을 활용하기 위해서는 아래의 명령어를 입력한다.

```
$ git init
```

- 해당 디렉토리 내에 `.git`이라는 숨김 폴더가 생성되며, 모든 `git`과 관련된 동작은 해당 폴더에 기록된다.
- git bash에서 `(master)`라는 브랜치 정보가 표기된다.



### add

`git`에서 커밋할 대상 파일을 `staging area`로 이동시키는 명령어이다.

```
$ git add a.txt				# 특정 파일을 stage
$ git add images/			# 특정 폴더를 stage
$ git add.					# 모든 디렉토리 파일 및 폴더를 stage
```



항상 `git status` 명령어를 통해서 현재 상태를 확인하는 것이 중요하다**



### commit

git에서 이력을 남기기 위해서는 commit을 통해서 진행한다.

`commit`을 남길 때에는 항상 커밋 메시지를 작성한다.

메시지는 해당 이력에 대한 정보를 담는다.

```
$ git commit -m "커밋메시지"
```

커밋 이력을 확인하기 위해서는 아래의 명령어를 활용한다.

```
$ git log
```

이후 변경 사항이 발생하기 되면, `add` -> `commit`을 한다.

`add`: 커밋할 대상 파일 선정

`commit`: 이력의 확정





## 원격 저장소(remote repository) 활용하기

> 원격 저장소를 제공해주는 서비스는 다양하다.
>
> 우리는 github을 기준으로 활용.



### 0. 기본 설정

github에 비어있는 저장소(repository) 생성



### 1. 원격 저장소 설정

```
$ git remote add origin http://~(원격저장소 주소)
```

원격저장소(remote)를 origin이라는 이름으로 http://~로 설정한다.

아래의 명령어를 통해 저장된 원격 저장소 목록을 확인할 수 있다.

```
$ git remote -v					# 연결이 잘 되었는지 확인만 하는 거라 필수는 아님
```

혹시 잘못 설정되었다면 아래의 명령어를 통해 삭제 가능하다.

```
$ git remote rm origin
$ git remote -v
```



### 2. push

원격저장소에 업로드하기 위해서는 `push` 명령어가 필요하다.

```
$ git push origin master
```

`origin`으로 설정된 원격 저장소에 `push` 한다.

변경된 사항(`commit`)이 발생했을 때, `git push origin master` 명령어를 통해서 매번 업로드해줄 수 있다.









