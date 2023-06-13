# Generic

---

### 정의

---

- 제네릭은 요구 사항에 따라 모든 타입에서 동작할수 있는 더 유연하고 재상용 가능한 함수와 타입을 작성할 수 있도록 해준다.

### 장점

---

- 중복을 피할 수 있으며 명확하고 추상적인 방법으로 그 의도를 표현할 수 있는 코드를 작성할 수 있다.
- 컴파일러가 코드에서 사용되는 타입을 체크하여 타입 안정성을 보장할 수 있다.
- 컴파일 타임에 타입 에러를 감지하여 런타임 에러를 방지하고 코드의 안정성을 높일 수 있다.

### 실전

---

```swift
// 두개의 수를 바꾸는 함수를 구현
func swapTwoInts(_ a: inout Int, _ b: intout Int) {
	let tempA = a
	a = b
	b = tempA
}
//위 코드처럼 만들면 파라미터 타입이 모드 Int형일 경우에 만 가능하기 때문에 Double, String을 바꾸는 함수를 또 만들어야한다.
func swapTwoDoubles(_ a: inout Double, _ b: intout Double) {
	let tempA = a
	a = b
	b = tempA
}

func swapTwoStrings(_ a: inout String, _ b: intout String) {
	let tempA = a
	a = b
	b = tempA
}
//이렇게 해주면 Double, String을 사용할 수 있긴 하지만 코드가 매우 길고 비효율적이다.

//이럴 때 제네릭을 사용해서 타입에 제한을 두지 않는 코드를 사용해 더 코드를 효율적으로 짤 수 있음.
// T는 Type Parameter임, T는 굳이 T가 아니여도 되고 원하는 이름으로 해도 되고 콤마를 사용해 여러 개 선언 가능하다
func swapTwoValues<T>(_ a: inout T, _ b: intout T) {
	let tempA = a
	a = b
	b = tempA
}

// 제네릭으로 선언해준 함수를 사용할 때
var someInt = 1
var aotherInt = 2
swapTwoValuse(&someInt, &aotherInt) //함수 호출시 T는 Int 타입

var someString = "Hi"
var aotherString = "Bye"
swapTwoValues(&someString, &aotherStirng) // 함수 호출시 T는 String 타입

swapTwoValues(&someInt, &aotherStirng)
```