# 클로저

스위프트에서 함수형 프로그래밍 패러다임을 접할 때 첫걸음으로 꼭 알아야 할 녀석이 바로 클로저이다.  잘 이해한다면 스위프트의 함수형 프로그래밍 패러다임 스타일을 좀 더 명확하게 이해할 수 있다. 

클로저는 일정 기능을 하는 코드를 하나의 블록으로 모아놓은 것을 말한다. 함수를 비슷 한걸 느낄 수 있다. 함수는 클로저의 한 형태이기 때문이다.

## 클로저의 표현

 매개변수와 반환 값의 타입을 생략할 수 있다.

단 한 줄의 표현만 들어있다면 암시적으로 이를 반환 값으로 취급한다.

축약된 전달인자 이름을 사용할 수 있다.

후행 클로저 문법을 사용할 수 있다.

## 기본 클로저

기본 클로저 내용을 포함하여 sorted(by : ) 메서드를 이용해 동일한 기능을 간결하게 표현할 수 있다.

```swift
public func sorted(by areInIncreaseingOrder: (Element, Element) -> Bool) -> [Element]
```

String 타입의 배열 생성하기

```swift
let names: [String] = ["wizplan", "eric", "yagom", "jenny"]
```

## 후행 클로저

클로저를 읽기 쉽게 바꿔볼 수 있다. 클로저가 조금 길어지거나 가독성이 조금 떨어진다 싶으면 후행클로저 기능을 사용하면 좋다. 또한 단 하나의 클로저만 전달인자로 전달하는 경우에는 소괄호를 생략 해줄 수도 있다. 다중 후행 클로저도 사용가능하다.

```swift
let resrved: [String] = names.sorted() { (first: String, second: String) -> Bool in 
return first > second
}
let reserved: [String] = names.sorted { (first: String, second: String) -> Bool in
return first > second
}

func doSomething(do: (Sting) -> Void,
								onSucces: (Any) -> Void,

								onFailure: (Error) -> Void) {
		//do something...
}
```

## 클로저 표현 간소화

메서드의 전달인자로 전달하는 클로저는 메서드에서 요구하는 형태로 전달해야한다. 즉 타입을 같게 맞추어 전달해야 한다는 것. 하지만 클로저는 이미 적합한 타입을사용하여 유추할 수 있다. 그렇기 때문에 구현할 때 매개변수의 타입이나 반환 값의 타입을 굳이 표현해주지 않고 생략해도 문제가 없다뜻이다.

```swift
let reserved: [String] = names.sorted { (first, second) in
		return first > second
}
```

### 단축 인자 이름

```swift
let reserved:[String] = names.sorted {
return $0 > $1
}
```

### 암시적 반환 표현

```swift
let reserved: [String] = names.sorted { $0 > $1 }
```

## 클로저는 참조 타입

두 상수를 정의 했다고 치고 두 상수는 같은 클로저를 참조하기 때문에 동일한 클로저가 동작하는 것을 볼 수 있다.

```swift
let increment ByTwo: (() -> Int ) = makeIncrementer(forIncrement: 2)
let sameWithIncrementByTwo: (() -> Int) = incrementByTwo

let first: Int = incrementByTwo()
let second: Int = smallWithIncrementByTwo()
```

## 자동 클로저

함수의 전달인자로 전달하는 표현을 자동으로 변환해주는 클로저를 자동 클로저라고 한다. 자동 클로저는 전달인자를 갖지 않는다. 자동 클로저는 호출되었을 때 자신이 감싸고 있는 코드의 결괏값을 반환한다.

자동클로저의 사용

```swift
var customersInLine: [String] ["Eunho", "Tyler", "Eunhoo", "Tylerr"]

func serveCustomer(_ customerProvider: @autoclosure () -> String) {
  printf("Now serving \(customerProvider))!")

}

serveCustomer(customersInLine.removeFirst())
```