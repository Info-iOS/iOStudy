# Generic

## 제네릭

제네릭은 스위프트의 강력한 기능 중 하나이다. 제네릭을 이용해 코드를 구현하면 어떤 타입에도 유연하게 대응할 수 있다. 코드의 중복을 중일 수 있기에 깔끔하고 추상적인 표현이 가능하다. 

```swift
제네릭을 사용하고자 하는 타입 이름 <타입 매개변수>
제네릭을 사용하고자 하는 함수 이름 <타입 매개변수> (함수의 매개변수)
```

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
   let tempA = a
   a = b
   b = tempA
}
```

이렇게 하면 Int형의 제네릭 함수는 구현할 수 없지만 문자열은 구현할 수 없다.

```swift
func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
   let tempA = a
   a = b
   b = tempA
}

func swapTwoStrings(_ a: inout String, _ b: inout String) {
   let tempA = a
   a = b
   b = tempA
}
```

그래서 이렇게 구현하면 실수형과 문자열 테이터 타입을 제네릭 함수로 구현할 수 있다.

하지만 이렇게 표현하게되면 모든 데이터 타입을 구현할 수 없기 때문에 귀찮다. 따라서 밑에 처럼 표현하면 모든 데이터 타입을 구현가능하다.

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
   let tempA = a
   a = b
   b = tempA
}
```