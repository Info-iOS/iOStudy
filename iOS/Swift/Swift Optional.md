# Swift Optional

<br>
<aside>

🧐 **옵셔널이란?**

---

**이 변수에는 값이 들어갈 수도 있고, 아닐 수도 있어(nil)라는 뜻**

- nil을 표현하기 위한 수단 : ?
    
    ```swift
    let someData: Int?
    ```
    
</aside>

```swift
var optionalString: String = nil //error
var optionalString: String? = nil //not error
```

<br>

# Wrapping

![wrap](image/wrap.png)

<aside>
🔍 랩핑

---

**Optional로 선언된 변수들은 값이 있는 것인지, nil인 것인지 wrap되어 있어서 모르는 상태**

- wrap된 상태에서는 **변수의 value값이 바로 출력되지 않음**

```swift
var optionalString: String? = “Hello”
print(optionalString)
// 출력 결과: Optional(“Hello”)
```

</aside>

<br>

### Forced Unwrapping 🗺️

---

<aside>

💪 **강제 언랩핑**

**Optional변수를 `!`를 사용해 강제로 언랩핑 하는 것**

```swift
var optionalString: String? = “Hello”
print(optionalString)
// 출력 결과: Optional(“Hello”)
```

*위 예제와 같이 옵셔널 변수들은 기본적으로 nill인지 아닌지 알 수 없기 때문에
optional에 감싸져 있습니다*

무조건 변수가 있는 상황이 보장된 경우 느낌표(!) 사용

```swift
var optionalString: String? = “Hello”
print(optionalString!)
// 출력 결과: Hello
```

nil인 변수를 강제 언랩핑 하면 에러

```swift
let value1: String? = nil
let value2: String! = nil // 여기서는 에러가 아닙니다.
print(value1) // nil 출력
print(value2) // error
```

</aside>

<br>

# Optional Building

![OptionalBuliding](image/OptionalBuliding.png)

<aside>

🧱 **Optional Binding**

---

**Optional 타입으로 선언된 변수에 값의 존재 여부를 확인할 수 있도록 해주는 기능**

```swift
let opV: String? = "Hello"

if let value = opV {
    print("\(value)") // opV가 nil이 아니면 실행 : Hello 출력
} else {
    print("opV는 nil") // opV가 nil이면 실행
}
```

- 위 코드에서 value는 if문 안 로컬 변수로 else에선 사용 **X**
</aside>

<br>
<aside>

🌒 **Optional Chaining**

---

**Optional 빌딩에서 ?만 붙인 것으로 nil인 경우 nil을 반환해준다**

```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}
```

nil인 경우

```swift
let john = Person()

if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s)")
} else {
    print("John's residence is \(john.residence)")
}
// Prints "John's residence is nil"
```

*else문에서는 residence가 nil이기 때문에 numberOfRooms를 불러올 수 없다*

nil이 아닌 경우

```swift
let john = Person()

john.residence = Residence()

if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s)")
} else {
    print("John's residence is \(john.residence)")
}
// Prints "John's residence has 1 room(s)"
```

</aside>