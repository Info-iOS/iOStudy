# Function

## 함수

함수 대부분은 작업의 가장 작은 단위이자 하나의 작은 프로그램이기도 하다.

함수는 프로그램을 이루는 주된 요소중 하나이다.

스위프트에서 함수는 다른 언어보다 훨씬 다양한 모습으로 존재하고, 코딩스타일도 다양하다.

따라서 팀 프로젝트를 진행할 때에는 코딩 규칙을 만들어 함수를 사용하는게 좋다.

## 함수와 메서드

함수와 메서드는 기본적으론 같다.

단지 상황이나 위치에 따라 다른 용어로 부르는 것.

구조체, 클래스, 열거형 등 특정 타입에 연간되어 사용하는 함수를 **메서드**, 모듈 전체에서 전제에서 사용할 수 있는 함수를 그냥 **함수**라고 부른다. 즉, 함수가 위치하거나 사용되는 범위 등에 따라 호칭이 달라질 뿐, 함수라는 것 자체에는 변함이 없다.

## 함수의 정의와 호출

함수와 메서드는 정의하는 위치와 호출되는 범위만 다를 뿐, 정의하는 키워드와 구현하는  방법은 같다. 조건문이나 반복문 같은 스위프트의 다른 문법과 달리 함수에서는 소괄호(())를 생략할 수 없다. 

함수는 재정의와 중복 정의를 모두 지원한다. 따라서 매개변수의 타입이 다르면 같은 이름의 함수를 여러 개 만들 수 있고, 매개변수의 개수가 달라도 같은 이름의 함수를 만들 수 있다. 따라서 이름이 같은 함수를 구현해도 오류가 발생하지 않는다.

## **기본적인 함수의 정의와 호출**

스위프트의 함수는 자유도가 굉장히 높은 문법 중 하나이다. 함수를 사용할 때에는 이름과 매개변수, 반환 타입등을 사용하여 함수를 정의한다.

함수를 정의하는 키워드는 function을 줄여놓은 func이다. 함수 이름을 지정해준 후 매개변수는 소괄호(())로 감싸준다. 반환 타입을 명시하기 전에는 ->를 사용하여 어떤 타입이 반환될 것인지 명시해준다. 반환을 위한 키워드는 C언어처럼 return을 사용한다.

함수에서 return 키워드를 생략할 수도 있다.

매개변수는 함수를 정의할 때 외부로부터 받아들이는 전달 값의 이름을 의미한다. 

 

```swift
//함수의 기본 형태
func 함수이름(매개변수…) -> 반환 타입 {
실행 구문
return 반환 값
}
```

```swift
//함수 기본 형태 책 예제
hello(name: String) -> String {
  return "Hello \(name)!"
}
let helloJenny : String = hello(name : "Jenny")
print(helloJenny)
```

```swift
//함수의 기본 형태 직접 프로그래밍
func hi(name : String) -> String{
  return "Hi \(name)!"
}
let hiEunho: String = hi(name: "Eunho")
print(hiEunho)
```

```swift
//함수의 기본 형태 2 책 예제
func introduce(name : String) -> String {
  "제 이름은" + name + "입니다"
}
let introduceJenny: String = introduce(name:"Jenny")
print(introduceJenny)
```

```swift
//함수의 기본 형태 2 직접 프로그래밍
func introduce(name: String) -> String{
  return "내 이름은" + name + "입니다."
}
let introduceEunho: String = introduce(name: "Eunho") 
print(introduceEunho)
```

## 매개변수

스위프트의 함수는 매개변수를 어떻게 정의하냐에 따라서도 모습이 크게 달라질 수 있다.

## **매개변수가 없는 함수와 매개변수가 여러 개인 함수**

함수에 매개변수가 필요 없다면 매개변수 위치를 공란으로 비워둔다. 

다음은 매개변수가 없는 함수를 구현한 코드이다.

```swift
//매개변수가 없는 함수 책예제
func helloWorld() -> String {
  return "Hello World!"
}
print(helloWorld())
```

```swift
//매개변수가 없는 함수 직접 프로그래밍
func eunhoIsHandsome() -> String {
  return "eunho is Handsome"
}
print(eunhoIsHandsome())
```

```swift
//매개변수가 여러 개인 함수의 정의와 사용 책 예제
func sayHello(myName: String, yourName: String) -> String{
return "Hello \(yourName)! I'm \(mmyName)"
}
print(sayHello(myName:"yagom", yourName:"Jenny"))
```

매개변수가 여러 개  필요한 함수를 정의할 때는 쉼표( , )로 매개변수를 구분한다. 

주의할 점은 함수를 호출할 때, 매개변수 이름을 붙여주고 콜론( : )을 적어준 후 전달인자를 보내준다는 점.

## **매개변수 이름과 전달인자 레이블**

매개변수 이름과 전달인자 레이블을 지정할 때는 이처럼 표현한다.

```swift
func 함수 이름(전달인자 레이블 매개변수 이름: 매개변수 타입, 전달인자 레이블 매개변수 이름:
				매개변수 타입...) -> 반환 타입{
실행 구문
return 반환 값
}
```

```swift
func sayHello(from myName:String, to name:String) -> String {
return "Hello \(name)! I'm \(myName)"
}
print(sayHello(from: "yagom", to: "Jenny"))
```

## 매개변수 기본값

스위프트의 함수에서는 매개변수마다 기본값을 저장할 수 있습니다.

즉, 매개변수가 전달되지 않으면 기본값을 사용합니다. 

## **기본 매개변수와 입출력 매개변수**

매개변수로 몇 개의 값이 들어올지 모를 때, 가변 매개변수를 사용할 수 있다. 가변 매개변수는 0개 이상(0개 포함)의 값을 받아올 수 있으며, 가변 매개변수로 들어온 인자 값은 배열처럼 사용할 수 있다. 함수마다 가변 매개변수는 하나만 가질 수 있다.

```swift
func sayHelloFriends(me: String, friends names: String...) -> String {
var result: String = " "

for friend in names {
	result += "Hello \(friend)!" + " "
{
	result += "I'm + me + "!
	result result
}
print(sayHelloFriends)
print(sayHelloFriends)
```

## **중첩 함수**

스위프트는 데이터 타입의 중첩이 자유롭다.

열거형 안에 또 하나의 열거형이 들어갈 수 있고 클래스 안에 또 다른 ‘클래스’가 들어올 수 있다.