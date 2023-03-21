# Optional

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

옵셔널을 만든 의미가 사라지기도 함. 옵셔널의 값을 강제 추출하려면 옵셔널의 값의 뒤에 느낌펴(!)를 붙여주면 값을 강제로 추출하여 반환해준다. 옵셔널에 nil이라면 런타임 오류가 발생함.

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