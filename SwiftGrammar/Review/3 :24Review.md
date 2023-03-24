# 3/24 요약

## 프로퍼티

프로퍼티는 클래스, 구조체 또는 열거형 등에 관련되 값을 뜻한다. 메서드는 특정 타입에 관련되 함수를 뜻한다. 우리가 앞서 봤던 변수나 상수, 함수 등이 어떤 목적으로 쓰이느냐, 어디에서 어떻게 쓰이느냐에 따라 용어가 조금씩 달라질 뿐이다.

## 저장 프로퍼티

클래스 또는 구조체의 인스턴스와 연관된 값을 저장하는 가장 단순한 개념의 프로퍼티 이다.

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

---

## 객체지향 프로그래밍 패러다임

객체지향 프로그래밍 패러다임은 컴퓨터 프로그래밍 패러다임의 한 종류로 객체지향 프로그래밍이라고도 불린다. 객체지향 프로그래밍은 컴푸터 프로그램을 명령어의 목록으로 보는 기존의 명령형 프로그래밍 패러다임의 시각에서 벗어나 여러 갱듸 독립된 단위인 객체의 모임으로 파악하고자 하는 시각이다. 

객체만 잘 이해하면 프로그래밍을 더 쉽게 배우고, 개봘과 유지보수가 산편하고, 직관적으로 코드를 분석할 수 있다.

### 캡슐화

캡슐화란 관련된 데이터와 알고리즘이 하나의 묶음으로 정리된 것이다. 

### 상속

상속은 이미 작성된 클래스를 이어 받아서 새로운 클래스를 생성하는 기법이다. (기존 코드를 재활용 한 것)

### 다형성

다형성이란 하나의 이름으로 많은 상황에 대처하는 기법이다.

### 객체지향의 장점

코드의 재활용성이 높음

코딩이 절차지향보다 간편함

디버깅이 쉽다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

절차지향과 객체 지향의 차이는 그림과 같이 객체 지향은 절차지향처럼 순서대로 진행되는 것이 아니라 순서의 제약을 받지않고 더 쉽고 간편하게 프로그래밍 하는것이 객체 지향이다.

## 옵셔널

옵셔널은 스위프트의 특징 중 하나인 안전성(Safe)을 문법으로 담보하는 기능이다. 옵셔널은 단어 뜻  그대로 ‘선택적인’, ‘있을 수도, 없을 수도 있음’을 나타내는 표현이다.

nil 옵셔널 변수 또는 상수가 아니면 nil을 할당할 수 없기 때문이다.

```swift
var myNAme: String = "yagom"
myName = nil
```

## 옵셔널 추출

열거형의 some 케이스로 꼭꼭 숨어있는 옵셔널의 값을 옵셔널이 아닌 값으로 추출하는 것이 옵셔널 추출이다.

## 강제 추출

옵셔널 강제 추출 방식은 옵셔널의 값을 추출하는 가장 간단하지만 가장위험한 방법이다. 런타임 오류가 일어날 가능성이 가장 높기 때문이다.

옵셔널을 만든 의미가 사라지기도 함. 옵셔널의 값을 강제 추출하려면 옵셔널의 값의 뒤에 느낌표(!)를 붙여주면 값을 강제로 추출하여 반환해준다. 옵셔널에 nil이라면 런타임 오류가 발생함.

```swift
var myNAme: String? = "yagom"
var yagom: String = myName!
myName = nil
yagom = myName!

if myName != nil {
print("my name is \(myName!)")
}else {
print("myName == nil")
}

```

## 옵셔널 바인딩

옵셔널 바인딩은 옵셔널에 값이 있는지 확인할 때 사용한다. 만약 옵셔널에 값이 있다면 옵셔널에서 추출한 값을 일정 블록 안에서 사용할 수 있는 상수나 변수로 할당해서 옵셔널이 아닌 형태로 사용할 수 있도록 해준다. 

```swift
var myNAme: String? = "yagom"
if let name = myName {
print("MY name is \(name)")
}else {
print("myName == nil")
}
if var name = myName {
name = "wizplan"
print("My name is \(name!)")
}else {
print("myName == nil")
}

```

## 암시적 추출 옵셔널

nil을 할당하고 싶지만, 옵셔널 바인딩으로 하기 귀찮다면 사용하는 것이 암시적 추출 옵셔널이다. 암시적 추출 옵셔널을 상용하려면 타입 뒤에 느낌표(!)를 사용해주면 된다. 암시적 추출 옵셔널로 지정된 타입은 일반 값처럼 사용할 수 있으나, 여전히 옵셔널이기 때문에 nil도 할당해줄 수 있다. 

```swift
var myNAme: String! = "yagom"
print(myName)
myname = nil
if let name = myName {
print("my name is \(name!)")
}else {
print("myName == nil")
}

```

## view의 생명주기

앱들은 ‘View Controller’로 이루어져 있는데, 하나 이상의 화면이 있다면 이 각각의View Controller들은 생명주기를 가지고 있다. View Controller의 생명주기는 보여졌다 사라지는 주기이다.

  

## Will과  Did

Will은 미래를 나타내고 Did는 과거를 나타낸다.

1. viewDidLoad
2. viewWillAppear
3. viewDidAppear
4. viesWillDisappear
5. viewDidDisappear

### 1. viewDidLoad

Did : 과거

뜻 : “뷰가 로드 되었다”라는 뜻이다.

viewDidLoad 메소드는 뷰의 로딩이 완료 되었을 때 시스템에 의해 자동으로 호출되기 때문에 리소스를 초기화하거나 초기 화면을 구성하는 용도로 주로 사용한다. 화면이 처음 만들어질 때 한 번만 실행되므로, 처음 한 번만 실행해야 하는 초기화 코드가 있을 경우 이 메소드 내부에 작성하면 된다.(View Controller생에 딱 한번만 호출이 된다.)

