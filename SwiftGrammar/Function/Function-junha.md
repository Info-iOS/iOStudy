# 함수
---
Swift의 함수는 기본적으로 1.함수이름, 2.매개변수, 반환타입을 사용하여 함수를 정의합니다

//매개변수란 = **함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 있게 해주는 변수입니다.**

//반환타입이란 = 원하는 타입을 받는 것

```swift
func 함수이름(매개변수...) -> 반환 타입 {
    실행 구문
  return 반환 값
}
```

swift에서 원하는 타입을 받기 위해서는 →를 사용합니다

```swift
func printName() {
    print("my name")
}

printName()
```

함수에는 매개변수와 반환타입이 없어도 사용가능 합니다

```swift
func printName(age: Int, Name: String) {
    print("my age is \(age) and my name is \(Name)")
}

printName(age: 17, Name: "박준하")
```

기본적인 함수의 구조이며 함수를 사용시 정했던 타입형식에 맞게 작성해야 오류를 피할 수 있다

```swift
func printName(나이 age: Int, 이름 Name: String) {
    print("my age is \(age) and my name is \(Name)")
}

printName(나이: 17, 이름: "박준하")
```

위처럼 전달인자가 있는 경우에는 다른 누군가가 코드를 볼떄 가독성이 높아질 것 입니다

//전달인자란 = 매개변수 앞에 붙는 것 (위코드의 전달인자는 ‘나이’와 ‘이름’이 전달인자다

```swift
func printName(나이 age: Int = 17, 이름 Name: String) {
    print("my age is \(age) and my name is \(Name)")
}

//나이는 defaultValue
printName(이름: "박준하")

//나이 변경이 가능함 어디까지나 default임
printName(나이: 18, 이름: "박준하")
```

함수에도 `defaultValue`를 정해서 아무 것도 입력하지 않았을 경우를 대비할 수 있다 하지만 `defaultValue`를 적었다고 해서 변경이 불가한 것은 아니다 물론 `defaultValue`를 사용하면 swfit에서 함수값에 default값을 안주지만 우리가 손수 다시 쓰면 값을 다시 바꿀 수 있다

```swift

func printName(age: Int, Name: String) -> String {
    let userName = "나이는 \(age) 이름은 \(Name)"
  return userName
}

let junhaName = printName(age: 17, Name: "박준하")

//junhaName  //"나이는 17 이름은 박준하"
```

 함수를 변수 안에 담아서도 출력할 수 있다 하지만 함수를 담을려면 꼭 return 값이 있어야한다

```swift
// In-out paramter
var age = 4

func printAge(_ age: inout Int) {
    age += 1
    print(age)
}

printAge(&4)

//출력 5
```

기존 우리는 함수 내부의 파라미터를 바꿀 수 없었다, 만약 우리가 실수를 해서라도 변경할 수 없다는 뜻이다
하지만 파라미터의 값을 변경하고 싶거나 변경된 값이 종료후에도 계속 지속되기를 바란다면 `inout`파라미터를 사용하면 된다)

in-out 파라미터는 함수 정의시 파라미터의 타입 전에 `inout`
 키워드를 추가하면 된다. in-out 파라미터는 변수(variable)만을 취급하며 함수의 인자로 전달할 때 `&`
를 사용하여 해당 값이 함수내부에서 변경될 것임을 나타내야 한다.

inout의 원리는 

1. 함수가 호출되면, 매개변수로 넘겨진 변수가 복사된다.
2. 함수 몸체에서, 복사한 값을 수정한다.
3. 함수가 반환될 때, 변화된 값을 원본 변수에 재할당한다.

```swift
//Function as a paramter
func add(a: Int, b: Int) {
    return a + b
}

func subtract(a: Int, b: Int) {
    return a - b
}
var function = add
function(5, 2) // 7
function = subtract
function(5, 2) // 3

//함수 타입이 같아야함
func printResult(_ function: (Int, Int) -> _ a: Int, _ b: Int) {
    let result = function(a,b)
    print(result)
}

printResult(add, 10, 5) // 15
printResult(subtract, 10, 5) // 5
```

위 같은 경우 함수를 변수나 데이터 구조로 담는 것을 “일급 객체"라고 하는데 5가지를 충족해야지 1급객체가 될 수 있다

- 변수나 데이터 구조 안에 담을 수 있습니다.
- 리턴 값으로 사용할 수 있습니다.
- 전달 인자 (Argument)로 전달이 가능합니다.
- 동적 프로퍼티 할당이 가능합니다.
- 할당할 때 사용된 이름과 관계없이 고유한 객체로 구별 가능합니다.
