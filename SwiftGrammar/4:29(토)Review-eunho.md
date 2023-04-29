# 4/29 (토) Review

# Codable, Encoding, Decoding

---

## Codable

---

- Codable은 Encodable과 Decodable이 합쳐진것이다.
    - Encodable은 data를 Encoder에서 변환해주려는 프로토콜로 바꿔주는 것. 모델을 json으로 인코드 해주는 것.
    - Decodable은 data를 원하는 모델로 Decode 해주는 것. json을 내가 원하는 모델로 디코드
    
    ```swift
    struct Person: Codable {
        var name: String
        var age: Int
    } // 이름과 나이
    
    let person = Person(name: "John", age: 30) 
    
    // JSON 인코딩 데이터를 다른형식으로 변환
    if let jsonData = try? JSONEncoder().encode(person),
       let jsonString = String(data: jsonData, encoding: .utf8) {
        print(jsonString)
    }
    
    // JSON 디코딩 다시 원래의 형태로 변환한다
    let jsonString = """
        {
            "name": "Jane",
            "age": 25
        }
    """
    
    if let jsonData = jsonString.data(using: .utf8), 
       let decodedPerson = try? JSONDecoder().decode(Person.self, from: jsonData) {
        print(decodedPerson)
    }
    ```
    

## Encoding

---

- 프로그래밍에서는 데이터를 다양한 형식으로 인코딩하고, 이를 다시 디코딩하여 원래의 데이터로 변환한다.
- 인코딩은 어떤 데이터를 다른 형식으로 변환하는 것을 말한다.
- 인코딩은 주로 데이터의 전송 및 저장에 사용된다.

## Decoding

---

- 디코딩은 인코딩된 데이터를 다시 원래의 형식으로 변환하는 것을 말한다.
- 데이터를 인코딩할 때는 해당 데이터를 다른 형식으로 변환하여 다른 시스템에서도 사용할 수 있도록 한다.
- 해당 데이터를 사용하려면 다시 원래의 형식으로 변환해야 하는데, 이 작업을 디코딩이라고 한다.

# 디바이스가 없을 경우의 개발

---

- 가장 먼저 앱을 코딩했는데 실제로 볼 수도 없고 감도 잡히기 어렵기 때문에 짠 코드를 테스트 해보기 어렵다.

### 없이도 할 수 있는 것들

---

- 코딩 작성 및 수정
- 빌드 및 컴파일
- 로그 분석 및 디버깅

### 없으면 하기 어려운 것들

---

- 앱 UI 디자인 및 레이아웃 테스트
    - 시뮬레이터가 없다면 디바이스마다 직접 앱을 설치하고 실행하여 UI를 확인하고 레이아웃을 조정해야 하는 번거로움이 있다.
- 시뮬레이터 없이는 디바이스마다 직접 앱을 설치하고 실행하여 성능을 확인하고 최적화해야 하는 번거로움이 있다.

# Storyboard

---

### 장점

---

- 결과물을 예측하기 쉬움. 속성을 쉽게 확인가능하다.
- 소스코드를 일일히 파악하지 않아도 UI 확인 가능
- pop, push, present, dismiss를 코드로 치지 않을수도 있다.
- 프로토타입 - 스토리보드는 사용자 인터페이스 및 흐름의 프로토타이핑 및 목업을 단순화한다.
    - SwiftUI 가 나온 지금에 와서 장점으로 불리기 애매함

### 단점

---

- 화면 로딩 시 무겁고 오래걸린다. (스토리 보드 분리로 약간 해결 가능)
- 링크가 끊어졌을 때 파악하기 힘들다 ( IBOutlet, IBAction )
- 협업 문제 ( Diff 로 알기 힘들고, Conflict 나면 해결 어려움 ) - 여러 storyboard로 나눈다
- 데이터 흐름이 표시되지 않는다
- 앱이 커지면 커질수록 가독성이 떨어진다

# Dependency Injection(의존성 주입)

### Dependency(의존성)

---

- 객체 지향 프로그래밍에서 의존성은 서로 다른 객체 사이에 의존 관계가 있다는 것을 말한다. 즉, 의존하는 객체가 수정되면, 다른 객체도 영향을 받는다는 것이다.
- 의존성을 가지는 코드가 많아진다면, 재활용성이 떨어지고 매번 의존성을 가지는 객체들을 함께 수정해 주어야 한다는 문제가 발생한다.
- 이러한 의존성을 해결하기 위해 나온 개념이 바로 Dependency Injection, 의존성 주입이다.

