# map, filter, reduce

## map

> map() 메서드는 배열 내의 모든 요소 각각에 대해 제공된 함수(callback)를 호출하고 그 결과를 모아서 새로운 배열을 반환함

``` javascript
// 기존의 명령형 코드
let names = []
for (const p of products) {
  names.push(p.name)
}
log(names)

let prices = []
for (const p of products) {
  names.push(p.price)
}
log(prices)


// 리팩토링
// 맵 함수 정의, 추상화
const map = (f, iter) => {
  let res = []
  for (const a of iter) {
    res.push(f(a))
  }
  return res
}

// 이터러블 안의 값에 일대일로 매핑되는 어떤 값을 수집하겠다고, map 함수에 보조함수를 전달하는 방법으로 사용함
// map 함수에 p를 받아서 p의 값을 수집하는 함수를 전달, products를 iter로 줌
log(map(p => p.name, products))
log(map(p => p.price, products))

// 결과로 map 함수를 이용해 로직의 중복을 제거함
// map 함수는 고차함수이기도 함 (함수를 값으로 다루면서 내가 원하는 시점에 인자를 적용함)

```

<br>

### map 함수의 다형성

> 이터러블 프로토콜을 따르기 때문에 다형성이 높음
>
> iterable인 모든 값, 문장인 generator 함수의 결과를 포함하여 사실상 모든 것에 map 가능

``` javascript
// 브라우저에 사용되는 값에 map
log(map(el => el.nodeName, document.querySelectorAll('*')));

// generator 함수를 수집하여 map
function *gen() {
  yield 2
  if (false) yield 3
  yield 4
}

log(map(a => a * a, gen()));
```

<br>

``` javascript
// 새로운 Map 객체(iterable)를 조합을 통해 만들 수 있음
let m = new Map()
m.set('a', 10)
m.set('b', 20)
log(new Map(map(([k, a]) => [k, a * 2], m)))

```

<br>

## filter

> filter() 메서드는 제공된 함수로 구현된 테스트를 통과하는 모든 요소가 있는 새로운 배열을 만듦

- 내부의 값에 대한 다형성은 보조함수를 통해 지원함
- 외부의 값에 대해서는 이터러블 프로토콜을 따름으로써 다형성을 지원함

``` javascript
// 기존의 명령형 코드를 개선하여 리팩토링
const filter = (f, iter) => {
  let res = []
  for (const a of iter) {
    if (f(a)) res.push(a)
  }
  return res
}

log(...filter(p => p.price < 20000, products))
log(...filter(p => p.price >= 20000, products))

log(filter(n => n % 2, [1, 2, 3, 4]))

// 제너레이터 함수를 즉시 실행해서 필터된 결과도 확인 가능
log(filter(n => n % 2, function* () {
  yield 1
  yield 2
  yield 3
  yield 4
  yield 5
}()))

```

<br>

## reduce

> reduce() 메서드는 왼쪽에서 오른쪽으로 이동하며 배열의 각 요소마다 누적 계산값과 함께 함수를 적용해 하나의 값으로 줄임

- 내부의 값에 대한 다형성은 보조함수를 통해 지원함
- 외부의 값에 대해서는 이터러블 프로토콜을 따름으로써 다형성을 지원함

<br>

- 이터러블 값을 다른 값으로 축약해나가는 함수
- 특정한 값을 계속해서 순회하면서 하나의 값으로 누적해나감

- 내부적으로는 재귀적으로 받은 보조함수를 실행하면서 하나의 값으로 누적해나감

``` javascript
// 기존의 명령형 코드
const nums = [1, 2, 3, 4, 5]

let total = 0
for (const n of nums) {
  total = total + n
}
log(total)

const reduce = (f, acc, iter) => {
  // 자바스크립트에서는 acc 값을 optional하게 사용할 수 있도록 구현되어있음
  if (!iter) {
    iter = acc[Symbol.iterator]()
    acc = iter.next().value // acc의 값은 이터레이터 안의 첫번째 값
  }
  for (const a of iter) {
    // 더하는 연산 자체를 보조함수에게 위임함
    acc = f(acc, a) // 계속해서 누적하고 있는 값과 이번에 사용할 값을 넘겨줌
  }
  return acc
}

const add = (a, b) => a + b

// reduce: 특정 값을 누적하면서 하나의 값으로 만들어나가는 데 사용하는 함수
log(reduce(add, 0, [1, 2, 3, 4, 5])) // 15

// 내부 구현
log(add(add(add(add(add(0, 1), 2), 3), 4), 5)) // 15

// acc 값은 optional
// 시작하는 값을 생략을 했을 경우 첫번째 값을 기본값으로 변경하는 방식으로 동작함
log(reduce(add, [1, 2, 3, 4, 5])) // 15

// 1. [1, 2, 3, 4, 5]의 이터러블을 이터레이터로 만듦
// 2. 이터레이터에서 첫 번째 값을 next로 꺼내서 acc로 옮김
// 3. 그리고 동작
log(reduce(add, 1, [1, 2, 3, 4, 5])) // 15

```

<br>

- reduce가 보조함수를 통해 '어떻게 축약할지'를 완전히 위임하기 때문에
- 복잡한 형태의 데이터 역시 축약 가능함

``` javascript
log(
  reduce(
    (total_price, product) => total_price + product.price,
    0,
    products))
```

<br>

## map + filter + reduce 중첩 사용과 함수형 사고

- 함수를 연속적으로 실행
- 오른쪽부터 읽어나감
  - 값(products)으로부터 출발해서 -> ... -> 하나의 값으로 평가를 만들어서 -> log

``` javascript
const add = (a, b) => a + b

// 아래의 두 코드는 똑같이 기능함

log(
  reduce(
    add,
    map(p => p.price,
        filter(p => p.price < 20000, products))))

log(
  reduce(
    add,
    filter(n => n < 20000,
           map(p => p.price, products))))

```

<br>

<br>

<br>