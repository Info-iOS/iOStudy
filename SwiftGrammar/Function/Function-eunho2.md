# 함수

---

## 함수 vs 메서드 ❓

---

> 함수 : func이라는 키워드로 생성하는 것 모두 함수임
메서드 : 클래스, 구조체, 열거형 속에 포함되어 있는 함수
> 

```swift
func printEunhoName() {
    print("Eunho")
}
```

*참고사항 : 함수가 더 큰 범주로 함수안에 메서드가 포함됨

## 함수 vs 클로저 ❗️

---

<aside>
🔥 func 키워드를 이용해 이름을 붙여주는 함수들은 모두 클로저

</aside>

![스크린샷 2024-05-14 오후 10.41.13.png](%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20782e9d7e182940f58fe52f77e83adab0/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-14_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.41.13.png)

```swift
// Named Closure
func printEunhoName() { 
    print("Eunho")
}

// Unnamed Closure
let closure = { print("Eunho") }
```

## Argument Label, Parameter Name

---

![스크린샷 2024-05-14 오후 10.43.46.png](%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20782e9d7e182940f58fe52f77e83adab0/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-14_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.43.46.png)

```swift
func sayHello(name: String) {
   print("Hello, \(name)")
}
 
sayHello(name: "Sodeul")

func sayHello(to name: String) { // name은 함수 안에서 사용함
   print("Hello, \(name)")
}
 
sayHello(to: "Sodeul") // name 키워드가 아닌 to
```

### 더 생략 하는 방법

```swift
func sayHello(_ name: String) {
   print("Hello, \(name)")
}

sayHello("Sodeul")
```

# **파라미터로 전달되는 Value 타입의 값은 복사된 상수 값**

---

- 복사 값이기 때문에 원본에는 영향을 미치지 않음
- 파라터로 받아온 값은 상수이기 때문에 변경 불가

![스크린샷 2024-05-14 오후 10.48.06.png](%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20782e9d7e182940f58fe52f77e83adab0/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-14_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.48.06.png)

# **파라미터로 전달되는 Reference 타입의 값은 참조**

---

- 주소를 전달하기 때문에 원본에도 영향을 미침

```swift
func changeName(human: Human) {
    human.name = "Somaker"
}
 
let sodeul = Human.init(name: "Sodeul", age: 10)
changeName(human: sodeul)
print(sodeul.name)
```

# 입출력 파라미터

---

<aside>
🔥 In-Out Parameters : Value 타입의 값을 참조로 전달하는 방법

</aside>

```swift
func sayHello(name: inout String) {
    name = "Somaker"
}
 
var name: String = "Sodeul"
sayHello(name: &name)
print(name)
```

# 중첨 함수 🤔

---

- Swift에선 함수 안에 함수를 선언 가능

```swift
func outer() {
    print("outer")
    
    func inner() {
        print("inner")
    }
}ㄱ
```