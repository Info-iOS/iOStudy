# Swift Closure

<br>
<aside>

😶‍🌫️ **클로저**

---

**코드블럭으로 C와 Objective-C의 블럭, JAVA의 람다와 비슷**

- 어떤 상수나 변수의 참조를 캡쳐해 저장
- 🌦️ 전역 함수 : 이름이 있고 어떤 값도 캡쳐하지 않는 클로저
- 💦 중첩 함수 : 이름이 있고 관련한 함수로 부터 값을 캡쳐 할 수 있는 클로저
- ☀️ 클로저 표현 : 경량화 된 문법으로 쓰이며, 관련 문맥으로부터 값을 캡쳐하는 클로저
    - *이름이 없음 → name-less*
</aside>

<br>

### 정렬 메소드 예시 🌧️

---

<aside>
💡 표준 라이브러리에 `sorted(by:)`라는 메소드의 `by`에 클로저를 넣으면 클로저대로 정렬

</aside>

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

> 배열의 콘텐츠와 같은 타입을 갖고 두개의 인자를 갖는 클로저
`*name`의 콘텐츠는 String 타입이므로 `(String, String) -> Bool`의 타입의 클로저
> 

```swift
// 클로저를 제공하는 일반적인 방법은 함수를 하나 만드는 것
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}

var reversedNames = names.sorted(by: backward)
// ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

<br>

# Closure Expressions

<aside>

🕯️ **클로저 표현**

---

**코드의 명확성과 의도를 잃지 않으면서 문법을 축약해 사용할 수 있는 최적화 방법을 제공**

- 클로저를 명확하게 표현하는 방법으로 문법에 초첨이 맞춰져 있음
- Swift에서 클로저 표현은 최적화 됨, 최적화는 다음과 같은 내용을 포함
    1. 문맥에서 인자 타입과 반환 타입의 추론
    2. 단일 표현 클로저에서의 암시적 반환
    3. 축약된 인자 이름
    4. 후위 클로저 문법
</aside>

<br>

## Syntax 📝

---

```swift
// 클로저 표현 문법의 일반적 형태
{ (parameters) -> return type in
    statements
}
```

```swift
//ex
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

<aside>

<br>

🔥 **문맥에서의 타입 추론**

---

**이미 (String, String) -> Bool 타입의 인자가 들어와야 하는지 알기 때문에 생략 O**

```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

</aside>

<aside>

<br>

🌚 **단일 표현 클로저에서의 암시적 반환**

---

**단일 표현 클로저에서는 반환 키워드를 생략**

```swift
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

</aside>

<aside>
<br>

🏷️ **인자 이름 축약**

---

**자동으로 축약 인자 이름 제공 → 인자 값을 순서대로 $0, $1, $2 등으로 사용**

```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```

</aside>

<aside>
<br>

🌩️ **연산자 메소드**

---

**Swift의 String타입 연산자에는 비교 연산자가 구현해 되어있음**

```swift
reversedNames = names.sorted(by: >)
```
</aside>

<br>

# Trailing Closures

<aside>
<br>

🌈 **후위 클로저**

---

**함수의 마지막 인자로 클로저를 넣고 그 클로저가 길다면 후위 클로저를 사용**

```swift
func someFunctionClosure(closure: () -> Void) {
    // function body goes here
}
```

*이런 형태의 함수와 클로저가 있다면*

```swift
// 위 클로저의 인자 값 입력 부분과 반환 형 부분을 생략해 다음과 같이 표현
someFunctionClosure(closure: {
    // closure's body goes here
})
```

```swift
//후위 클로저로 표현하면 아래와 같이 표현
someFunctionClosure() {
    // trailing closure's body goes here
}
```

</aside>

```swift
// 정렬 예제를 후위 클로저를 이용해 표현
reversedNames = names.sorted() { $0 > $1 }
```

만약 함수의 마지막 인자가 클로저이고 후위 클로저를 사용하면 괄호 생략

```swift
reversedNames = names.sorted { $0 > $1 }
```

<br>

# Capturing Value
<br>
<aside>

📸 **값 캡쳐**

---

**원본 값이 사라져도 클로져의 body안에서 그 값을 활용**

- Swift에서 값을 캡쳐 하는 가장 단순한 형태는 중첩 함수입니다

```swift
// makeIncrementer함수 안에서 incrementer함수를 호출하는 형태인 중첩 함수
func makeIncrementer(forIncrement amount: Int) -> () -> Int {

    var runningTotal = 0

    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }

    return incrementer
}
```

- 위 코드를 쪼개 보면 ->를 기준으로 뒤 () -> Int는 반환 값
- 반환 값이 클로저인 형태
- 📬 반환 값 :  인자가 없고 Int형의 반환하는 클로저를 반환
- incrementer함수만 따로 봐도 보면
    
    ```swift
    func incrementer() -> Int {
            runningTotal += amount
            return runningTotal
        }
    ```
    
    - runningTotal과 amount가 없지만 캡쳐링 됐기 때문에 함수는 돌아갑니다
</aside>

> *~~최적화 이유로 Swift는 만약 더 이상 클로저에 의해 값이 사용되지 않으면 그 값을 복사해 저장하거나 캡쳐링 하지 않습니다. Swift는 또 특정 변수가 더 이상 필요하지 않을 때 제거하는 것과 관련한 모든 메모리 관리를 알아서 처리합니다.~~*
>