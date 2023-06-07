# Initialization

---

- 클로저, 구조체, 열거형에서 인스턴스를 준비하기 위한 과정
- 인스턴스의 프로퍼티들마다 초기값을 설정해주고 새 인스턴스를 사용하기 위해 필요한 설정과 초기화를 수행
- swift에서 처음 사용되기 전에 올바르게 초기화 되는 것을 보장
- 클래스 인스턴스는 인스턴스를 메로리에서 제거하는 deinitializer(소멸자)를 지원한다.

저장 프로퍼테를 위한 초기값 설정 방법

- 저장 프로퍼티는 사용하기 전에 반드시 특정 값으로 초기화 해야한다.
- 저장 프로퍼티에 값을 직접 설정하면 프로퍼티 옵저버가 호출되지 않고 값 할당이 수행된다

initailization

- 특정 타입의 인스턴스를 생성
- 간단한 init은 파라미터가 없고 init 키워드만 사용됨

```swift
init() {

}
```

기본 프로퍼티

- 항상 초기값을 갖는다면 기본 프로퍼티 사용하는 것이 좋음
- 기본 프로퍼티에 즉시 초기화하면 타입을 선언하지 않아도 컴파일러가 알아서 해주며 상속시 함께 상속된다.
- ex)인잇

```swift
struct a {
    var b = 10.0
}
```

customizing initialization

- 생성자가 수행되는 것을 매개변수, 옵셔널 프로퍼티, 초기화 중 상수 프로퍼티를 지정하여 생성자를 원하는 데로 할 수 있음
- 라이브러리 만들 때 자주 활용 (물론 개발도)

```swift
struct good {
    var nice: String
    init() {
        nice = "NICE"
    }

    init(nice: String) {
        self.nice = nice
    }
}

let n = good() // NICE
let n = good(nice: "긋") // 긋
```

init 와일드 카드 예제

```swift
struct good {
    var nice: String
    init() {
        nice = "NICE"
    }

    init(_ nice: String) {
        self.nice = nice
    }
}

let n = good() // NICE
let n = good("긋") // 긋
```

init 가상의 이름 주기 예제

```swift
struct good {
    var nice: String
    init() {
        nice = "NICE"
    }

    init(junha nice: String) {
        self.nice = nice
    }
}

let n = good() // NICE
let n = good(junha: "긋") // 긋
```

옵셔널 프로퍼티 타입

- 프로퍼티 최초 값이 없고 나중에 추가될 수 있는 값을 옵셔널로 선언해 사용할 수 있다. 옵셔널 프로퍼티는 자동으로 nil로 초기화 된다.

```swift
struct good {
    var nice: String
    
    init(nice: String) {
        self.nice = nice // 없으면 자동으로 nil
    }
}

let n = good(nice: "NICE") // 최초값
```

- 위와 같이 let으로 설정하면

```swift
let n = good(nice: "NICE")
n.text = "안녕" //에러
```

- let 으로 선언했기에 변경이 불가능하다는 에러가 발생한다

****Default Initializers****

- 모든 프로퍼티가 초기값을 다 가지고 있다면 ****Default Initializers**** 가 된다

```swift
class User{
    var name: String?
    var age = 18
    var password = 12345678
}
var user = User()
```

구조체 타입의 멤버 별 생성자 ****(memberwise initializer)****

- 구조체는 생성자를 정의하지 않으면 ****memberwise initializer를 자동으로 받습니다. Default 생성자와는 다르게 저장 프로퍼티에 default 값이 없을 때 받습니다.****

```swift
struct Size {
    var width = 0.0, height = 0.0
}
let size = Size(width: 2.0, height: 2.0)
```

클래스 상속과 생성자

- 모든 클래스의 저장 프로퍼티와 superclass 에게 상속받는 모든 프로퍼티는 초기화 단계에서 반드시 초기값이 할당되어야한다. swift에서는 클래스 타입에서 모든 프로처티가 초기 값을 보장하도록 2가지를 지원한다.

****지정 생성자와 편의 생성자****

- 지정생성자
    - Designated
    - 클래스의 기본적인 생성자
    - 클래스의 모든 프로퍼티를 초기화하고 적절한 super 클래스의 생성자도 호출하여 슈퍼 클래스의 프로퍼티들도 초기화한다
    - 클래스에는 하나의 지정 생성자가 있는 것이 일반적이다.
    
    ```swift
    init(parameters) {
    
    }
    ```
    
- 편의 생성자
    - ****Convenience****
    - 클래스의 생성자를 보조하는 역활
    - 클래스의 특수한 인스턴스를 만들 때 사용하기 위해 편의 초기화를 정의할 수 있다
    - 필요 없으면 안써도됨
    
    ```swift
    convenience init(parameters) {
    
    }
    ```
    

클래스 타입을 위한 생성자 위임

1. 지정 생성자는 호출 즉시 슈퍼 클래스의 지정 생성자를 호출한다
2. 편의 생성자는 같은 클래스 내의 다른 생성자를 호출한다.
3. 편의 생성자는 지정 생성자를 호출해야만 한다.

요약: designated initializer는 항상 delegate UP 해야하고, Convenience initializer는 항상 delegate across 해야한다.

이니셜라이저의 상속과 오버라이딩

- 서브 클래스는 기본적으로 슈퍼클래스의 생성자를 상속자를 상속하지 않는다.
- 무분별하게 상속되어 복잡하게 돼 서브 클래스에서 이것들이 잘못 초기화 되는 것을 막기 위함
- 모든 프로퍼티의 초기 값이 지정돼 있고, 아무러 커스텀 생성자를 선언하지 않으면, 기본 생성자 init() 으로 사용 가능

지정 생성자와 편의 생성자의 사용

```swift
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "없음")
    }
}

let namedMeat = Food(name: "cake")
let nonMeat = Food() // 없음

```

참고 블로그 설명이 진짜 미쳤음

https://didu-story.tistory.com/218
