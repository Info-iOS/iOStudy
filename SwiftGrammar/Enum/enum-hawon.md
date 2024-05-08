# 열거형

### 열거형(enum)이란?

연관된 항목들을 묶어서 표현할 수 있는 타입

### 사용하는 경우

1. 제한된 선택지를 주고 싶을 때
2. 정해진 값 외에는 입력받고 싶지 않을 때
3. 예상된 입력 값이 한정되어 있을 때

‼️ 열거형은 하나의 타입 ‼️

➡️ 대문자 카멜 케이스로 이름 설정

➡️ case는 소문자 카멜 케이스로 이름 설정

➡️ case는 그 자체가 고유의 값

```swift
enum Weekday {
	case mon // 한 줄씩 쓰기
	case tue
	case wed
	case thu, fri, sat, sun // 한 번에 쓰기
}
```

```swift
var day: Weekday = Weekday.mon // 열거형 타입과 케이스를 모두 사용 가능
day = .tue // 타입이 명확할 경우
```

### 열거형의 switch문 사용

```swift
switch day {
case .mon, .tue, .wed, .thu:
	print("평일")
case Weekday.fri:
	print("불금")
case .sat, .sun:
	print("주말")
}
```

모든 열거형 case를 포함한다면 default를 작성할 필요❌

### 정수 값을 값을 가지고 싶다면?

➡️ rawValue를 사용

‼️ case별로 각각 다른 값을 가져야함 ‼️

```swift
enum Fruit: Int {
	case apple = 0
	case grape = 1
	case peach
}

print("Fruit.peach.rawValue == \(Fruit.peach.rawValue)")
// Fruit.peach.rawValue == 2
```

정수 타입 뿐만 아니라 모든 타입이 원시값의 타입으로 지정될 수 ⭕️

(원시 값 타입이 String일 때, 원시 값이 지정되지 않았다면 case의 이름을 원시 값으로 사용)

### 원시 값을 통한 초기화

rawValue를 통해 초기화할 수 있음

rawValue가 case에 해당하지 않을 수 있으므로 rawValue를 통해 초기화한 인스턴스는 옵셔널 타입

```swift
let apple: Fruit? = Fruit(rawValue: 0) // rawValue로 초기화 함(Fruit 타입 아님)
```

```swift
if let orange: Fruit = Fruit(rawValue: 5) {
	print("rawValue 5에 해당하는 케이스는 \(orange)입니다.")
} else {
	print("rawValue 5에 해당하는 케이스가 없습니다")
}
// rawValue 5에 해당하는 케이스가 없습니다.
```

if let 구문을 사용하면 rawValue에 해당하는 케이스를 곧바로 사용 ⭕️

### 메서드

메서드 추가 가능

```swift
enum Month {
    case dec, jan, feb
    case mar, apr, may
    case jun, jul, aug
    case sep, oct, nov
    
    func printMessage() {
        switch self {
        case .mar, .apr, .may:
            print("따스한 봄~")
        case .jun, .jul, .aug:
            print("여름 더워요~")
        case .sep, .oct, .nov:
            print("가을은 독서의 계절!")
        case .dec, .jan, .feb:
            print("추운 겨울입니다")
        }
    }
}

Month.mar.printMessage()
// 따스한 봄~
```