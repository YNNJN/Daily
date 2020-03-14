### 객체

- 객체는 키와 밸류로 구성된 프로퍼티들의 모임

- 객체 생성법
  - 객체 리터럴
  - Object 생성자 함수
  - 생성자 함수를 만들어 사용하면, 속성이 동일한 객체를 여러개 생성할 수 있음 (마치 클래스처럼)
- 속성 접근은 . 또는 []로 가능
  - 반드시 []로 접근해야 하는 경우가 있는데
  - 속성이 스트링 형식이 아닌 경우













### 배열

- Array, list

- JS에서 배열은 값만 존재함

  - 배열 리터럴
    - var a = [1, 2, 3]
  - Array 생성자 함수
    - var b = new Array(1, 2, 3)

- 배열 순회

  - for - 길이만큼 반복문 수행

  ```javascript
  for (var i = 0; i < a.length; i++){
    console.log(i, a[i]);
  }
  ```

  - for... of - 안에 있는 원소 값들을 하나하나 출력
    - 배열 요소만 접근하는 것이 아니라 속성까지 출력할 수 있음
    - 자스에서 배열도 객체라서 속성 설정이 가능하지만, 리스트의 요소가 아니라 객체의 속성이 됨

  ```javascript
  for (var elem of a) {
    console.log(elem)
  }
  ```

  - forEach - 메서드로 접근
    - 함수 자체를 인자로 받음

  ```javascript
  a.forEach(function(elem, idx) {
    console.log(idx, elem)
  })
  ```

  - for... in
    - Object의 모든 속성을 순회함
    - 즉 배열의 요소만 접근하는 것이 아니라 속성까지 출력됨
    - 자스에서 배열도 Object이기 때문에 속성 설정이 가능하지만, 리스트의 요소가 아닌 객체의 속성이 됨
    - 사용 지양

  ```javascript
  for (var i in a) {
    console.log(i, a[i])
  }
  ```


- 메서드

  - sort()
    - 비교 함수(인자)가 없으면 문자열 기준으로 정렬함
    - 비교함수가 있다면 해당 함수의 리턴값이 0보다 크거나 작음으로 정렬함
      - return a-b; (익명 함수의 개념)

  ```javascript
  var number = [4, 2, 5, 1, 3, 100]
  numbers.sort();
  console.log(numbers);
  //output: [1, 100, 2, 3, 4, 5]
  ```

  ```javascript
  var number = [4, 2, 5, 1, 3, 100]
  numbers.sort(function(a,b) {
    return a-b;
  });
  console.log(numbers);
  //output: [1, 2, 3, 4, 5, 100]
  ```




- 배열 메서드

  - 문자열 관련 - join, toString
  - 배열 합치기 - concat

  ```javascript
  var a = [1, 2, 3]
  a.join('-')
  //output: "1-2-3"
  a.toString()
  //output: "1,2,3"
  ```

  ```javascript
  var a = [1, 2, 3]
  a.concat([4, 5])
  //output: [1, 2, 3, 4, 5]
  a + [4, 5]
  //output: "1,2,34,5" //문자열로 자동 형 변환되어 합쳐짐, 메서드를 이용하자!
  a.concat(4, 5)
  //output: [1, 2, 3, 4, 5]
  ```

  

  - 원소 삽입 / 삭제: pust, pop, unshift, shift

  ```javascript
  //push() - 마지막 추가, 길이 반환
  var numArray = [1, 2, 3];
  var arrayLength = numberArray.push(4,5);
  
  //pop() - 마지막 제거, 제거 원소 반환
  var numberArray= [1, 2, 3];
  var removeElement = numberArray.pop();
  
  //unshift() - 앞 추가, 길이 반환
  var numberArray = [1, 2, 3];
  var arrayLength = numberArray.unshift('one', 'two');
  
  //shift() - 앞 제거, 제거 원소 반환
  var numberArray = [1, 2, 3];
  var arrayLength = numberArray.shift();
  ```

  

  - 인덱스 탐색: indexOf
    - 주어진 배열 안에 없는 인덱스라면 -1 반환

  - 배열 조작 - splice (원본을 바꿈) like sort, 원소의 삭제 수정도 가능
  - 배열 자르기 - slice (return함) like sorted

  ```javascript
  var a = [1, 2, 3]
  a.splice(1)
  //output: [2, 3]
  a
  //output: [1]
  ```

  ```javascript
  var a = [1, 2, 3]
  a.slice(-2)
  //output: [2,3]
  a.slice(1,2)
  //output: [2]
  a.slice(1)
  //output: [2,3]
  a.slice()
  //output: [1, 2, 3]
  ```

  - [참조_MDN_Array_splice](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

  

  ```javascript
  var a = [1, 2, 3]
  a.splice(1, 2, '처음', '두번')
  //output: [2,3]
  a
  //output: [1, "처음", "두번"]
  var a = [1, 2, 3]
  a.splice(1, 2, '처음')
  //output: [2,3]
  a
  //output: [1, "처음"]
  ```













### 함수

- 자스 = 함수형 언어
- 자스의 함수: 객체
- 자스의 객체: 생성자 함수 + 프로토타입 (메소드의 집합)
- 자스의 함수: 데이터 타입으로 변수에 할당, 값으로 전달 가능
- 리턴 문이 없을 수 있음 - 없을 때 함수에 undefined 값 반환

- 함수 선언
  - 함수 선언문

  ```javascript
  function sum(a,b) {
    return a + b;
  }
  ```

  - 함수 표현식

  ```javascript
  var sub = function(a,b) {
    return a - b;
  }
  ```

  - 즉시 실행 함수 like lambda

  ```javascript
  (function(a,b){return a*b})(1, 2)
  //output: 2
  ```

  

  - 화살표 함수
    - function 키워드가 화살표(=>)와 동일, 인자((a,b), (r))가 오른, 왼에 각각 있고, 괄호({})는 가장 오른쪽
    - 문법만 기억

  ```javascript
  var sum = (a, b) => a + b //한 줄인 경우 중괄호 생략 가능
  ```

  ```javascript
  var area = (r) => {
    const PI = 3.14;
    return r * r * PI
  }
  ```

  

- 함수 인자의 특징

  - 매개변수 전달에 대한 제한이 없음
  - arguments 객체는 매개변수로 넘겨진 모든 정보를 갖고 있음

  ```javascript
  function foo(a) {
    console.log(arguments);
    return a
  }
  foo()
  //output: Arguments [callee: f Symbol(Symbol.iterator): f]
  foo(1, 2, 3)
  //output: Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
  ```













- 길이가 정해지지 않은 전달 인자를 받는 함수 - ex. max()

```javascript
function max(){
  var max = Number.NEGATIVE_INFINITY;
  //여러 개 값 복사한 배열을 추가함
  for (i=0; i < arguments.length; i++){
    if (arguments[i] > max) max = arguments[i];
  }
  return max;
}
var maxNumber = max(23, 11, 42, 52, 34, 74, 33);
document.writeln(maxNumber);
```



- 변수 test가 배열인지 객체인지 구분하는 함수

```javascript
function objType(test){
  if ((test instanceof Array) || (typeof test == "object" && "length" in test)){
    return "배열";
    /* length 프로퍼티 존재 여부를 검사하여 존재하면 배열, 존재하지 않으면 객체
    이를 Array 객체의 인스턴스에 대해 검사 */
  } else if(typeof test == "object"){
    return "객체";
  } else {
    return "배열이나 객체 아님"
  }
}
```



