# 함수형으로 리팩토링 (go, pipe, currying)

- 코드를 값으로 다루어 표현력 높이기
  - 코드를 값으로 다룬다는 것은
  - 어떤 함수가 코드인 함수를 받아서 평가하는 시점을 원하는대로 다룰 수 있다는 것 (표현력이 높다)

<br>

## go

> 초기값과 함수를 받아서 순차적으로 함수를 실행하는 함수

- 함수들과 인자를 전달해서 값을 즉시 평가하는 데 사용함

<br>

``` javascript
const go = (...args) => reduce((a, f) => f(a), args)

go(
  add(0, 1),
  a => a + 10,
  a => a + 100,
  log)
  // 111

```

<br>

## pipe

> 함수들을 받아서 함수들을 순차적으로 실행해주는 함수를 리턴하는 함수

<br>

### 동작

1. 처음에는 함수만 받아서 함수를 리턴함
2. 다음으로 인자를 받고 go 함수로 받아두었던 함수들을 실행하면서 인자와 함수들을 전달함

- 파이프 함수는 결국  내부에서 go를 사용하는 함수

- 하지만 go와 달리 인자는 받지 않고 함수만 받음 -> 중첩 실행된 함수를 리턴함

<br>

``` javascript
const pipe = (f, ...fs) => (...as) => go(f(...as), ...fs)

const f = pipe(
  // 인자를 두 개 이상 전달할 수 있도록 하는 코드를 추가
  (a, b) => a + b,
  a => a + 10,
  a => a + 100)

  log(f(0, 1))
  // 111

```

<br>

## go 함수로 가독성 UP

<br>

``` javascript
// 기존 코드
log(
  reduce(
    add,
    map(p => p.price,
        filter(p => p.price < 20000, products)))
)

// go 사용하여 리팩토링
go(
  products,
  products => filter(p => p.price < 20000, products),
  products => map(p => p.price, products),
  prices => reduce(add, prices),
  log
)

```

<br>

## go + curry 조합으로 가독성 UPUP

> [Currying 가이드 번역](https://sujinlee.me/currying-in-functional-javascript/)

### curry

> 함수를 값으로 다루면서 받아둔 함수를 원하는 시점에 평가시키는 함수

- 원하는 개수만큼의 인자가 들어왔을 때 받아두었던 함수를 나중에 평가시킴
- 함수를 받아서 함수를 리턴하는 함수로서
  - n개의 인자를 받던 방식 대신 n개의 함수로 각각의 인자를 받도록 함
  - 부분적으로 적용된 함수를 체인으로 계속 생성해 결과적으로 값을 처리하도록 하는 것이 본질

<br>

``` javascript
// 함수를 받아서 함수를 리턴함
// 1. 리턴된 함수가 실행되었을 때 인자가 두 개 이상이라면 (렝스가 있다면)
// 2. 받아둔 함수를 즉시 실행하고, 아니라면 다시 한번 함수를 리턴함
// 3. 이후에 받은 인자들을 합쳐서 실행함
const curry = f => (a, ..._) =>
        _.length ? f(a, ..._) : (..._) => f(a, ..._)

const mult = curry((a, b) => a * b)

// 사용
const mult3 = mult(3)
log(mult3) // (..._) => f(a, ..._)
log(mult3(2)) // 6
log(mult3(2, 3)) // 6


// 기존 코드
go(
  products,
  products => filter(p => p.price < 20000, products),
  products => map(p => p.price, products),
  prices => reduce(add, prices),
  log
)

// go 리팩토링 - map, filter, reduce에 curry 적용
// -> 모든 함수들이 인자를 하나만 받으면 일단 이후 인자들을 더 받길 기다리는 함수를 리턴하도록 됨
go(
  products,
  products => filter(p => p.price < 20000)(products),
  products => map(p => p.price)(products),
  prices => reduce(add)(prices),
  log
)

// go 함수를 통해서 왼쪽 -> 오른쪽으로의 가독성을 만들고
// currying을 통해서 간결한 표현을 만듦
go(
  products,
  filter(p => p.price < 20000),
  map(p => p.price),
  reduce(add),
  log
)

// 결과로 간결한 코드, 선언적 함수 사용, 문장을 연결해서 사용
// 상품을 가격으로 필터링하고, 가격만 뽑아서, 더한 것을 로그로 찍겠다

```

<br>

``` javascript
products => filter(p => p.price < 20000)(products)
```

⇣

``` javascript
filter(p => p.price < 20000)
```

<br>

## 함수 조합으로 함수 만들기

> 파이프라인으로 만들어진 코드를 조합하여 중복을 제거할 수 있다

<br>

``` javascript
// 기존의 중복된 코드
go(
  products,
  filter(p => p.price < 20000),
  map(p => p.price),
  reduce(add),
  log
)

go(
  products,
  filter(p => p.price >= 20000),
  map(p => p.price),
  reduce(add),
  log
)

// 고차 함수를 함수의 조합을 통해 만들어 중복 제거
const totalPrice = pipe(
  map(p => p.price),
  reduce(add)
)

const baseTotalPrice = predi => pipe(
  filter(predi),
  totalPrice,
)

go(
  products,
  baseTotalPrice(p => p.price < 20000)
  log
)

go(
  products,
  baseTotalPrice(p => p.price >= 20000)
  log
)

```

<br>

### 의미

- 함수를 값으로 다루는 함수들을 조합하여 코딩함으로써
- 코드의 어디에도 비동기가 나타나지 않음
- 비동기 처리에 골머리 앓지 말고 문제 해결만 고민하자

<br>

<br>

<br>