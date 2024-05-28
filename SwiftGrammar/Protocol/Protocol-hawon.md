# 프로토콜

## 프로토콜(Protocol)이란?

특정 역할을 수행하기 위한 메서드, 프로퍼티, 기타 요구사항 등의 ❣️청사진

❣️청사진은 원래 건축과 공학에서 사용되는 설계 도면을 의미한다. 비슷하게 프로토콜에서는 데이터 통신을 위해 어떤 규칙과 절차를 따라야 하는지 명확하게 정의한 설계서라는 의미임

### 1) 프로토콜 정의하는 법

```swift
protocol Band {
    var drum: String   { get set }
    var vocal: String  { get set }
    var piano: String  { get set }
    var guitar: String { get set } 

    func play()
}
```

**‼️**프로퍼티를 선언하여 값을 직접 정의하고, 메서드를 직접 구현 하는 것이 아님!!

**이 프로토콜을 따르려면 이러 이러한 것들이 필요하다 라는 약속을 정의**해두는 것임

위에 코드는 

***Band라는 프로토콜을 따르기 위해선 drum vocal piano guitar 프로퍼티가 반드시 정의***

***되어 있어야 하고, play란 메서드가 반드시 정의되어 있어야 한다는 뜻***

➡️ 어떤 기능을 수행할 때 필요한 어떠한 프로퍼티, 메서드에 대해 구현하는 것이 아닌, "선언"만 해두는 것

‼️프로퍼티 요구는 항상 var 키워드를 사용함!

저 위 코드에서 `{ get set }` 이 뭐냐면 get은 읽기만 해도 상관 업썽이라는 뜻이구 get과 set을 모두 명시하면 읽기 쓰기가 다 가능해야 해! 라는 뜻이담.

### 2) 프로토콜 채택하는 법

```swift
struct ABand: Band {}
```

위 코드는 ABand를 생성할 때 필요한 요소들을 미리 정의해둔 Band라는 프로토콜(약속)을 따르고 싶다는 뜻임

상속처럼, Band라는 프로토콜을 클래스 이름 옆에 선언해주는 것만으로 **해당 프로토콜을 "채택"** 하게 되는 것임

```swift
class ABand: Band {
    var drum:   String = "A"
    var vocal:  String = "B"
    var piano:  String = "C"
    var guitar: String = "D"
    
    func play() {
        print("day6 예뻤어 연주 중!")
    }
}
```

이제 약속처럼 Band 프로토콜 안에 선언만 되어있던 애들을 채택한 곳인 ABand에 구현해준 것임

---

### 근데 근데 근데 만약에

**프로토콜 안에 선언되어 있는 프로퍼티 / 메서드는 모두 필수적인 건데, 있을 수도 없을 수도 있는 애가 있다면??**

➡️ 예상했듯, optional을 사용하면 됨!

```swift
@objc protocol Band {
    var drum: String   { get set }
    var vocal: String  { get set }
    var piano: String  { get set }
    var guitar: String { get set }
    @objc optional var bass: String { get set } 

    func play()
}
```

요렇게 ㅎㅎ

bass란 프로퍼티 앞에 @objc optional을 붙일 경우(프로토콜에도 당연히 @objc 선언)

이땐 bass라는 프로퍼티에 한해서 required가 아닌 optional로 바뀜!

➡️ 채택해주는 곳에서 꼭 선언해주지 않아도 에러가 안 남

‼️ **@objc라는 문법을 붙이는 순간 Objective-C에서도 사용될 수 있단 것인데, Objective-C에서 프로토콜은 오로지 "클래스 전용"에서만 채택**할 수 있음‼️

## 상속

프로토콜은 하나 이상의 프로토콜을 상속받아 기존 프로토콜의 요구사항보다 더 많은 요구 사항을 추가할 수 있다!

‼️ 구현할 때는 상속받은 프로토콜의 요구사항까지 모두 구현해야 한다. ‼️

```swift
protocol Readable {
    func read()
}
protocol Writeable {
    func write()
}
protocol ReadSpeakable: Readable {
    func speak()
}
protocol ReadWriteSpeakable: Readable, Writeable {
    func speak()
}

struct SomeType: ReadWriteSpeakable {
    func read() {
        print("Read")
    }
    func write() {
        print("Write")
    }
    func speak() {
        print("Speak")
    }
}
```