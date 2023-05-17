# 동기/비동기/동시/직렬

---

## **동기(Sync)?**

- 동시에 일어난다.
- 순차적으로 처리
- 해당 작업이 끝날 때까지 기다린다.
- ex) 집에서 친구에게 전화를 걸고 쇼핑하러가기
    - (순서)
    - 1. 친구에세 전화를 걸고 대화를 한다
    - 2. 전화가 끝날 때까지 집에 있는다
    - 3. 대화가 끝나고 쇼핑하러간다
    - 4. 백화점에 가서 쇼핑을 한다.

동기 예제 코드)

```swift
func calculateSum(a: Int, b: Int) -> Int {
    return a + b
}

func printSum() {
    let result = calculateSum(a: 3, b: 5)
    print("The sum is: \(result)")
}

printSum()
```

### **실행 순서**

- calculateSum → printSum
    - calculateSum가 끝나기 전까지는 printSum는 할 수 없다.

---

## 비**동기(Async)?**

- 동시에 일어나지 않는다
- 작업이 끝날 때까지 안기다리고 작업을 실행한다
- ex) 집에서 친구에게 메시지를 보내고, 응답을 받은 후에 쇼핑을 하러 간다.
    - (순서)
    - 집에서 친구에게 메시지를 한다.
    - 메세지를 보낸 후 쇼핑하러간다.
    - 백화점에 왔을 때 친구가 메세지에 응답을 기다린다
    - 응답이 도착하면 쇼핑하러 간다

비동기 예제 코드)

```swift
func printDelayedMessage() {
    DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
        print("Delayed message after 3 seconds")
    }
}

printDelayedMessage()
```

### **실행 순서**

- 3초후 printDelayedMessage() 실행

- 비동기는 왜? 사용할까?
    - 네트워크 통신 시, 결과물이 언제 도착할지 모름
    - 예) 급식 앱
        - 칼로리를 가져로려면 오늘 급식이 필요함
        - 때문에 급식을 못가져오면 칼로리를 보지 못함
    - 예) 파일 다운
        - 큰 파일을 다운 받음
        - 멈추면 사용자가 멈췄다고 생각할 수 있음
    

---

# 직렬**(Serial)?**

- 다른 하나의 스레드로 작업을 넘기는 것
- 직렬은 2가지로 나누어집니다
    - 직렬화, 직렬큐

## 직렬화**(Serialization)?**

- 직렬화는 객체나 데이터 구조를 일련의 바이트로 변환하는 프로세스(위키)
- ex) 택배를 포장해서 전송할 때, 그 물건을 분해하지 않고 한 줄로 전송
- Swift에서 직렬화는 객체나 데이터 구조를 일련의 바이트
- 데이터를 저장해서 네트워크 통신을 할 수 있음

직렬화 예제 코드)

```swift
struct Person: Codable {
    var name: String
    var age: Int
}

let junha = Person(name: "junha", age: 18)

let encoder = JSONEncoder()
if let jsonData = try? encoder.encode(junha) {
}
```

**`JSONEncoder` 를** 사용해서 `Person` 객체를 `JSON`으로 직렬화 하는 코드이며 `jsonData`에 저장합니다. jsonData는 파일에 저장 또는 네트워크를 할 수 있는 상태가 됩니다

## 역직렬화(deserialization)

- 나중에 필요할 때는 직렬화된 데이터를 읽어와서 다시 객체로 복원하는 작업
- **`Codable`**이 직렬화된 코드를 역직렬화 할 수 있습니다

역직렬화 예제 코드)

```swift
let decoder = JSONDecoder()

if let decodedPerson = try? decoder.decode(Person.self, from: jsonData) {
    // jsonData에서 가져온 직렬화된 데이터를 Person 객체로 역직렬화
    print(decodedPerson.name) // 출력: "junha"
    print(decodedPerson.age)  // 출력: 18
}
```

**`JSONDecoder`**를 사용하여 **`jsonData`**에서 직렬화된 데이터를 읽어 옵니다.
 **`Person`** 객체로 역직렬화하고 있습니다. 역직렬화된 객체는 **`decodedPerson`**에 저장됩니다.

