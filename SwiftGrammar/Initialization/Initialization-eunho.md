# Initialization

초기화는 클래스, 구조체, 열거형 인스턴스를 사용하기 위해 준비 작업을 하는 단계 이다. 이 단계에서는 각 저장 프로퍼티의 초기값을 정해준다.

## 이니셜라이저 (initializers)

init 키워드를 사용한다

```swift
init() {
//something
}
```

이러한 형식으로 init을 사용함

```swift
struct Fahrenheit {
    var temperature = 32.0
}
```

프로퍼티 선언과 동시에 같이 선언을 해준 코드이다. 

## 커스터마이징 초기화

초기화 프로세스를 입력 값과 옵셔널 프로퍼티 타입 혹은 상수 값을 할당해서 커스터마이징 할 수 있다.

## 옵셔널 프로퍼티 타입

프로퍼티의 최초 값이 없고 나중에 추가될 수 있는 값을 옵셔널로 선언해 사용할 있다. 옵셔널 프로퍼티는 자동으로 nil로 초기화임.

## 소멸자

init의 반대인 deinit을 사용한다.

## 초기화 파라미터 (파라미터 == 매개변수)

```swift
struct Celsius {
    var temperatureInCelsius: Double
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
```