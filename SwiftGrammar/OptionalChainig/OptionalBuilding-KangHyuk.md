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
