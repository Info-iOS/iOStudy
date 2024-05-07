# 야곰’s 기초문법 강좌 3

## 기본 데이터 타입

- 타입 종류
    - Bool
    - Int
    - UInt
    - Float
    - Double
    - Character
    - String
    

### **Bool**

```swift
var someBool: Bool = true
someBool = false
```

true와 false만 값으로 가지는 타입

someBool = 1   or   someBool = 0 ❌

### **Int**

```swift
var someInt: Int = -100
```

정수 타입

### **UInt**(양의 정수)

```swift
var someUInt: UInt = 100
```

양의 정수(자연수) 타입

### **Float**

```swift
var someFloat: Float = 3.14
someFloat = 3 //가능
```

실수 타입(32비트)

정수를 넣어도 딱히 상관❌

### **Double**

```swift
var someDouble: Double = 3.14
someDouble = 3
someDouble = someFloat //오류
```

실수 타입(64비트)

정수를 넣어도 딱히 상관❌

### **Character**

```swift
var someCharacter: Character = "😢"
someCharacter = "가" //가능
someCharacter = "A"  //가능
someCharacter = "히히" //오류
```

유니 코드로 표현할 수 있는 모든 문자를 받을 때 선언

한 글자만 가능 두 글자 이상은 문자열!

### **String**

```swift
var someString: String = "안녕하세요.😄"
someString = someString + "하원입니다."
//안녕하세요.😄하원입니다.
```

문자열 타입

유니 코드 사용, 큰따옴표(””) 사용 (여러줄은 큰따옴표 3개 시용)