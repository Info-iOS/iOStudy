# 제네릭

## 1. 제네릭(Generic)이란?

코드의 유연성을 높이고, 재사용성을 높이며, 타입 안전성을 보장하는 방법

### 1) 제네릭 함수(Generic Function)

위는 인자로 오는 두 Int 타입의 값을 swap하는 함수임. (피라미터 모두 Int형이기에 잘 돌아감)

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
   let tempA = a
   a = b
   b = tempA
}
```

하지만, 만약에 피라미터 타입이 String, Double이라면 ❌

하고 싶다면? 아래와 같이 할 수 있음

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

하지만 너무 귀찮음 😏

### **이럴 때 제네릭을 사용함!**

➡️ 타입에 제한을 두지 않는 코드를 사용하고 싶을 시 씀

어케 쓰냐면..

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
   let tempA = a
   a = b
   b = tempA
}
```

이런식으로 사용함

위 코드랑 비교해 보자면 `<T>` 이 생기고 코드가 짧아짐

저게 뭐냐면 꺽쇠를 사용해서 안에 타입처럼 사용할 이름(T)를 선언해줘서 ❣️T를 타입처럼 쓰는 거임

❣️이때 저 T를 Type Parameter이라고 하는데, **T라는 새로운 형식이 생성되는 것이 아니라**,

**실제 함수가 호출될 때 해당 매개변수의 타입으로 대체되는 Placeholder**임

이때, Type Parameter의 이름은 맘대로 해두 댐 근데 보통 단일 문자 or Upper Camel Case 사용함

또, comma(,)를 이용해 여러 개 선언 가능함

함수를 선언하고 싶다면

```swift
omeInt = 1
var aotherInt = 2
swapTwoValues(&someInt,  &aotherInt) // 함수 호출 시 T는 Int 타입으로 결정됨
 
 
var someString = "Hi"
var aotherString = "Bye"
swapTwoValues(&someString, &aotherString) // 함수 호출 시 T는 String 타입으로 결정됨
```

‼️ 실제 함수를 호출할 때, T의 타입이 결정됨 

➡️ 그래서 만약 서로 다른 타입을 피라미터로 전달하면 오류가 남

### **결론 : 똑같은 내용의 함수를 오버로딩 할 필요 없이 제네릭을 사용하면 됨!**

### 2) 제네릭 타입(Generic Type)

제네릭은 함수뿐만 아니라 클래스, 구조체, 열거형에서도 선언 ⭕️

EX)

```swift
struct Stack<T> {
    let items: [T] = []
 
    mutating func push(_ item: T) { ... }
    mutating func pop() -> T { ... }
}
```

고럼 제네릭 타입의 인스턴스 생성을 어케 하냐면

```swift
let stack1: Stack<Int> = .init()
let stack2 = Stack<Int>.init()
```

이렇게 함

제네릭 함수와 똑같이 꺽쇠를 이용하여 어떤 타입인지 명시해 줘야함

이건 배열 생성이랑 똑같이 생겼는데, 배열이 제네릭 타입이기 때문임.

## 2. 타입 제약(Type Constrants)

**제네릭 함수와 타입을 사용할 때 특정 클래스의 하위 클래스나, 특정 프로토콜을** 

**준수하는 타입만 받을 수 있게 제약을 둘 수 있음**

### 1) 프로토콜 제약

만약, 파라미터로 두 개의 값을 받아서두 값이 같으면 true, 다르면 false를 반환하는 함수를 제네릭으로 선언할 때

```swift
func isSameValues<T>(_ a: T, _ b: T) -> Bool {
    return a == b   // Binary operator '==' cannot be applied to two 'T' operands
}
```

이렇게 오류가 남 왜??

➡️ == 이란 연산자는, a와 b의 타입이 Equatable이란 프로토콜을 준수할 때만 사용할 수 있음

제네릭은 타입에 제한을 주지 않는다매? 라고 생각 할 수 있음

하지만, a, b가 Equatable 프로토콜을 준수하는 타입일 수도, 아닐 수도 있기 때문에 오류가 남

이때, 제약을 줘서 사용 할 수 있음 어케 쓰냐면

```swift
func isSameValues<T: Equatable>(_ a: T, _ b: T) -> Bool {
    return a == b               
}
```

요렇게 하면 isSameValues란 함수에 들어올 수 있는 파라미터는 Equatable이란 프로토콜을 준수하는 파라미터만 받을 수 있음 ➡️ 오류 안 남

### 2) 클래스 제약

클래스 제약 같은 경우엔, 프로토콜 제약과 똑같지만, 해당 자리에 프로토콜이 아닌 클래스 이름이 오는 것임

```swift
class Bird { }
class Human { }
class Teacher: Human { } // 상속
 
func printName<T: Human>(_ a: T) { }
```

**요렇게 T: Human** 이런 식으로 클래스 이름을 써주면

```swift
let bird = Bird.init()
let human = Human.init()
let teacher = Teacher.init()
 
printName(bird) // Global function 'printName' requires that 'Bird' inherit from 'Human'
printName(human)
printName(teacher)
```

Human 클래스와 Human 클래스를 상속 받은 Teather 클래스는 printName 함수를 실행시킬 수 있지만,

bird는 실행시킬 수 없음

## 3. 제네릭 확장하기

제네릭 타입인 배열로 예를 들어보겠당🙃

배열을 확장 시키고 싶다면?

```swift
extension Array {
    mutating func pop() -> Element {
        return self.removeLast()
    }
}
```

일단 여기 배열이 있는데 배열같은 경우에는 실제 Array 구현부에서 타입 파라미터가 Element이기 때문에 Element로 사용해야 함

‼️확장에서 새로운 제네릭을 선언하거나, 다른 타입 파라미터를 사용하면 안댐 

where을 통해서 확장 or 제약을 줄 수 있음

```swift
extension Array where Element: FixedWidthInteger {
    mutating func pop() -> Element { return self.removeLast() }
}
```

요런식으루 타입 파라미터 Element가 **FixedWidthInteger라는 프로토콜을 준수해야 한다!** 라는 제약을 준고임

FixedWidthInteger 프로토콜을 준수하는 Array<Int> 형인 nums는 **extension에서 구현된 pop이란 메서드를 사용할 수 있지만,**

FixedWidthInteger 프로토콜을 준수하지 않는 Array<String> 형인 strs는

**extension에서 구현된 pop이란 메서드를 사용할 수 업따**