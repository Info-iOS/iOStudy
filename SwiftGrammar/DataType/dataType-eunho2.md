# 기본 데이터 타입

---

> 프로그램 내에서 다뤄지는 데이터의 종류를 뜻한다.
> 

---

- 스위프트의 기본 데이터 타입이 모두 구조체를 기반으로 구현된다.

### Int와 UInt

---

- 정수 타입 : Int
- 양의 정수 타입 : UInt
- ❗️시스템 아키텍쳐에 따라 Int와 UInt의 타입이 달라진다. 32비트, 64비트 차이
- 굳이 양수라고 해서 UInt를 고집할 필요는 없다.
- 두타입을 모두 사용하는 것 보단 통일하는게 좋음

### 예제 코드

---

```swift
import Foundation

var inteeger: Int = -100
let unsigendInteeger: UInt = 50
print("inteeger 값 :  \(inteeger), unsigendInteeger 값 : \(unsigendInteeger)")
print("Int 최댓값 : \(Int.max), Int 최솟값 : \(Int.min)")
print("UInt 최댓값 : \(UInt.max), UInt 최솟값 : \(UInt.min)")

inteeger 값 :  -100, unsigendInteeger 값 : 50
Int 최댓값 : 9223372036854775807, Int 최솟값 : -9223372036854775808
UInt 최댓값 : 18446744073709551615, UInt 최솟값 : 0
```

```swift
// 진수별 정수 표현
import Foundation

let decimalInteger: Int = 28
let binaryInteger: Int = 0b11100
let octalInteger: Int = 0o34
let hexadecimalInteger: Int = 0x1C

print(decimalInteger, binaryInteger, octalInteger, hexadecimalInteger)

28 28 28 28
```

### Bool

---

- 참(true) 또는 거짓(false)만 값으로 가짐

### 예제 코드

---

```swift
import Foundation

var boolean: Bool = true

boolean.toggle()
let iLoveYou: Bool = true
let isTimeUnlimited: Bool = false
print("시간은 무한입니까? : \(isTimeUnlimited)")
```

### Float & Double

---

- 부동소수점을 사용하는 실수(부동소수 타입)
- Double : 64비트
- Float : 32비트

### 예제 코드

---

```swift
var floatValue: Float = 1234567890.1
let doubleValue: Double = 1234567890.1

print("floatValue = \(floatValue) doubleValue = \(doubleValue)")
// 1.234568e+09 1234567890.1
// float는 10진수로 표현할 수 있는 한계를 넘어서 16진수로 표현함

floatValue = 12345.1

print(floatValue)
```

### random(임의의 수 만들기)

---

- 정수, 실수 모두 임의의 수를 만들 수 있다.

### 예제 코드

---

```swift
var num: Int = Int.random(in: -100...100)
var num1: UInt = UInt.random(in: 1...30)
var num2: Double = Double.random(in: 1.5...4.3)
var num3: Float = Float.random(in: -0.5...1.5)

// Double, Float는 자릿 수 끝까지 나옴

print(num, num1, num2, num3)

//-98 30 1.8235742596045639 1.4989741
```

### Character

---

- Character 는 말 그대로 ‘문자’를 의미
- 큰따옴표 사용

### 예시 코드

---

```swift
let appleA: Character = "A"
print(appleA)

let commandCharacter: Character = "😋"
print(commandCharacter)

let 한글변수이름: Character = "ㄱ" // 변수는 원래 한글로 만들면 안됨
print(한글변수이름)\

A
😋
ㄱ
```

### String

---

- 스위프트에서는 손쉽게 문자열을 다룰 수 있다.
- 문자의 나열, 즉 문자열임
- 큰따옴표 사용
- 다양하게 활용 가능함

### 예시 코드

---

```swift
let name: String = "eunho"

var introduce: String = String()

introduce.append("제 이름은")

introduce = introduce + " " + name + "입니다."
print(introduce)

print("name의 글자 수 : \(name.count)")
print("introduce의 글자 수 : \(introduce.count)")

print("introduce 비어 있음? : \(introduce.isEmpty)")

let unicodeScalarValue: String = "\u{2665}" + "\u{2667}"

print(unicodeScalarValue)

제 이름은 eunho입니다.
name의 글자 수 : 5
introduce의 글자 수 : 15
introduce 비어 있음? : false
♥♧
```

### 특수 문자

---

| \n | 줄바꿈 문자 |
| --- | --- |
| \\ | 문자열 내에서 백슬래시 표현 |
| \” | 문자열 내에서 큼따옴표 표현 |
| \t | 탭 문자, 키보드 탭키 효과 |
| \0 | 문자열이 끝났음을 알리는 null문자 |

### Any & AnyObject & nil

---

- Any, AnyObject는 사용하지 않는 것이 좋음 타입은 될 수 있으면 명시
- Any는 스위프트의 모든 데이터 타입을 사용할 수 있다는 뜻
- AnyObject는 Any보단 조금 한정된 의미로 클래스의 인스턴스만 할당할 수 있다.
    - 잠깐 !!! : 인스턴스란 클래스 / 구조체 / 열거형에서 생성된 객체이다.
- nil은 특정 타입이 아니라 ‘없음’을 나타내는 스위프트의 키워드

### 예시 코드

---

```swift
//Any
var someVar: Any = "hello eunho"
someVar = 500.67
someVar = -90
```