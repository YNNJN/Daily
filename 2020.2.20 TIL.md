## 2020.2.20





### OOP

- Object-Oriented Programming

- Object: 사물 객체 목적

- 즉 프로그래밍의 방법, 패러다임
  - 컴퓨터 프로그램을 명령어를 목록으로 보는 시각에서 여러 개의 독립된 단위, 즉 '객체'들의 모임으로 파악하고자 하는 것
  - 각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있다
  - 명령형 프로그래밍인 절차 지향 프로그래밍에서 발전된 형태를 나타냄, 기본 구성 요소는 클래스, 인스턴스, 속성, 메서드

- 파이썬의 모든 것은 객체이고, class를 이용한다



객체의 공통점

- 객체는 상태를 가지고 있다

- 객체는 행동을 할 수 있다



모든 객체를 개념화

- Person(Class)-종이 인간-머리 보유(속성)-숨을 쉼(행동)-어떤 이(instance)의 취미와 습관(self.attr)

- 객체에 이름을 붙임, Person은 Class, 즉 설계도

- 종관, 혜선, 준현 사람 각각은 instance

- 속성은 attribute

- 행동은 methode

- instance가 갖고 있는 속성들 앞에 self를 붙임. self.attr





#### 클래스

- 선언과 동시에 클래스 객체가 생성됨
- 선언된 공간은 local scope로 사용됨
- 정의된 attribute 중 변수는 멤버 변수로 불림
- 정의된 함수는 메서드로 불림. 메서드는 함수 정의하듯이 정의하면 됨





#### 인스턴스

- ClassName()을 호출함으로써 인스턴스 객체가 생성됨
- 인스턴스 객체와 클래스 객체는 서로 다른 name scope를 가짐
- instance -> class -> global  순으로 탐색함
- 클래스는 특정 개념을 표현하는 껍데기, 실제 사용을 위해서는 인스턴스를 생성해야





```python
#u1는 현재 name 이 없음. 그래서 User class 의 name 을 탐색하여 가져옴
#self가 없는 것은 클래스에 귀속됨. 인스턴스가 참조는 할 수 있되 인스턴스 것이 아님
#user의 이름을 가져옴. 그렇다고 User class 의 name 이 바뀐 것은 아님
#User class 와 인스턴스는 서로 다른 namespace 를 가지고 있음
#메소드를 인스턴스가 모두 사용할 수 있게 하기 위해서 반드시 매 앞 인자에 self를 넣어줘야
u1.change_password('ghdrlfehd!', 'ghdrlfehd123') #클래스에서 정의할 때는 썼는데, 인스턴스에서 호출할 때는 self를 쓰지 않아도 됨. 자기 자신이 알아서 호출해서 들어감


#self.username이 처음부터 있도록 프로그래밍, 갖고 태어남
#기존엔 인스턴스가 가진 게 아무것도 없었음. 다 클래스의 것
def __init__(self, username, password): #인스턴스의 생성과 동시에 실행이 됨. 인스턴스의 속성, 변수를 넣어줌
u1 = User('eric', 'eruc123') #각각이 self.username, self.password가 되는 것. 부러 만들고 넣을 필요가 없음
u_test = User() #변수 이름만 쓰는 경우는 거의 없고, self.username이라고 씀
```



``` python
username = '혁호님'
class User:
    username = '노바디'
    password = '노바디123'
    
    def print_username(self): #self를 안 써주면, 전역에 있는 것을 참조함....
        return username #노바디를 username으로 하려면 self.username을 리턴해야 한다
```



``` python
import datetime

today = datetime.datetime.now()
print(type(today)) #데이트 타임 모듈의 데이트 타임이라는 클래스의 객체라는 의미의 아웃풋 출력
print(today) #위의 str 표현과 마찬가지로 사람친화적
print(repr(today)) #파이썬친화적
```







#### 인스턴스와 객체

- 인스턴스와 객체는 같은 것 의미
- 보통 객체만 지칭할 때는 단순히 객체라고 부름
- 클래스와 연관지어서 말할 때는 인스턴스라고 부름



``` python
class MyList:
    data = []
    
    def __init__(self, data):
        self.data = data
        
    def append(self, n):
        if type(n) == list:
            self.data += n
        else:
            self.data += list(n)
            
    def pop(self):
        ans = self.data[-1]
        del self.data[-1]
        return ans
    
    def reverse(self):
        self.data = self.data[::-1]
        
    def count(self,n):
        cnt = 0
        for i in range(len(self.data)):
            cnt += 1
        return cnt
    
    def clear(self):
        self.data = []
        
    def __repr__(self):
        return f'내 리스트에는 {self.data}이 담겨있다'
```







#### self

- 인스턴스 객체 자기 자신
- 특별한 상황을 제외하고는 무조건 메소드에서 self를 첫번째 인자로 설정
- 메서드는 인스턴스 객체가 함수의 첫번째 인자로 전달되도록 되어있음

```python
#greeting 함수의 첫번째 인자 self의 뜻

Person.greeting(p1) #클래스에서 호출할 때는 변수가 자동으로 안 들어가니까 넘겨줘야
Person.greeting(p1) == p1.greeting() #인스턴스에서는 자동으로 호출됨

#그러나 인스턴스 에서 사용될 경우 self 자리에 자동으로 인스턴스 객체가 할당됨
```





#### 생성자/소멸자

- 언더스코어가 있는 메서드는 특별한 일을 하기 위해 만들어진 메서드이기 땓문에 스페셜 메서드 혹은 매직 메서드라고 불림

```python
# 생성자 역시 메서드(함수)기 때문에 추가인자를 받을 수 있음
# 생성과 동시에 인스턴스 변수에 값을 할당함

class Person:
    def __init__(self, name):
        self.name = name
        print(f'응애 {self.name}!!!')
        
    def __del__(self):
        print(f'{self.name}은 떠날게 안녕......')
```

