### Queue

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
  - 퀴의 뒤에서는 삽입만, 큐이 앞에서는 삭제만 이루어짐
- 선입선출구조(FIFO: First In First Out)
- 큐의 줄이 너무 길어질 때 -> 큐를 여러 개 만들어 나눠 사용함

- 삽입, 삭제의 두 위치를 모두 관리해야

  - 각각 Front(꺼내진 위치)와 Rear(저장한 위치), 초기에는 -1로 초기화해놓음
  - 삽입 - enQueue
  - 삭제 - deQueue

- isEmpty() & !isEmpty()

- 상태 표현

  - 초기상태: front = rear = -1
  - 공백상태: front = rear
  - 포화상태: rear = n-1 (리어의 값이 마지막 칸의 인덱스일 때 - 더이상 추가할 수 없음)

- 큐의 크기를 어떻게 정해야?

  - 문제를 통해 파악할 수 있고, 대략 백만 번

- ```
  def enQueue(item):
    global rear
    if isFull(): print("Queue_Full") #디버깅을 위한 코드, 큐가 꽉 찬 상태를 항상 고려해야
    else:
      rear <- rear + 1;
      Q[rear] <- item;
  ```

- ```
  deQueue()
  	if(isEmpty()) then Queue_Empty(); #역시 큐가 비어있는 상황을 고려해야
  	else {
  			front <- front + 1;
  			return Q[front];
  	}
  end deQueue()
  ```

- ```
  def isEmpty():
  	return front == rear
  	
  def Full():
  	return rear == len(Q) - 1
  ```

- ```
  #검색, 가장 앞에 있는 원소를 검색하여 반환하는 연산
  #front는 옮겨가지 않음. 즉 실제로 꺼내지는 않고 확인만 함
  
  def Qpeek():
  	if isEmpty(): print('Queue_Empty')
  	else: return Q[front + 1]
  ```

- ```python
  #1,2,3 넣고 1,2,3 순서로 꺼내서 출력
  #정석으로 구현
  def enq(n):
    global rear
    if rear == len(q) - 1:
      print('Full')
     else:
      rear += 1
      q[rear] = n
      
  q = [0] * 3
  front = -1
  rear = -1
  
  
  #간단하게 구현(큐과 꽉 찬 걸 확인해야할 경우가 많지 않기 때문)
  #enq(1)
  rear += 1
  q[rear] = 1
  #enq(2)
  rear += 1
  q[rear] = 2
  #enq(3)
  rear += 1
  q[rear] = 3
  
  
  #deq
  front += 1
  print(q[front])
  front += 1
  print(q[front])
  front += 1
  print(q[front])
  
  
  #사용예1
  while front != rear:
    front += 1
    print(q[front])
    
    
  #사용예2
  Q = []
  Q.append(1) #enq(1)
  print(Q.pop(0)) #deq()
  
  ```

- 작업순서 문제 - 위상정렬 알고리즘의 꼴이 위의 꼴











### 원형 큐

- 선형 큐 이용시의 문제점

  - 실제로는 비어있음에도 불구하고 꽉 차있다고 판단하여 더 이상의 삽입을 수행하지 않는 경우

  - 메모리를 둥글게 말아서 해결 (Index의 순환)

    - rear가 끝까지 갔다면, 다시 처음으로 돌아감, 인덱스를 다시 앞쪽으로 돌려보냄
    - 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용
    - 비어있는 공간을 조금 더 효율적으로 사용할 수 있지만, 원형큐라고 해서 full인 상태가 나타나지 않는 것은 x
    - 크기 정하는 것이 애매
    - 확률적으로 어느정도 가면 디큐가 일어나지 않을까 - 에 대한 가정으로 사용하는 것
    - 이를 위해 나머지 연산자 mod를 사용함

  - 확인작업을 덜 하기위한 방법

    - front가 있는 자리는 사용하지 않고 항상 빈자리로 둠 (공백과 포화 상태를 구분하기 위해)
    - front가 빼고 빈칸이 없는 상황(rear의 다음 칸이 front인 상황)을 full로 인식

  - |        | 삽입위치               | 삭제위치                  |
    | ------ | ---------------------- | ------------------------- |
    | 선형큐 | rear = rear + 1        | front = front + 1         |
    | 원형큐 | rear = (rear +1) mod n | front = (front + 1) mod n |

- 원형 큐 구현

  - ```
    def isEmpty():
    	return front == rear
    	
    def isFull():
    	return (rear + 1) % len(cQ) == front
    	
    def enQueue(item):
    	global rear
    	if isFull():
    		print("Queue_Full")
    	else:
    		rear = (rear + 1) % len(cQ)
    		cQ[rear] = item
    		
    def deQueue():
    	global front
    	if isEmpty():
    		print("Queue_Empty")
    	else:
    		front = (front + 1) % len(cQ)
    		return cQ[front]
    ```











### Linked List를 이용한 큐

- 인덱스 상 뿐만 아니라, 메모리 안에서, 즉 물리적인 주소로도 연결되어있는 배열
- 다음 칸의 위치를 저장하는 방식으로 메모리를 사용하는 방식
  - 필요할 때마다 메모리를 추가로 부여받아 사용할 수 있는 장점
  - 느려질 수 있고 구현이 복잡하다는 단점
- 연결 큐 구현 (pass)











### 우선순위 큐

- 우선순위를 가진 항목들을 저장하는 큐
- FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 됨
- 적용 분야는 다음과 같음
  - 시뮬레이션 시스템 
  - 네트워크 트래픽 제어
  - 운영체제의 테스크 스케줄링
- 최적화 관련 알고리즘 사용 시 우선수위 큐 개념이 필요 (효율 높임) - 최소 스패닝 트리, 프림 알고리즘 등
- 구현
  - 배열 이용
    - 우선순위를 이용한 정렬, 인큐할 때마다 정렬해야한다고? ㅇㅇ heap sort 이용
    - 가장 앞에 최고 우선순위의 원소가 위치하게 됨
    - 배열을 사용하므로 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생함
    - 이에 소요되는 시간이나 메모리 낭비가 큼
  - 리스트 이용
  - 실제 구현은 heap 이용











### 큐의 활용

- 버퍼
  - 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리 영역
  - 버퍼링: 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 의미함
- 버퍼의 자료 구조
  - 입출력 및 네트워크와 관련된 기능에서 이용됨
  - 순서대로 입력/출력/전달되어야 하므로 fifo 방식의 큐가 활용됨
- 키보드 버퍼
  - 키보드 입력 - 키보드 입력 버퍼 - 프로그램 실행 영역(std in(콘솔로 들어오는 입력))
  - 이 때 입력을 모아두는 역할을 큐가 담당함

