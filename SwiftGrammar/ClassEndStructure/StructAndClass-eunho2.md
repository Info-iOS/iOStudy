# 구조체와 클래스(Struct & Class)

---

# 구조체

---

<aside>
🐍 구조체 : Swift Loves Struct
           : class 친구

</aside>

> 구조체가 무엇인가?
> 

---

- 구조체란 인스턴스의 값(프로퍼티)을 저장하거나 기능(메서드)을 제공하고 이를 캡슐화할 수 있는 스위프트가 제공하는 타입(named type)

<aside>
😒 - 구조체 안의 변수 : “속성(property)”
- 구조체 안의 함수 : “메서드(method)”

</aside>

![스크린샷 2024-03-04 오후 3.09.10.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-04_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.09.10.png)

- *캡슐화…?
    - 하나의 객체에 대해 그 객체가 특정한 목적을 위해 필요한 변수나 메서드를 하나로 묶는 것을 의미한다.
    
    > 왜 필요한가?
    > 
    - 묶음으로 인해 프로그램을 바라보는 단위가 커진다. ⇒ 프로그램의 규모가 커질수록 중요하다. ⇒ 캡슐화를 통해 프로그램 관리가 좀 더 수월해진다.
    - 객체지향 프로그램의 특징으로 프로그램 소스를 클래스 단위로 바라보게 됨으로써 좀 더 복잡하고 커다란 소스코드도 쉽게 이해하게 된다.
    
    ![스크린샷 2024-03-04 오후 3.17.09.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-04_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.17.09.png)
    

> init() 어디감??
> 

---

- class의 경우 초기화 작업이 있고 초기화 작업을 통해 인스턴스에 매개변수를 변경해줄 수 있다.
- 하지만 구조체에서는 자동으로 초기화 코드를 만들어 준다.

![스크린샷 2024-03-04 오후 3.21.11.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-04_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.21.11.png)

- 위에 코드에서 name속성의 값을 선언하지 않고 인스턴스의 선언시 매개변수로 넣었다. 클래스의 경우 init()코드를 작성해야 하지만 구조체에서는 자동으로 초기화 코드를 만든다.

> 구조체 초기화(Initialization)
> 

---

- 초기화 코드를 작성할 수도 있다. 하지만 초기화 코드를 직접 정의하면 자동 초기화 코드는 더 이상 제공받지 못한다.

![스크린샷 2024-03-04 오후 3.28.30.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-04_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_3.28.30.png)

> 타입 프로퍼티 (static)
> 

---

- 타입 프로퍼티 : 구조체 타입 자체가 사용할 수 있는 프로퍼티
- 타입 메서드 : 구조체 타입 자체가 사용할 수 있는 메서드

![스크린샷 2024-03-05 오전 7.08.51.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-05_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_7.08.51.png)

*인스턴스 를 통해 사용할 경우 에러가 발생함.

![스크린샷 2024-03-05 오전 7.10.23.png](%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%AA%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A2%E1%84%89%E1%85%B3(Struct%20&%20Class)%2097626a314aa847878f964abaf0f1a21b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-03-05_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_7.10.23.png)

// error 내용 : static 즉 타입 프로퍼티와 메소드이기 때문에 varSample을 Sample로 변경하라.

# 클래스

---

- 스위프트 클래스는 부모클래스가 없더라도 상속 업시 단독으로 정의가 가능하다.
- 정의할 때는 class라는 키워드를 사용한다.
- 클래스도 구조체와 똑같이 케멜케이스를 사용하여 이름을 짓는다.
- 구조체와 다르게 let으로 선언해도 내부 프로퍼티 값을 변경할 수 있다.

```swift
class 클래스 이름: 부모클래스 이름 {
	프로퍼티와 메서드들
}

```

```swift
class Person {
var height: Float = 0.0
var weight: Float = 0.0
}

```

## 클래스 인스턴스의 소멸

클래스의 인스턴스는 참조 타입이므로 더는 참조할 필요가 없을 때 메모리에서 헤재된다.이 과정을 소멸이라고 하는데 소멸되기 직전 deinit 메서드가 호출된다.

```swift

class Person {
var height: Float = 0.0
var weight: Float = 0.0
}

```

*클래스는 struct와 비슷한 부분이 많아 짧게 정리함

# 구조체 & 클래스

---

## 공통점

- 값을 저장할 프로퍼티를 선언할 수 있습니다.
- 함수적 기능을 하는 메서드를 선언 할 수 있습니다.
- 내부 값에 “.”을 사용하여 접근할 수 있습니다.
- 생성자를 사용해 초기 상태를 설정할 수 있습니다.
- extension을 사용하여 기능을 확장할 수 있습니다.
- Protocol을 여러 개 채택하여 기능을 설정할 수 있습니다.

## 차이점  : 클래스

- 참조 타입입니다.
- ARC로 메모리를 관리합니다.
- 같은 클래스 인스턴스를 여러 개의 변수에 할당한 뒤 값을 변경시키면 할당한 모든 변수에 영향을 줍니다.
- 상속이 가능합니다.
- deinit을 사용하여 클래스 인스턴스의 메모리 할당을 해제할 수 있습니다.

## 차이점 : 구조체

- 값 타입입니다.
- 구조체 변수를 새로운 변수에 할당할 때마다 새로운 구조체가 할당됩니다.
- 즉 같은 구조체를 여러 개의 변수에 할당한 뒤 값을 변경시키더라도 다른 변수에 영향을 주지 않습니다. (값 자체를 복사)