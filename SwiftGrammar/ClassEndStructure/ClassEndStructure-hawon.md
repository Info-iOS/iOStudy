# 클래스와 구조체

### 클래스(Class)

- 참조 타입(reference type)
- 인스턴스(instance)를 생성할 때, 실제 객체는 ❣️힙(heap) 메모리에 저장됨.
- 인스턴스를 가리키는 변수는 ❣️스택(stack) 메모리에 저장됨.

❣️힙(heap)은 동적으로 할당된 메모리를 위한 메모리 영역을 가리킴, 일반적으로 프로그램이 실행 중에 필요에 따라 메모리를 할당하고 해제할 수 있는 공간을 제공

❣️스택(stack)은 데이터를 일시적으로 저장하고 임시적으로 사용하기 위한 메모리 구조, 후입선출(LIFO, Last-In-First-Out) 방식

**class 클래스 이름 { ‘코드’ }의 형태**

```swift
class Name {
    var name = "Hawon" // 속성
    
    func my_name() { // 메소드
        print("my name is \(name)")
    }
}

let hawon : Name = Name() // 인스턴스를 만들어 주는 작업 (인스턴스 선언)

print(hawon.name)
hawon.my_name()

hawon.name = "Minsu"
hswon.my_name()
```

### 구조체(Struct)

- 값 타입(value type)
- 스택(stack) 메모리에 직접 저장됨.
- 인스턴스를 생성할 때, 데이터가 복사되어 새로운 공간에 저장됨.

class에서 struct로 바뀜

```swift
struct Name {
    var name = "Hawon" // 속성
    
    func my_name() { // 메소드
        print("my name is \(name)")
    }
}

var hawon : Name = Name() // 인스턴스를 만들어 주는 작업 (인스턴스 선언)

print(hawon.name)
hawon.my_name()

hawon.name = "Minsu"
hawon.my_name()
```

### 클래스(Class)와 구조체(Struct)의 공통점

- 값을 저장할 프로퍼티 선언 ⭕️
- 메서드 선언 ⭕️
- 내부 값에 .을 사용하여 접근 ⭕️
- 생성자를 사용해 초기 상태 설정 ⭕️
- ❣️extension을 사용하여 기능을 확장 ⭕️
- Protocol을 채택하여 기능 설정 ⭕️

❣️extension은 기존 타입(클래스, 구조체, 열거형 등)에 새로운 기능을 추가하는 강력한 기능

### 클래스(Class)와 구조체(Struct)의 차이점

- 클래스 - 상속 ⭕️, 구조체 - 상속 ❌
- 클래스 - 참조, 구조체 - 값
- 클래스 - 초기화(init) 및 해제(deinit) 메서드를 사용하여 인스턴스의 초기화와 메모리 해제를 관리(ARC)
    
    구조체 - 일반적으로 초기화 메서드만 사용하여 인스턴스를 생성하며, 메모리는 스택에 할당되므로 자동으로 해제됨