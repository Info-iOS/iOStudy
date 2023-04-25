# Dependency Injection(의존성 주입)

---

# Dependency(의존성)

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

# ****Injection (주입)****

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

# Dependcy Injection (의존성 주입)

### 사용이유

- Unit Test가 용이해진다.
    - Unit Test란 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 단계이다.
- 코드의 재활용성을 높여준다.
- 객체 간의 의존성(종속성)을 줄이거나 삭제 할 수 있다.
- 객체 간의 결합도 낮추면서 유연한 코드를 작성할 수 있다.