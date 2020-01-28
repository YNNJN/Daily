## 2020. 1. 25 TIL





### Encoding and Decoding



- [Base64 Encoding and Decoding Using Python](https://code.tutsplus.com/tutorials/base64-encoding-and-decoding-using-python--cms-25588)

- 파이썬 문자열의 기본 인코딩은 **UTF-8**
- 문자열을 UTF-8이 아닌 아스키 코드로 처리하고 싶을 때 바이트 객체를 사용함
- **encode()** 메서드: 유니코드  -> 바이트 열
- **decode()** 메서드: 바이트 열 -> 유니코드
- 인코딩 시 출력 장치(콘솔, jupyter notebook이 어떤 인코딩을 지원하는지 알아야)
- **EUC-KR**은 한글 표준 인코딩
- **CP949**는 EUC-KR의 확장형(윈도우 사용), 마이크로 소프트 제작



- bytes로 바이트 객체를 만드는 방법
  - bytes(길이): 정해진 길이만큼 0으로 채워진 바이트 객체를 생성
  - bytes(iterable): 반복 가능한 객체로 바이트 객체를 생성
  - bytes(바이트객체): 바이트 객체로 바이트 객체를 생성
    - b'hello'처럼, 작은따옴표나 큰 따옴표 앞에 b를 붙이면 바이트 객체가 됨
  - 인코딩을 지정하여 객체를 생성할 수도 있음
    - bytes(값, encoding = '인코딩')
    - bytearray(값, encoding = '인코딩')



- bytes와 bytearray 모두 1바이트 단위의 값을 연속적으로 저장하는 시퀀스 자료형
  - 차이는 bytearray는 요소 변경 가능, bytes는 요소 변경 불가능
  - bytearray의 요소에 값을 할당할 시 int가 필요하므로, 문자를 할당할 때는 ord()를 사용하여 문자의 아스키코드(int)를 넣어야 함. 아래의 예시와 같이.
  - x[0] = ord('a')



- D2, 1928. Base64 Decoder 문제

  ```python
  import base64
  t = int(input())
  
  for i in range(1, t + 1):
  
      string = input()
      string_byte = string.encode('ASCII')
      decoded_string = base64.b64decode(string_byte)
      message = decoded_string.decode('ASCII')
      result = f'#{i} {message}'
      print(result)
  ```












### += 연산자



- 기존에 사용하던 변수에 += 으로 값을 대체할 수 있음
- 나아가 각 리스트를 합칠 때도 사용됨
- +연산자는 대칭이기 때문에 a+b과 b+a가 항상 같은 결과를 가져와야
  - 타입이 다를 경우, 좌변 우변 선언 순서에 따라 타입이 변경되므로 error가 발생
- +=연산자는 비대칭이기 때문에, 좌변이 전체의 변수 타입 결정
  - a += b의 경우 a의 타입이 유지됨











### replace()



- argument 첫 번째 인자의 값을 검색해서 두 번째 값으로 치환함
- 세 번째 인자까지 있다면 replace하는 횟수를 의미. 좌측부터 변환함



- for element in list:	리스트에 값이 있는지 확인











### hashable



> An object is hashable if it has a hash value which never changes during its lifetime(it needs a hash() method), and can be compared to other objects(it needs an eq() methond). Hashable objects which compare equal must have the same hash value.



- 객체의 라이프타임 동안 변하지 않는 해시 값을 갖고, 다른 객체와 비교 가능 -> 해당 객체는 hashable
- 즉 모든 not mutable objects -> hashable

- hashable objects
  - integer, float, tupple, frozen sets, string etc.

- mutable objects are not hashable
  - list, carry, sets, dictionary, collections.deque etc.



---



[튜플을 딕셔너리 키로 사용할 수 있을까?](https://lioliolio.github.io/about-python-dictionary-key/)

-> “가변 객체인 리스트는 해시 가능하지 않기 때문에 딕셔너리 키로 사용할 수 없고, 튜플은 불변 객체의 참조만 담고 있는 경우에 딕셔너리 키로 사용가능합니다.”







