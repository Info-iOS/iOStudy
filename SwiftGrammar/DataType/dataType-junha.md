# 데이터 타입

---

Boolean

- 불이라고도 하고 불리언이라고도 부른다
- true, false의 단일 값을 가진다.
- if나 swiftch에서 주로 사용한다.
- Sendable을 상속 받고 있습니다.
    - int.type과 같이 암시적으로 프로토콜을 준수합니다.

```swift
//근본(지정)
let a: Bool = true
let b: Bool = false

//근본(선언)
let a: Bool?
```

```swift
//이럴 경우 any 타입으로 인식후 값을 자동 저장
let a = 10 > 12 // a = false 저장
let b = 10 && 10 // b == true 저장
```

if문 사용 예제

```swift
let a = true 

if a == true {
    print("true")
} else {
    print("false")
}
```

Int와 UInt

Int는 +,- 정수를 담을 수 있습니다. 하지만 UInt는 -를 포함하지 않고 0 까지만을 허락 하는 int 타입의 정수입니다.

int와 UInt는 각각 8비트, 16비트, 32비트, 64비트의 형태가 있습니다.

int8, int16, int32, int64 / uint8, uint16, uint32, uint64 등 데이터 타입에 따라서 분리되있습니다.

보통 우리가 쓰는 Int는 Int64를 사용하고 있는 것과 같습니다. UInt도 UInt64를 사용하는 것과 같습니다.
