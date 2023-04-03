# High Oder Function

## 고차함수

고차함수는 다른 함수를 인자로 받거나, 함수의 결과로 함수를 반환하는 함수를 의미합니다. 스위프트에서는 map, filter, reduce 가 콜렉션 타입 내에 정의되어 있습니다.

## map

map 은 콜렉션 내부의 데이터를 가공하여 새로운 콜렉션을 생성합니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numbersPlusOne = numbers.map({ $0 + 1 })
```

## filter

filter 는 콜렉션 내부에서 조건에 맞는 데이터들만 골라 새로운 콜렉션을 생성합니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numbersGreaterThanTwo = numbers.filter({ $0 > 2 })
```

## reduce

reduce 는 콜렉션 내부의 데이터들을 하나로 통합시킵니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numberSum = numbers.reduce(0, { $0 + $1 }) 
let numberSumShortcut = numbers.reduce(0, +)
```