### 2.viewWillAppear

Wiill : 미래

뜻 : “뷰가 나타날 것이다”라는 뜻 이다.

타이밍 : 뷰 컨트롤러의 화면이 올라오고 난후 뷰가 나타나기 직전에 호출이 된다.

view가 이제 나타날 거라는 신호를 컨트롤러에게 알리는 역할을 한다. 즉 뷰가 나타나기 직전에 호출이 된다.  

viewWillAppear와 viewDidLoad의 차이 다른 뷰에서 갔다가 다시 돌아오는 상황에도 띄우고 싶다면 viewWillAppear를 사용해야 한다.

### 3.viewDidAppear

Did : 과거

뜻 : “뷰가 나타났다”라는 뜻이다.

타이밍 : view가 데이터와 함께 완전히 화면에 나타난 후 호출되는 메소드

viewDidAppear는 뷰가 나타났다는 것을 컨트롤러에게 알리는 역할을 한다. 또한 화면에 적용될 애니메이션을 그려준다. viewDidAppear는 뷰가 화면에 나타난 직후에 실행된다.

### 4. viewWillDisappear

Will : 미래

뜻 : “뷰가 사라질 것이다”라는 뜻이다.

타이밍 : 다음 View Controller 화면이 전환하기 전이나 View Controller가 사라지기 직전에 호출된다.

viewWillDisappear는 뷰가 삭제 되려고하고있는 것을 뷰 컨트롤러에 통지한다.

### 5. viewDidDisappear

Did : 미래

뜻 : “뷰가 사라졌다.”라는 뜻이다.

타이밍 : View Controller들이 화면에서 사라지고 나서 호출됨

viewDidDisappear가 호출 되면, 뷰 컨트롤러가 뷰가 제거되었음을 알려준다.

## 클로저

스위프트에서 함수형 프로그래밍 패러다임을 접할 때 첫걸음으로 꼭 알아야 할 녀석이 바로 클로저이다.  잘 이해한다면 스위프트의 함수형 프로그래밍 패러다임 스타일을 좀 더 명확하게 이해할 수 있다. 

클로저는 일정 기능을 하는 코드를 하나의 블록으로 모아놓은 것을 말한다. 함수를 비슷 한걸 느낄 수 있다. 함수는 클로저의 한 형태이기 때문이다.

## 클로저의 표현

 매개변수와 반환 값의 타입을 생략할 수 있다.

단 한 줄의 표현만 들어있다면 암시적으로 이를 반환 값으로 취급한다.

축약된 전달인자 이름을 사용할 수 있다.

후행 클로저 문법을 사용할 수 있다.

## 기본 클로저

기본 클로저 내용을 포함하여 sorted(by : ) 메서드를 이용해 동일한 기능을 간결하게 표현할 수 있다.

```swift
public func sorted(by areInIncreaseingOrder: (Element, Element) -> Bool) -> [Element]
```

String 타입의 배열 생성하기

```swift
let names: [String] = ["wizplan", "eric", "yagom", "jenny"]
```

## 후행 클로저

클로저를 읽기 쉽게 바꿔볼 수 있다. 클로저가 조금 길어지거나 가독성이 조금 떨어진다 싶으면 후행클로저 기능을 사용하면 좋다. 또한 단 하나의 클로저만 전달인자로 전달하는 경우에는 소괄호를 생략 해줄 수도 있다. 다중 후행 클로저도 사용가능하다.

```swift
let resrved: [String] = names.sorted() { (first: String, second: String) -> Bool in 
return first > second
}
let reserved: [String] = names.sorted { (first: String, second: String) -> Bool in
return first > second
}

func doSomething(do: (Sting) -> Void,
								onSucces: (Any) -> Void,

								onFailure: (Error) -> Void) {
		//do something...
}
```

## 클로저 표현 간소화

메서드의 전달인자로 전달하는 클로저는 메서드에서 요구하는 형태로 전달해야한다. 즉 타입을 같게 맞추어 전달해야 한다는 것. 하지만 클로저는 이미 적합한 타입을사용하여 유추할 수 있다. 그렇기 때문에 구현할 때 매개변수의 타입이나 반환 값의 타입을 굳이 표현해주지 않고 생략해도 문제가 없다뜻이다.

```swift
let reserved: [String] = names.sorted { (first, second) in
		return first > second
}
```

### 단축 인자 이름

```swift
let reserved:[String] = names.sorted {
return $0 > $1
}
```

### 암시적 반환 표현

```swift
let reserved: [String] = names.sorted { $0 > $1 }
```

## 클로저는 참조 타입

두 상수를 정의 했다고 치고 두 상수는 같은 클로저를 참조하기 때문에 동일한 클로저가 동작하는 것을 볼 수 있다.

```swift
let increment ByTwo: (() -> Int ) = makeIncrementer(forIncrement: 2)
let sameWithIncrementByTwo: (() -> Int) = incrementByTwo

let first: Int = incrementByTwo()
let second: Int = smallWithIncrementByTwo()
```

## 자동 클로저

함수의 전달인자로 전달하는 표현을 자동으로 변환해주는 클로저를 자동 클로저라고 한다. 자동 클로저는 전달인자를 갖지 않는다. 자동 클로저는 호출되었을 때 자신이 감싸고 있는 코드의 결괏값을 반환한다.

자동클로저의 사용

```swift
var customersInLine: [String] ["Eunho", "Tyler", "Eunhoo", "Tylerr"]

func serveCustomer(_ customerProvider: @autoclosure () -> String) {
  printf("Now serving \(customerProvider))!")

}

serveCustomer(customersInLine.removeFirst())
```