```swift
import UIKit

struct Food {
    func coffee() {
        print("아메리카노")
    }

    func meal() {
        print("피자")
    }
}

struct Person {
    var todayFood: Food
    
    func coffee() {
        todayFood.coffee()
    }
    
    func meal() {
        todayFood.meal()
    }
}
```

Person객체는 Food객체를 인스턴스로 사용하고 있으므로, Eat객체에 의존성이 생긴다.
만약 이때, Food 객체에 중요한 수정이나 오류가 발생한다면, Person 객체도 영향을 받을 수 있다.

---

### ****Injection (주입)****

---

- 주입은 외부에서 객체를 생성해서 넣는 것을 말한다.
- 밑 코드와 같이 init을 사용해서 주입시킬 수 있다.

```swift
class Food:Menu {
    var coffee: String // coffee라는 문자열 변수 생성
    var meal: String  // meal이라는 문자열 변수 생성
    
    init(coffee: String, meal: String) { //상속
        self.coffee = coffee // coffee라는 함수를 변수에 상속
        self.meal = meal // meal이라는 함수를 변수에 상속 
    }
    
    func printCoffee() {
        print("아메리카노")
    }
    
    func printMeal() {
        print("피자")
    }
}

let menu = Food(coffee: "아메리카노", meal: "피자") // 상속된 값을 출력
```

---

## Dependcy Injection (의존성 주입)

---

### 사용이유

- Unit Test가 용이해진다.
    - Unit Test란 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 단계이다.
- 코드의 재활용성을 높여준다.
- 객체 간의 의존성(종속성)을 줄이거나 삭제 할 수 있다.
- 객체 간의 결합도 낮추면서 유연한 코드를 작성할 수 있다.

# Async (비동기)

---

- 실행 시간이 다른 작업들과 독립적으로 실행될 수 있도록 하는 프로그래밍 기술이다.
- 즉, 코드가 실행되는 동안 다른 작업을 수행할 수 있도록 하여 앱의 반응성을 향상시키는 것을 의미한다.

---

### async, await

- 이 구문을 사용하면 쉽게 비동기 코드를 작성할 수 있고 가독성과 유지보수성을 높일 수 있다.

⬇️ 파일 다운로드를 비동기적으로 처리하는 코드

```swift
func downloadFileAsync(url: URL) async throws -> Data {
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}
```

위 코드는 파일 다운로드를 비동기적으로 처리하는 코드

이렇게 하면 다운로드가 완료될 때 까지 기다리지 않고도 코드의 실행을 계속할 수 있다.

---

### GCD (Grand Central Dispatch)

- GCD를 사용하면 백그라운드 스레드에서 작업을 수행하고, 결과를 메인 스레드에서 처리할 수 있다.
- 하지만 GCD대신 async/await 구문을 사용하면 더 간결하고 직관적인 코드를 작성할 수 있다.

# Bounds, Frame

---

- bounds 와 frame은 UIView 의 instance property 이다.

### Frame

---

- frame은 Super View 좌표계에서 View의 위치와 크기를 나타낸다.
- 간단하게 말해서 Super View의 좌표계이다.
- superView의 원점으로부터 x, y축으로 얼마나 떨어져 있는지를 나타낸다.
- superView 좌표계 안에서 현재 view가 사각형 영역으로 차지하고 있는 크기를 나타내기 때문에, view를 회전 시킨다면 frame의 크기는 달라질 수 있다.

### Bounds

---

- 자기 자신의 좌표계 안에서 원점을 결정하므로 별도의 값을 할당하기 전까지는 항상 0으로 초기화 된다.
- 자기 자신의 크기를 나타내서 view가 회전해도 frame과 달리 크기는 항상 같다

```swift
//bounds origin
bounds x = 0.0, y = 0.0
```

# View 객체

---

- 스위프트(Swift)에서의 View 객체는 iOS, watchOS, macOS 등 Apple의 다양한 플랫폼에서 UI를 구성하는데 사용되는 객체이다.
- View 객체는 UI 요소를 표시하는 데 사용된다. 예를 들어, UILabel, UIButton 등은 모두 View 객체의 하위 클래스로 구현된다.

### 예시

---

- ext : 텍스트를 표시하는 뷰
- Image: 이미지를 표시하는 뷰
- Button : 클릭할 수 있는 버튼을 만드는 뷰
- TextField : 사용자가 텍스트를 입력할 수 있는 뷰
- List : 목록을 표시하는 뷰
- NavigationView : 탐색 스택과 함께 사용되는 뷰