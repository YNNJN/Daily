## 2020.1.22 TIL



-   parameter(매개변수)와 argument(인수)의 구분
    
    매개변수는 함수에 입력으로 전달된 값을 받는 변수를 의미하고 인수는 함수를 호출할 때 전달하는 입력값을 의미한다.
    
    ```
    def add(a, b):  # a, b는 매개변수
        return a+b
    
    print(add(3, 4))  # 3, 4는 인수
    ```
    
-   함수를 정의할 때는 데이터의 형태에 관계 없이 단순히 이름만 적어주면 됨
    
-   print만 하는 것은 '반환'하는 것이 아님. 반환하면 변수에 저장할 수 있게 되는 것
    
    -   print만 할 경우 변수로 지정했을 때 none 값이 출력됨
    
-   함수 정의 시, argument가 없을 경우의 기본 값을 설정할 수 있음
    
    -   def func(p1 = v1):
        
        \->기본값으로 v1이 반환됨
    
-   단, 기본 인자 이후에 기본 값이 없는 인자를 사용할 수는 없음(arg의 경우에)
    
    ```
    def greeting(name='john', age):
        return f'{name}은 {age}입니다.'
    ```
    
    아니고
    
    ```
    def greeting(age, name='john'):
        return f'{name}은 {age}입니다.'
    ```
    
    이게 맞음. 기본값 없는 age가 먼저 오는 인자





-   키워드 인자는 함수를 호출할 때 이용. 직접 변수의 이름으로 특정 인자를 전달할 수 있음. 내가 넣는 인자가 무엇인지를 각각 명시적으로 알려줌. 정의 시에 적어줬던 순서와 다르게 넣어도 ok
-   단, 키워드 인자를 활용한 뒤에 위치 인자를 활용할 수는 없음. 키워드로 시작했으면 키워드만 넣거나, 아님 둘 다 순서 맞춰서 잘 넣거나 해야함.
-   args의 타입은 tuple임





-   ```
    def func(a, b, *args):
    ```
    
    `*args` : 임의의 개수의 위치인자를 받음을 의미
    
    보통, 이 가변인자 리스트는 형식 인자 목록의 마지막에 옴
    
-   ```
    def func(**kwargs):
    ```
    
    `**kwargs` : 임의의 개수의 키워드 인자를 받음을 의미







-   딕셔너리 생성 함수 만들기
    
    ```
    def my_dict(**kwargs):                                #keywords arguments
        result = []
        for key, value in kwargs.items():
            result.append(f'{key}: {value}')
        return ', '.join(result)
    
    my_dict(한국어 = '안녕', 영어 = 'hi')
    
    #{'한국어': '안녕', '영어': 'hi'}
    ```
    
    -   사실 dict()는 출력이 아니라 딕셔너리를 return 함
    
    ```
    def my_fake_dict(**kwargs):
        return kwargs
    
    my_fake_dict(한국어 = '안녕', 영어 = 'hi')
    ```
    
    -   그렇기 때문에 이 fake 함수를 사용해서 딕셔너리를 리턴할 수 있음







-   식별자는 숫자로 이뤄질 수 없다. 키워드 인자로 넘기면 함수 안에서 식별자로 쓰이기 때문
    
    ```
    dict(1 = 1, 2 = 2)                           #안됩니다
    dict([(1, 1), (2, 2)])                    #이렇게 사용해야 합니다
    ```
    







-   키워드 인자와 가변인자 함께 사용
    
-   이처럼 함수가 두 개 값을 반환할 수 있는데, 그 때의 값은 반드시 튜플로 반환된다
    
    ```
    def save_ranking(*args, **kwargs):
        return args, kwargs
    
    result = save_ranking('nick', 'alice', 'tom', fourth = 'wilson', fifth = 'roy')
    print(result)
    ```
    
-   인자 리스트 언패킹
    
    ```
    args = [3, 6]
    list(range(*args))
    ```
    
    -   output: \[3, 4, 5\]
        
    -   \*arg를 통해서, \[3, 6\]이 (3, 6)으로 언패킹되는 것
        

-   \*\*가 있으면, 함수 실행 시 알아서 언패킹되어 실행됨









#### 문제풀이 리뷰

-   달력 출력하기
    
    딕셔너리\[키값\] = 밸류. 정렬은 어떻게 해결할지 아직 모르겠음
    
-   개인정보보호
    
    스트링도\[:\] 슬라이싱 가능
    
-   가운데 문자 꺼내기
    
    실수형으로 출력될 가능성이 있는 숫자형의 경우, int로 변환해주는 작업을 습관화하기
    
-   소수 찾기
    
    break 문을 이 때 쓰는구나. while문 쓸 때 인자를 증감시켜줘야 다음의 루프를 도는 거고.
    
    그렇기에 초기값의 설정과 그 위치의 선정이 중요함.
    
    반복문에도 else가 쓰일 수 있음 (while~else)
    
    이 문제에서 if가 아닌 while과 else의 인덴테이션을 맞춰야 문제를 해결할 수 있었던 이유는?
    
    \->if와 인덴테이션을 맞춰 break 해버리면 else로 가지 않으니까