# 4/7 요약

## if let

if let은 if문 안의 조건문의 값이 nil인지 아닌지 판단하는 문법이다.

조건문이 nill이 아니라면 해당 블럭이 실행되는 구조이다.

```swift
	if let constant name = optional {
			statements
}
```

위 코드는 if let 문법의 기본적인 형태이다.

### if let 예제 코드

```swift
let data: String? = nil
// 결과 : data is nil

let data: String? = "eunho"
// 결과 : data :: eunho

if let str = data {
	print("data :: /(str)")
} else {
	print("data is nil")
}
```

```swift
var name: String? 
var = "eunho"
print(name) //옵셔널 은호

if let myName = name { // name이 nil이 아니라면 참 nil이면 거짓
	print(myName) // name이 nil이 아니라면 
} else {
	print("nil") // name이 nil이라면
}
// 이 코드의 결과 : eunho
```

if let 구문 안에 있는 my name 변수는 지역변수로서 if let 구문 안에서만 사용할 수 있다. 

```swift
var name: String? 
var = nil
print(name) // nil

if let myName = name { // name이 nil이 아니라면 참 nil이면 거짓
	print(myName) // name이 nil이 아니라면 
} else {
	print("nil") // name이 nil이라면
}
// 이 코드의 결과 : nil
```

이와 같이 myName이 name과 다른 즉 nil일 때 라면 거짓이 실행되어 nil을 출력하게 된다.

## 접근 제어자

코드끼리 상호작용을 할 때 소스파일 간, 모듈 간 접근을 제한할 수 있는 기능이다.

### Open

가장 넓은 범위이다. 지정된 요소는 어디서든 사용 가능하다. public과 비슷하지만 약간의 차이가 있다.

Open**은 클래스에만 사용 가능하다.**

Open에서만 클래스가 정의된 모듈 외부에서 override 할 수 있다.

### Public

스위프트 표준 라이브러리에 있는 기본 요소는 모두 open 래밸을 가진 Struct이다. ex)Bool, Int, String.....

클래스가 정의된 모듈 내에서만 override 할 수 있다.

### Internal

요소 앞에 키워드를 쓰지 않아도 자동으로 지정되는 기본값이다.

Internal 래밸을 가진 요소는 모듈 내부에서는 어디서든 사용 가능하다.

### FilePrivate

해당 소스파일 내부에서만 사용 가능하다. (모듈이 같아도 다른 소스파일에서는 사용불가하다)

### Private

가장 한정적인 범위이다. 해당 요소를 정의한 범위 내에서만 사용가능하다.

클래스 내부에 선언된 private 요소는 같은 파일이더라도 사용 불가능하다

### Setter

구조체 or 클래스를 사용하여 저장 프로퍼티를 구현할때 값을 변경할수 없도록 구현할 수 있다.

## High Oder Fuction

### 고차함수

고차함수는 다른 함수를 인자로 받거나, 함수의 결과로 함수를 반환하는 함수를 의미합니다. 스위프트에서는 map, filter, reduce 가 콜렉션 타입 내에 정의되어 있습니다.

### map

map 은 콜렉션 내부의 데이터를 가공하여 새로운 콜렉션을 생성합니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numbersPlusOne = numbers.map({ $0 + 1 })
```

### filter

filter 는 콜렉션 내부에서 조건에 맞는 데이터들만 골라 새로운 콜렉션을 생성합니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numbersGreaterThanTwo = numbers.filter({ $0 > 2 })
```

### reduce

reduce 는 콜렉션 내부의 데이터들을 하나로 통합시킵니다.

```swift
let numbers = [1, 2, 3, 4, 5]
let numberSum = numbers.reduce(0, { $0 + $1 }) 
let numberSumShortcut = numbers.reduce(0, +)
```

## Error Handling

Error Handling은 프로그램에서 에러 조건들에 대해 대응하고 회복하는 프로세스이다.

Swift는 런타임에서 에러가 발생한 경우 해당 에러를 처리하기 위해 throwing, catching 등이 있다.

### 3Throw

Swift에서 에러는 Error 프로토콜을 준수하는 타입의 값으로 표현된다.

```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}

throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```

자판기 오류 예시 코드 

에러를 던지는 것(throwing)은 예기치 못한 무언가가 발생했고 일반적인 실행 흐름을 계속할 수 없다는 것을 가리킨다. throw**문**을 사용하여 에러를 발생시킬 수 있다. 위 코드처럼 코인이 다섯 개 부족하다는 코드도 만들 수 있다.

### Catch

do-catch문을 사용하여 에러를 처리하는 코드 블록을 작성할 수 있다. 만약 에러가 do절 안에서 코드에 의해 발생한다면, catch절 중에서 일치하는 것을 결정해 에러를 처리할 수 있습니다.

## User Defaults

간단하게 말해서 데이터 저장소라고 생각할 수 있다.

UserDefaults를 사용하면 앱의 어느 곳에서나 데이터를 쉽게 읽고 저장할 수 있게된다.

### 사용

UserDefaults를 통해 plist에 데이터를 저장한다.

UserDefaults는 사용자의 정보를 저장하는 싱글톤 인스턴스이다.

간단한 사용자 정보를 저장 및 불러오는게 가능하지만,

내부적으로 plist 파일에 저장되기 때문에 보안상 강력하지는 않다.

```swift
// 데이터 저장
UserDefaults.standard.set("hohyeon", forKey: "userID")
    
// 데이터 불러오기
let aUser:String = UserDefaults.standard.object(forKey: "UserID") as! String 
let bUser:String = UserDefaults.standard.string(forKey: "UserID")!
```

## Generic

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