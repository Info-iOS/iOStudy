# Property

## 프로퍼티

프로퍼티는 클래스, 구조체 또는 열거형 등에 관련되 값을 뜻한다. 메서드는 특정 타입에 관련되 함수를 뜻한다. 우리가 앞서 봤던 변수나 상수, 함수 등이 어떤 목적으로 쓰이느냐, 어디에서 어떻게 쓰이느냐에 따라 용어가 조금씩 달라질 뿐이다.

프로퍼티는 크게 저장 프로퍼티와 연산 프로퍼티, 타입 프로퍼티로 나눌 수 있다. 

저장 프로퍼티는 인스턴스의 변수 또는 상수를 의미한다.

연산 프로퍼티는 값을 저장한 것이 아니라 특정 연산을 실행한 결과값을 의미한다.

저장 프로퍼티는 구조체와 클래스에서만 사용할 수 있다.

타입 프로퍼티는 특정 타입에 사용되는 프로퍼티이다.

프로퍼티의 값이 변하는 것을 감시하는 프로퍼티 감시자도 있다.

## 저장 프로퍼티

클래스 또는 구조체의 인스턴스와 연관된 값을 저장하는 가장 단순한 개념의 프로퍼티이다.

var 키워드를 사용하면 변수 저장 프로퍼티, let 키워드를 사용하면 상수 저장 프로퍼티가 된다.

let 키워들 사용하면 상수 저장 프로퍼티가 된다.

```swift
struct CoordinatePoint {
  var x: Int
  var y: Int
}

let yagomPoint: CoordinatePoint = CoordinatePoint(x: 10, y: 5)
class Poisition {
  var point: CoordinatePoint
  let name: String

  init(name: String, currentPoint: CoordinatePoint) {
    self.name = name 
    self.point = currentPoint
  }
}
let yagomPosition: Position = Poisition(name: "yagom" , currentPoint: yagomPoint)
```

```swift
struct CoordinatePoint {
  var x: Int = 0
  var y: Int = 0
}

let yagomPoint: CoordinatePoint = CoordinatePoint()

let wizplanPoint: CoordinatePoint = CoordinatePoint(x : 10, y: 5)

print("yagom's point : \(yagomPoint.x), \(yagomPoint.y)")

print("wizplanPoint: : \(wizplanPoint.x), \(wizplanPoint.y)")

class Poisition {
  var point: CoordinatePoint = CoordinatePoint()
  var name: String = "Unknown"
}

let yagomPosition: Position = Position()

yagomPosition: Poisition = Poisition()

yagomPosition.point = yagomPoint
yagomPosition.name = "yagom"
```

옵셔널 저장 프로퍼티

```swift
struct CoordinatePoint {
  var x: Int 
  var y: Int 
}

class Poisition {
  var point: CoordinatePoint?
  let name: String

  init(name: String)
  {
    self.name = name
  }
}

let yagomPosition: Poisition = Poisition(name: "yagom")

yagomPosition.point = CoordinatePoint(x: 20, y:10)
```

## 지연 저장 프로퍼티

인스턴스를 생성할 때 프로퍼티에 값이 필요 없다면 프로퍼티를 옵셔널로 선언해줄 수 있다.

다른 용도로 필요할 때 값이 할당되는 지연 저장 프로퍼티가 있다. 지연 저장 프로퍼티는 호출이 있어야 값을 초기화하며, lazy라는 키워드를 사용한다.

## 연산 프로퍼티

연산 프로퍼티는 실제 값을 저장하는 프로퍼티가 아니라, 특정 상태에 따른 값을 연산하는 프로퍼티 이다. 인스턴스 외부에서 메서드를 통해 인스턴스 내부값에 접근하려면 메서드를 두 개 구현해야한다. 따라서 가독성을 올리기 위해 연산 프로퍼티를 사용한다.

## 프로퍼티 감시자

프로퍼티 감시자를 사용하며 프로퍼티의 값이 변경됨에 따라 적절한 작업을 취할 수 있다. 프로퍼티 감시자는 프로퍼티의 값이 새로 할당될 때마다 호출한다. 변경되는 값이 현재의 값과 같아도 호출한다.

상속받지 않은 연산 프로퍼티에는 프로퍼티 감시자를 사용할 필요가 없으며 할 수도 없다.

## 전역변수와 지역변수

전역변수는 함수나 메서드, 클로저, 클랙스, 구조체, 열거형 등의 범위 안에 포함되지 않았던 변수나 상수 즉 프로퍼티를 다루기 전에 사용했던 변수이다.

지역변수는 저장변수라고 할 수 있다. 저장변수는 저장 프로퍼티처럼 값을 저장하는 역할을 한다.

## 타입 프로퍼티

각각의 인스턴스가 아닌 타입 자체에 속하는 프로퍼티를 타입 프로퍼티라고 한다.
