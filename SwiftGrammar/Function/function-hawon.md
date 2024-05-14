# 함수

### 함수 선언의 기본 형태

func 함수이름(매개변수 1이름: 매개변수 1타입, 매개변수 2이름: 매개변수 2타입 …) → 반환타입 {

함수 구현부

return 반환값

}

ex>

```swift
func sum(a: Int, b: Int) -> Int {
	return a + b
}
```

### 반환 값이 없는 함수

func 함수이름(매개변수 1이름: 매개변수 1타입, 매개변수 2이름: 매개변수 2타입 …) → Void {

함수 구현부

return 

}

```swift
func printMyName(name: String) -> Void {
	print(name)
}
```

이때 Void는 생략⭕

### 매개변수가 없는 함수

func 함수이름() → 반환타입 {

함수 구현부

return 반환값

}

```swift
func maximumIntegerValue() -> Int {
	return Int.max
}
```

### 매개변수와 반환값이 없는 함수

func 함수이름() → Void {

함수 구현부

return

}

```swift
func hell() -> Void { printf("hello") }
```

함수가 간단하다면 줄바꿈 없이 가능

### 매개변수 기본값

은 무엇일까?

매개변수의 기본값은 함수에 매개변수의 값이 들어오지 않아도 자동으로 매개 변수를 갖게 되는 것.

func 함수이름 (매개변수 1이름: 매개변수 1타입, 매개변수 2이름: 매개변수 2타입 = 매개변수 기본값 …) → 반환타입 {

함수 구현부

return 반환값

}

기본값은 갖는 매개변수는 매개변수 목록 중에 뒤쪽에 위치하는 것이 좋습니다.

```swift
func greeting(friend: String, me: String = "yagom") {
print("Hello \(friend)! I'm \(me)")
```

매개변수 기본값을 가지는 매개변수는 생략⭕

```swift
greeting(friend: "hana") // Hello hana! I'm yagom
greeting(friend: "john", me: "eric") // Hello john! I'm eric
```

### 전달인자 레이블

은 언제 사용하는가?

전달인자 레이블은 함수를 호출할 때

매개변수의 역학을 좀 더 명확하게 하거나 함수 사용자의 입장에서 표현하고자 할 때 

func 함수이름(전달인자 레이블 매개변수 1이름: 매개변수 1타입, 전달인자 레이블 매개변수 2이름: 매개변수 2타입 …) → 반환타입 {

함수 구현부

return

}

함수 내부에서 전달인자를 사용할 때에는 매개변수 이름을 사용합니다

```swift
func greeting(to friend: String, from me: String) {
	print("Hello \(friend)! I'm \(me)")
}
```

함수를 호출할 때에는 전달인자 레이블을 사용해야 합니다

```swift
greeting(to: "hana", from: "yagom") // Hello hana! I'm yagom
```

### 가변 매개변수

전달 받을 값의 개수를 알기 어려울 때 사용할 수 있습니다

가변 매개변수는 함수당 하나만 가질 수 있습니다

func 함수이름(매개변수 1이름: 매개변수 1타입, 전달인자 레이블 매개변수 2이름: 매개변수 2타입…) → 반환타입 {

함수 구현부

return

}

```swift
func sayHelloToFriends(me: String, friends: String...) -> String {
	return "Hello \(friends)! I'm \(me)!"
}
print(sayHelloToFriends(me: "yagom", friends: "hana", "eric", "wing"))
// Hello ["hana", "eric", "wing"]! I'm yagom!

print(sayHelloToFriends(me: "yagom"))
// Hello []! I'm yagom!
```

위에 설명한 함수의 다양한 모양은 모두 섞어서 사용⭕

### 데이터 타입으로서의 함수

swift는 함수형 프로그래밍 패러다임을 포함하는 다중 패러다임 언어임

swift의 함수는 일급객체이므로 변수, 상수 등에 저장⭕

매개변수를 통해 전달⭕

### 함수의 타입표현

반환타입을 생략할 수 없음

(매개변수 1타입, 매개변수 2타입 …) → 반환타입

```swift
var someFunction: (String, String) -> Void = greeting(to:from:)
someFunction("eric", "yagom") // Hello eric! I'm yagom

someFunction = greeting(friend:me:)
someFunction("eric", "yagom") // Hello eric! I'm yagom
```

타입이 다른 함수는 할당할 수 없음