---

# 동시성(Concurrency)**?**

- 여러 작업을 동시에 실행하는 것
- 프로그램의 성능과 응답성을 향상시키는데 도움을 줌
- 여러 작업을 효율적으로 처리하는 방법을 제공
- 비동기 함수, 비동기적 호출, 구조적 동시성

## 비동기 함수(Async Functions)

- 비동기 함수는 작업이 완료될 때까지 기다리지 않고 다음 코드를 실행하는 함수.
- **`async`** 를 사용하여 함수를 선언
- `a**wait**` 를 사용하여 다른 비동기 작업의 완료를 기다리거나 결과 받기

```swift
func fetchData() async -> Data {
   
    let data = await 비동기작업()
    return data
}
```

## 비동기적 호출(Async Calls)

- 비동기적 호출은 **`await`**를 사용하여 다른 비동기 함수의 실행이 완료될 때까지 기다립니다.

```swift
let result = await fetchData()
print(result)
```

## 구조적 동시성(Structured Concurrency)

- 구조적 동시성은 동시성 작업을 조직화하고 제어하는 방법
- **`Task`**와 **`TaskGroup`** 구조체를 사용하여 비동기 작업의 **생성**, **그룹화**, **조작**, **취소** 등을 관리합니다.

```swift
let task = Task {
    // 비동기 작업
}

let taskGroup = TaskGroup {
    // 여러 비동기 작업을 그룹으로 묶음
}

await taskGroup.add {
    // 비동기 작업 추가
}
```

- 동시성? 언제 사용하는가?
    - 순서가 중요한 작업 처리 → 직렬처리
        - ex) 노래를 다운 받고 노래를 재생하는 경우
    - 독립적이지만 비슷한 여러개의 작업 처리 → 동시 처리
        - 인스타 그램 피드 가져오는 경우

---

## 비동기? 동시? 같은 말 아님?

> `아니요!` 엄연이 다른 말입니다
> 

### 비동기

- main thread에서 다른 스레드로 보낸 작업을 대기할지 진행할지에 대한 개념

### 동시

- main에서 분산 처리 시킨 작업
- 하늬의 스레드에서 처리할지, 여러 스레드에서 처리할지에 대한 개념

---

# 개인적으로 궁금했던 것

## 1. 동시성 많이 쓰면 좋을까?

- 데드락, 경합 조건, 다른 작업과의 상호작용 등 문제 발생 가능성이 높아짐

## 2. 비동기 많이 쓰면 좋을까?

- ~~1학년때 비동기 병에 걸림~~
- 장점
    - 응답성 향상
        - UI의 응답성을 유지하거나, 네트워크 요청 등의 시간이 오래 걸리는 작업을 수행할 때 사용자 경험을 향상
    - 병렬 처리
        - 작업을 분산하여 처리하므로 전체적인 성능 향상
    - 자원 효율성
        - 시스템 자원의 최적 활용
- 단점
    - 복잡성 증가
        - 흐름을 추적하기 어렵게 만듬
        - 유지보수가 힘들어짐
        - 디버깅이 어려워짐
        - 가독성이 너무 떨어짐
    - 동기화와 경쟁 조건
        - 잘못된 동기화는 버그를 유발
        - 잘못되면 화면이 영원히 멈추거나 지직거린다
        - ~~내가 사용했을 때는 이상한 버그로 화면이 없어지는 사태 발생~~
    - 성능 저하
        - 무지성으로 비동기를 쓰면 짧은 시간 수행 작업일 경우 오버헤드 발생

## 3. iOS에서 비동기를 사용하는 방법

- 라이브러리 제외(rxswift)
- **async**
- **await**
- GCD
- 클로저
- 델리게이트
- Notification center
- Operation

---

## **iOS에서 동시성 프로그래밍이 필요한 이유**

- 다수에 이미지를 렌더링할 때
- collectionView 무한 스크롤할 경우
- 사용자에게 자연스러움을 연출하기 위해서