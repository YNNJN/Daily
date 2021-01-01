# ES6에서의 순회와 이터러블: 이터레이터 프로토콜

> ES6에서 도입된 이터레이션 프로토콜은 데이터컬렉션을 순회하기 위한 프로토콜이다
>
> 이터레이션 프로토콜을 준수한 객체는 for...of문으로 순회할 수 있고 spread 문법의 피연산자가 될 수 있다
>
> Goal: 이터레이터 프로토콜을 준수한 객체를 잘 사용한 함수를 만들고 값을 다루자

<br>

## ES6에서 리스트 순회

> Goal: 이터레이터 프로토콜이 어떻게 동작하고, 순회를 추상화하는지 알아보자

### for...of 문

- 이전보다 간결하고 선언적으로 바뀜

``` javascript
const list = [1, 2, 3]
for (const a of list) {
  log(a)
}
```

<br>

## 이터러블/이터레이터 프로토콜

> ES6에서 제공하는 빌트인 이터러블은 Array, String, Map, Set, TypedArray, DOM data structure(NodeList, HTMLCollection), Arguments
>
> 여기서는 Array, Set, Map을 통해 알아보자

<br>

### 접근

- for of 문으로 순회 시 Set, Map은 인덱스로 접근 불가

- 하지만 값은 찍힘

  - => 아래와 같은 방식으로 동작하는 것이 아님을 의미

  ```javascript
  for (let i = 0; i < list.length; i++) log(list[i])
  ```

- 즉 Array처럼 키와 키에 매핑되는 값을 순회하면서 동작하는 방식이 아님

- 배열은 `Symbol.iterator` 메서드를 소유함

  - `Symbol.iterator`는 어떤 객체의 키로 사용될 수 있음

    ``` javascript
    const arr = [1, 2, 3]
    arr[Symbol.iterator] // f values() { [native code] }
    // 함수를 비워보면
    arr[Symbol.iterator] = null // TypeError: arr is not iterable
    // Array는 iterable인데???
    // for of 문과 Symbol.iterator에 담긴 함수가 연관이 있구나!
    ```

<br>

### 정의

- 이터러블: 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값
- 이터레이터: { value, done } 객체를 리턴하는 `next()`를 가진 값
- 이터러블/이터레이터 프로토콜: 이터러블을 `for...of`, `전개 연산자` 등과 함께 동작하도록 한 규약

``` javascript
// 1. Array
const arr = [1, 2, 3]
arr[Symbol.iterator] // f values() { [native code] }
arr[Symbol.iterator] () // Array Iterator {}
let iterator = arr[Symbol.iterator] ()
iterator.next() // {value: 1, done: false}
iterator.next() // {value: 2, done: false}
iterator.next() // {value: 3, done: false}
iterator.next() // {value: undefined, done: true}
```

<br>

``` javascript
// 2. Map
const map = new Map([['a', 1], ['b', 2], ['c', 3]])
map.keys() // iterator를 리턴함, MapIterator {"a", "b", "c"}
let iterator = map.keys()
iterator[Symbol.iterator] // f [Symbol.iterator]() { [native code] }
iterator.next() // value에 key만을 담음, {value: "a", done: false}

for (const a of map.keys()) log(a)
for (const a of map.values()) log(a)
for (const a of map.entries()) log(a)
```

<br>

``` javascript
// 3. DOM data structure
for (const a of document.querySelectorAll('*')) log(a)
const all = document.querySelectorAll('*')
let iterator = all[Symbol.iterator]()
log(iterator.next())

// 순회 가능한 이유는
// 1. all이라는 값이 symbol.iterator가 구현되어있기 때문
// 2. 실행되서 iterator를 만들고
// 3. iterator는 안의 값을 리턴해주고 있으니
```

<br>

### 이터레이션 프로토콜의 필요성

- 다양한 데이터 소스가 하나의 순회 방식을 갖도록 규정하여 데이터 소비자가 효율적으로 다양한 데이터 소스를 사용할 수 있도록 하기 위해 이터레이션 프로토콜이 필요함
- 이로써 이터레이션 프로토콜은  **데이터 소비자와 데이터 소스를 연결하는 인터페이스의 역할**을 함

<br>

## 사용자 정의 이터러블, 이터러블/이터레이터 프로토콜 정의

- 일반 객체는 이터러블이 아님
  - 일반 객체는 Symbol.iterator 메소드를 소유하지 않기 때문
  - 즉 일반 객체는 이터러블 프로토콜을 준수하지 않으므로
  - for...of 문으로 순회할 수 없음
- 하지만 일반 객체가 이터레이션 프로토콜을 준수하도록 구현하면 이터러블이 됨

```javascript
const iterable = {
  [Symbol.iterator]() {
    let i = 3
    return {
      next() {
        return i == 0 ? { done: true } : { value: i--, done: false }
      }
      // 실행했을 때 자기 자신을 리턴하도록 하는 코드를 추가함
			// 즉 이터레이터로 반환한 값도 이터러블이 되도록 만드는 과정 [well-formed iterable]
      [Symbol.iterator]() { return this }
      // 결과로, 이터레이터로 반환한 값을 for...of문에 넣어도 순회가 가능하게 됨
    }
  }
}
let iterator = iterable[Symbol.iterator]()
for (const a of iterable) log(a) // 모든 값을 순회 가능함을 확인!
```

<br>

### well-formed iterable

- 자기 자신을 반환하는 Symbol.iterator 메서드를 가지고 있음
- 이터레이터로 반환한 값을 이전까지 진행된 자신의 상태에서 계속해서 next() 가능

<br>

### +

- 빌트인 이터러블 뿐 아니라 순회가 가능한 형태의 값을 가진 값들은 대부분 이 프로토콜을 따르기 시작함
- 페이스북의 immutable.js 등

<br>

## 전개 연산자

> 전개연산자도 이터레이터 프로토콜을 따름
>
> 다시 말해 이터레이터 프로토콜을 준수한 객체는 spread 문법의 피연산자가 될 수 있음

``` JavaScript
const a = [1, 2]
a[Symbol.iterator] = null
log([...a, ...[3, 4]]) // TypeError: a is not iterable
```

<br>

<br>

<br>