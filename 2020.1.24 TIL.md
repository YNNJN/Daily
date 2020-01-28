## 2020. 1. 24 TIL





#### SWEA 문제풀이



#### D1

을 죽 풀었는데요. 그 중 유의미한 배움을 얻었던 문제들을 아래에 정리합니다.



- 1933 거꾸로 출력해 보아요 문제

  - range()에서 처음, 끝, 증감값 세 가지를 설정할 수 있음에 유의
  - range(a, -1, -1)로 인풋한 값에서 -1까지를 -1씩 감소시켜 풀이함

  

- 1936 가위바위보 문제

  - A가 이길 경우를 True로 두고, 해당 경우 A를 출력
  - 몇 가지의 케이스 분류가 필요한 지를 먼저 따지고 풀이하면 조건을 빠짐없이 고려할 수 있을 것

  

- 2050 알파벳을 숫자로 변환하는 문제

  - ord() 함수로 알파벳을 아스키코드로 변환할 수 있고, 대문자 알파벳의 경우 A부터 순차적으로 아스키코드의 값이 1씩 증가하는 형태
  - 따라서 인풋 alpha = A일 때 num = ord(alpha[i])-ord('A')+1, 즉 1로 변환하여 숫자 출력이 가능함

  

- 2056 연월일 달력 문제

  - 문자열 slicing으로 연/월/일 구분해 변수를 지정함
  - 한 달의 날짜 수를 딕셔너리 형태{월: 일}로 지정. 이 때 한 자리수 숫자가 앞에 0을 쓰는 것을 고려하여 키 값을 str으로 받음
  - 변수 또한 day와 day_i 구분하여 지정하고 day_i는 int형으로 변수를 받음
  - 딕셔너리에서 키 또는 밸류 값을 추출하는 방법을 숙지하고, 딕셔너리를 만들었으면 활용을 잘 할 것

  

- 2058 자릿수 더하기 문제

  - str도 iterable 객체이므로 값에 순차적으로 접근할 수 있음에 유의

  

- 2063, 2068, 2070, 2071, 2072의 테스트케이스의 회차를 거듭하고, 각 회당 인풋을 여러 개 받는 문제 

  ```python
  t = int(input())
  
  for i in range(1, t+1):
      l = map(int, input().split(' '))
      
      ...
  ```

  - 위의 꼴로, 테스트 케이스 t번을 입력받아 1부터 t까지의 반복문을 수행함
  - map()을 이용하고, 제시된 입력 값의 형태대로 split(' ') 하여 입력값을 받음

  









#### 그리고 대망의 D2



- 기차로 본가에 가며 1204 최빈값 문제에 도전하였는데요

- 런타임 에러 -> 10개의 테스트 케이스 중 1개 케이스 오답을 거쳐 -> 겨우 pass

  

  1. 런타임 에러

  ```python
  t = int(input())
  
  for i in range(1, t+1):
      scrs = map(int, input().split(' '))
  
  
      cnt = [0 for j in range(101)]
      for scr in scrs:
  
          cnt[scr] += 1
  
      major = max(cnt)
      idx_major = cnt.index(major)
      print(f'#{i} {idx_major}')
  ```

  

  - Python MemoryError trying to split large string

  - 위의 질문이 많이 검색되는 것을 보니 map으로 인풋을 받고, 그것을 한번에 split 하는 작업이 메모리 하중이 큰 것이라 판단하여

    

  2. 오답 (10개의 테스트 케이스 중 9개 정답)

  ```python
      #scrs = list(map(int, input().split(' ')))
      #scrs = input().split(' ')
      
      raw_scrs=input()
      scrs=[]
      while ' ' in raw_scrs:
          idx=raw_scrs.index(' ')
          scrs.append(int(raw_scrs[:idx]))
          raw_scrs=raw_scrs[idx+1:]
  
      cnt = [0 for j in range(101)]
      for scr in scrs:
  
          cnt[scr] += 1
  
      major = max(cnt)
      idx_major = cnt.index(major)
      print(f'#{i} {idx_major}')
  ```

  

  - 한 번에 split하는 것이 아닌, 인풋을 순차적으로 읽어갈 수 있게끔 코드를 짜고자 했습니다
  - 이 때  테스트 케이스를 살피니 1000개의 값 마지막에 space 공백이 있음을 가까스로 확인하여....... while문으로 int를 떼어내어 살 필 수 있게 했고요
  - 그런데 또 오답이었습니다. (단, 최빈수가 여러 개일 때에는 가장 큰 점수를 출력하라)라는 조건을 고려하지 않았기 때문인데요

  

  3. Pass

  ```python
  t = int(input())
  
  for i in range(1, t+1):
      _ = input()
      raw_scrs=input()
      scrs=[]
      while ' ' in raw_scrs:
          idx=raw_scrs.index(' ')
          scrs.append(int(raw_scrs[:idx]))
          raw_scrs=raw_scrs[idx+1:]
  
      cnt = [0 for j in range(101)]
      for scr in scrs:
  
          cnt[scr] += 1
  
      major = max(cnt)
  
      result=[j*(major==cnt[j]) for j in range(101)]
      idx_major=max(result)
      print(f'#{i} {idx_major}')
  ```

  

  - 이름 없이 받는 input()을 _ = input()로 받고
  - 같은 값을 가지는 max(cnt) 중 큰 값을 찾기 위해  마지막 단을 추가했습니다
  - 즉 result=[j*(major==cnt[j]) for j in range(101)]에서 major==cnt[j]값이 참(1)이면 j를 result에 넣고
  - 이 중 max를 새로운 변수에 주어 문제를 해결했습니다













- 아래는 오늘 저의 인고의 시간의 기록입니다
- 처음 마주한 런타임 에러를 해결하는 과정에서 함수의 하중을 처음으로 인식했어요
- 반복문이 꼭 필요한 순간에 대한 판단이 중요하다고 합니다
- 혼자서는 어려웠을 것 같고, 애인과 (기차에서) 함께 머리를 싸맸기에 고군분투할 수 있었어요. 늘 고맙습니다.



- ~~장장 한 시간 가량의 코드 수정 시간~~
- <img src="/Users/myung/Desktop/스크린샷 2020-01-24 오후 10.06.09.png" alt="스크린샷 2020-01-24 오후 10.06.09" style="zoom:50%;" />





