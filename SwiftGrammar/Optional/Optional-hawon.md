# 옵셔널

## 옵셔널(Optional)이란?

optional은 ‘선택적인’이라는 뜻 그대로, 값이 있을 수도, 없을 수도 있음을 나타내는 표현

➡️ 변수 또는 상수의 값이 nil일 수도 있다.

## 옵셔널(Optional) 사용

nil은 옵셔널이 선언된 곳에서만 사용 가능

변수 또는 상수 등은 데이터 타입 뒤에 물음표(?)를 붙여 표현

```swift
var myName: String? = "Hawon"
print(myName) // Optional("Hawon")

myName = nil
print(myName) // Optional("nil")
```

‼️ 옵셔널 타입의 값을 print 함수의 매개변수로 전달 ❌ ‼️

## 옵셔널(Optional) 추출

옵셔널의 값을 옵셔널이 아닌 값으로 추출한다

➡️ 옵셔널 타입의 변수나 상수에서 실제 값을 가져오는 작업

### 옵셔널 바인딩(Optional Binding)

옵셔널의 값의 존재하는지 검사하고, 존재한다면 그 값을 다른 변수나 상수에 대입시켜줌

if let,  guard let 사용 (복잡도 if let > guard let)

if let은 값의 유무에 따라 각 코드를 실행하고, guard let은 값이 없으면 함수를 실행하지 못하도록 방어함.

**if let을 사용할 경우**

```swift
var myName: String? = "Hawon"

if let name = myName { // myName이 값을 가지고 있다면, name이라는 새로운 변수에 이 값을 할당함
	print("My name is \(name)")
} else {
	print("myName == nil")
}
```

지역 변수만 사용 ⭕️ ➡️ 구문 밖에서 접근 ❌

**guard let을 사용할 경우 (함수에서만 사용 가능)**

```swift
func printName() {
	var name: String?
	name = "Hawon"
	print(name) //Optional("Hawon")
	
	guard let myName = name else { return	}
	print(name) // "Hawon"
}
```

항상 else문이 뒤에 따라와야 함 

‼️ else 내부 코드에는 return, break, continue, throw 등의 “제어문 전환 명령어”를 사용

옵셔널 바인딩을 통해 한 번에 여러 옵셔널의 값을 추출 ⭕️

‼️ 바인딩하려는 옵셔널 중 하나라도 값이 없다면 해당 블록 내부의 명령문 실행 ❌

### 옵셔널 체이닝(Optional Chaining)

Chaining - 연쇄라는 뜻 그대로 연쇄적으로 옵셔널(?)를 사용한다는 의미

옵셔널에 속해 있는 nil일지도 모르는 프로퍼티, 메서드, 서브스크립션 등을 가져오거나 호출할 때 사용할 수 있는 일련의 과정

➡️ 값이 있다면 프로퍼티, 메서드, 서브스크립트 등을 호출 가능

➡️ 값이 없다면 프로퍼티, 메서드, 서브스크립트 등은 nil을 반환

‼️ 중첩된 옵셔널 중 하나라도 값이 존재하지 않는다면 결과적으로 nil을 반환

옵셔널 변수나 상수 뒤에 물음표(?)를 붙여 표현

‼️ nil이 반환될 가능성이 있음 ➡️ 옵셔널 체이닝 값은 항상 옵셔널

### 강제 추출

느낌표(!)를 붙여주면 값을 강제로 추출라여 반환해줌

‼️ 만약 강제 추출 시 옵셔널에 값이 없다면(nil 이라면), 런타임 오류 발생

강제 추출은 런타임 오류가 일어날 가능성이 가장 높고, 옵셔널을 만든 의미가 무색해짐

➡️ 강제 추출을 사용하는 것을 지양하자 ^^

## 옵셔널(Optional) 뜯어보기

옵셔널은 값이 갖는 케이스와 그렇지 못한 케이스 두 가지로 정의되어 있음

nil일 때는 none 케이스, 값이 있을 때는 some의 연관 값인 Wrapped에 값이 할당됨.

즉, 값이 옵셔널이라는 열거형의 방패막에 보호되어 래핑되어 있는 모습

➡️ 옵셔널 자체가 열거형이기 때문에 옵셔널 변수는 switch 구문을 통해 값이 있고 없음을 확인함.