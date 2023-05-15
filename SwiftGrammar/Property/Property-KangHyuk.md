# Swift Property

![Properties](image/SwiftProperise.png)

<aside>

🌮 **property**

---

**프로퍼티는 클래스, 구조체, 열거형과 관련한 값**

- 🍤 Stored Properties : 저장 프로퍼티는 말 그대로 값을 저장하고 있는 프로퍼티
    - 클래스와 구조체에서만 사용 **O**
- 💻 Computed Properties : 계산된 프로퍼티는 값을 저장하지 않고 특정하게 계산한 값을 반환
    - 클래스, 구조체, 열거형 모두에서 사용 **O**
- 추가로 프로퍼티 옵저버를 정의해서 값이 변할 때마다 모니터링 **O**
</aside>

<br>
<br>

# Stored Properties

<aside>

💡 **저장 프로퍼티**

`let`키워드를 이용해서 상수 혹은 `var`키워드를 이용해서 변수로 선언

```swift
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// 범위 값은 0, 1, 2 입니다.
rangeOfThreeItems.firstValue = 6
// 범위 값은 6, 7, 8 입니다.
```

> **상수 구조체 인스턴스의 저장 프로퍼티 🎯**
> 
> 
> ---
> 
> **구조체를 상수로 선언하면(`let`) 그 구조체 인스턴스의 프로퍼티는 변경 X**
> 
> ```swift
> let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
> // 범위 값은 0, 1, 2, 3 입니다.
> rangeOfFourItems.firstValue = 6
> // 에러 발생!
> ```
> 
</aside>


<br>

<aside>

🦥 **Lazy Stored Properties**

---

**값이 처음으로 사용 되기 전에는 계산되지 않는 프로퍼티**

- 프로퍼티의 선언 앞에 `lazy`키워드
- 반드시 변수(`var`)로 선언해야 함
    - → 상수는 초기화가 되기전에 항상 값을 같는 프로퍼티
- *~~지연 프로퍼티가 여러 스레드에서 사용될 때 지연 프로퍼티가 한번만 실행되는 걸 보장하지 않음~~*

```swift
class DataImporter {
    /*
        DataImporter는 외부 파일에서 데이터를 가져오는 클래스입니다.
         이 클래스는 초기화 하는데 매우 많은 시간이 소요된다고 가정하겠습니다.
     */
    var filename = "data.txt"
    // 데이터를 가져오는 기능의 구현이 이 부분에 구현돼 있다고 가정
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // 데이터를 관리하는 기능이 이 부분에 구현돼 있다고 가정
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// DataImporter 인스턴스는 이 시점에 생성돼 있지 않습니다.
```

```swift
print(manager.importer.filename)
// the DataImporter 인스턴스가 생성되었습니다.
// "data.txt" 파일을 출력합니다.
```

> `manager.importer.filename`가 실행돼 실제 프로퍼티에 처음 접근할 때 인스턴스 생성
> 
</aside>

<br><br>

# Computed Properties
<aside>

🧮 **계산된 프로퍼티**

---

**클래스, 구조체, 열거형만 선언할 수 있고 getter와 optional한 setter를 제공하는 프로퍼티**

```swift
struct Point {
    var x = 0.0, y = 0.0
}

struct Size {
    var width = 0.0, height = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}

var square = Rect(origin: Point(x: 0.0, y: 0.0), size: Size(width: 10.0, height: 10.0))
//Rect 구조체는 사각형의 중점을 표현하는 center라는 계산된 프로퍼티를 제공

let initialSquareCenter = square.center

square.center = Point(x: 15.0, y: 15.0)

print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// "square.origin is now at (10.0, 10.0)" 출력
```

</aside>

<br>

### Shorthand Setter Declaration 🥫

---

<aside>

🏵️ **Setter 선언의 간략한 표현**

**(newCenter)라고 인자 이름을 지정하지 않으면 인자 기본 이름인 newValue를 사용**

```swift
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
    }
}
```

</aside>
<br><br>

# Read-Only Computed Properties 
<aside>

🥙 **읽기전용 계산된 프로퍼티**

---

**getter만 있고 setter를 제공하지 않는 계산된 프로퍼티를 읽기전용 계산된 프로퍼티**

```swift
//volume이라는 읽기전용 계산된 프로퍼티를 사용한(예)
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
print("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// "the volume of fourByFiveByTwo is 40.0" 출력
```

</aside>

> 읽기전용 계산된 프로퍼티를 포함해 계산된 프로퍼티를 선언시에는 반드시 let이 아니라 var로 선언
계산된 프로퍼티는 읽기전용이라 하더라도 계산 값에 따라 값이 변할 수 있기 때문에 var로 선언
>

<br><br>

# Property Observers

<aside>

 **프로퍼티 옵저버**

---

**프로퍼티에 새 값이 set 될 때마다 이 이벤트를 감지할 수 있는 옵저버**

- 새 값이 이전 값과 같더라도 항상 호출
- 지연 저장 프로퍼티에서 사용 **X**
- 계산된 프로퍼티는 setter가 있기 때문에 따로 옵저버를 정의할 필요 **X**
- 🐠 willSet : 값이 저장되기 바로 직전에 호출 되는 프로퍼티
- 🍣 didSet : 값이 저장되고 직후에 호출 되는 프로퍼티

> 서브클래스에는 initializer가 호출 된 후 프로퍼티 옵저버 실행
> 
</aside>

```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

<br><br>

# Type Properties

<aside>

💡 **타입 프로퍼티**

---

**특정 타입에 속한 고정된 속성 값을 정의할 수 있는 프로퍼티**

- 특정 인스턴스와 연관 **X**
- 특정 타입에 대해 하나의 값만 존재
- 속성 값은 타입의 모든 인스턴스에서 동일
- 타입의 고정된 속성 값을 정의하고 사용할 때 유용
</aside>

<br>

### 정의 ⚖️

---

```swift
class ClassName {
    static var propertyName: PropertyType = DefaultValue
}
```

> 위의 코드에서 static 키워드는 Type Properties를 정의하고 있다는 것을 나타내며 class 키워드로 대체 **O**
> 

<br>

### Type Properties의 예시 🚀

---

```swift
struct Circle {
    static var pi = 3.14
    var radius: Double

    var circumference: Double {
        return 2 * Circle.pi * radius
    }
}

let circle1 = Circle(radius: 5)
let circle2 = Circle(radius: 10)

print(circle1.circumference) // 31.4
print(circle2.circumference) // 62.8
```

> 해석
> 
> 
> ---
> 
> 1. 위의 예시에서 pi는 Type Properties로 정의됨
> 2. radius는 인스턴스 속성으로 정의됨
> 3. pi는 모든 Circle 인스턴스에서 동일한 값을 가짐
> 4. 따라서 circumference 계산에서 pi는 같은 값이 반환

```swift
//pi를 클래스로 선언하여 Type Property를 만들면
//아래와 같이 만들 수 있다
struct Circle {

    class var pi: Double {
				return 3.14
		}

    var radius: Double

    var circumference: Double {
        return 2 * Circle.pi * radius
    }
}

let circle1 = Circle(radius: 5)
let circle2 = Circle(radius: 10)

print(circle1.circumference) // 31.4
print(circle2.circumference) // 62.8
```

<br>

### Constant와 차이점 ❄️

---

**Type Property**

1. 타입 자체에 저장되는 값
    - 프로그램 실행 중에 변경될 수 있음
        - → let **X**, var **O**

**Constant**

- 값이 아닌 상수
    - 변경 **X**