# Extensions

익스텐션 기본 문법 

```swift
extension 확장할 타입이름 {
	// 타입에 추가될 새로운 기능
}
```

```swift
extension 확장할 타입 이름: 프로토콜1, 프로토콜2, 프로토콜3... {
    /* 프로토콜 요구사항 구현 */
}
```

새로운 함수적 기능을 class, structure, enumeration, or protocol type에 확장한다는 의미를 지니고 있습니다.

## 연산 프로퍼티 추가

```swift
extension Int {
    var isEven: Bool {
        return self % 2 == 0
    }
    var isOdd: Bool {
        return self % 2 == 1
    }
}

print(1.isEven) // false
print(2.isEven) // true
print(1.isOdd)  // true
print(2.isOdd)  // false

var number: Int = 3
print(number.isEven) // false
print(number.isOdd) // true

number = 2
print(number.isEven) // true
print(number.isOdd) // false
```

익스텐션을 활용해서 Int 정수형 데이터 타입을 확장하여 사용한 것이다.

홀수인지 짝수인지  판단해서 Bool 타입으로 알려주는 연산 프로퍼티이다.

```swift
extension String {
    init(int: Int) {
        self = "\(int)"
    }
    
    init(double: Double) {
        self = "\(double)"
    }
}

let stringFromInt: String = String(int: 100) 
// "100"

let stringFromDouble: String = String(double: 100.0)    
// "100.0"
```

 익스텐션 안에 init 을 사용해서 초기화를 사용할 수 있다.