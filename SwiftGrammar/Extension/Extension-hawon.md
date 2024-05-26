# extension

## 확장(extension)이란?

기존 클래스, 구조체, 열거형 타입에 새로운 Property, Method, Initializer 등을 추가하는 것으로,

원본 타입(소스 코드)에 접근하지 못하는 타입들도 확장해서 사용할 수 있다

‼️ 기존에 존재하는 기능을 재정의 ❌

extension이라는 키워드를 이용하여 확장

```swift
extension 확장할 타입 {
		// 기능 구현
}
```

확장할 타입 = 기존에 정의된 클래스, 구조체, 열거형 등의 타입

## extension?? 어케 쓰는데??

EX) Int 타입에 isEven이라는 프로퍼티를 추가하고 싶음

```swift
extension Int {
	var isEven: Bool {
		return self % 2 ==0
	}
}
```

여기서 Int는 확장할 타입, isEven이라는 새로운 프로퍼티가 기능구현

사용은?

```swift
let number = 10
print(number.isEven) // true
```

요렇게!

### 근데 그러면 상속이랑 뭐가 달라??

|  | 상속 | extension |
| --- | --- | --- |
| 확장 | 수직 확장 | 수평 확장 |
| 사용 | 클래스 타입에서만 사용 | 클래스, 구조체, 프로토콜, 제네릭 등 모든 타입에서 사용 |
| 재정의 | ⭕️ | ❌ |

## extension으로 멀 추가하는데??

많은걸………..

### 1. 연산 프로퍼티

저장 프로퍼티 ❌

```swift
extension Int {
	var half: Int {
		return self / 2
	}
}
```

요렇게 선언하구,

```swift
let num = 100
print(num.half)
```

이렇게 모든 Int 타입에서 사용 기능!

### 2. 메서드

인스턴스 메서드, 타입 메서드 모두 추가 가능

**타입 메서드 - 특정 타입 그 자체에 속하며, 타입 수준에서 동작하는 작업을 수행**

```swift
extension Int {
	static func printZero() {
		print(0)
	}
}
Int.printZero() //0
```

**인스턴스 메서드 - 특정 인스턴스에 속하며, 인스턴스의 프로퍼티에 접근하고 상태를 변경 ⭕️**

```swift
extension Int {
	func printDouble() {
		print(self*2)
	}
}
Int.printDouble() //200
```

### 3. 생성자(initializer)

class 타입에 편의 생성자는 추가할 수 있지만, 지정 생성자는 추가할 수 없음

```swift
extension String {
	init(intTypeNumber: Int) {
		self = "\(intTypeNumber)"
	}
	init(doubleTypeNumber: Double) {
		self = "\(doubleTypeNumber)"
	}
}
```

요렇게 선언하고,

```swift
let stringFromInt: String = String(intTypeNumber: 100) // "100"
let stringFromDouble: String = String(doubleTypeNumber: 100.0) // "100.0"
```

요렇게 사용함!

### 4. 서브 스크립트(Subscipt)

❣️서브 스크립트는 클래스, 구조체, 열거형에서 시퀀스의 멤버 요소에 접근하기 위한 바로가기 첨자

```swift
extension String {
    subscript(idx: Int) -> String? {
        guard (0..<count).contains(idx) else {
            return nil
        }
        let target = index(startIndex, offsetBy: idx)
        return String(self[target])
    }
}
```

요렇게 선언하구,

```swift
let sodeul = "Hello, Sodeul!"
sodeul[0]           // Optional("H")
sodeul[100]         // nil
```

이렇게 []을 통해 원하는 index의 문자에 접근할 수 있음!

### 5. 중첩 타입

```swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
            }
    }
}
```

이렇게 Int 타입의 extension 안에 Kind라는 enum을 중첩해서 선언할 수 있고,

```swift
let num = 100
print(num.kind)      // positive
 
let num2 = -100
print(num2.kind)     // negative
```

요렇게 사용 가능함!