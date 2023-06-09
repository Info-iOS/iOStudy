# 3/17 요약

## 1. Data Type

3/14일은 데이터 타입에 대하여 공부하였다. 

공부한 데이터타입은 Bool, Int, UInt, Float, Double, Character, String, AnyObject, nil, Typealies, Array, Dictionary, Set, NSSet등 이다.

1. Bool

Bool은 불리언 타입이다. 
불리언의 데이터 타입은 참(true) 또는 거짓(false)만 값으로 가진다.

1.  Int와 UInt

Int와 UInt는 정수형 데이터 타입이다. 

Int는 +, - 부호를 포함한 정수를 뜻한다. 
UInt는 -부호를 포함하지 않는 양의 정수를 표현한다.  
Int와 UInt는 각각 8비트, 16비트, 32비트, 64비트의 형태가 있다.

 3.  Float과 Double 

Float과 Double은 부동소수점을 사용하는 실수며 부동소수 데이터 타입이라 한다. 
흔히 말해 소수점 자리가 있는 수이다. 
또한 정수형 데이터 타입보다 훨씬 넓은 범위의 수를 표현할 수 있다. 

4. Character 
Character는 말 그대로 문자를 의미한다.  
a,b,c 와 같은 문장과 단어가 아닌 하나의 문자를 의미한다. 
스위프트는 유니코드9 문자를 사용하므로 영어 그리고 특수기호 등 유니코드에서 지원하는 모든 언어 및 특수기호를 사용할 수 있다. 
문자를 표현하기 위해서는 값의 앞뒤에 큰따옴표를 사용해서 표현해야한다. 

1. String  

String은 문자(Charater)의 나열, 즉 문자열이다.  
String은 Character와 마찬가지로 유니코드9를 사용할 수 있으며 앞뒤에 큰따옴표를 사용하여 표현합니다. 

6.   Any, AnyObject와 nil 

Any는 스위프트의 모든 데이터 타입을 사용할 수 있다는 뜻이다. 

 변수 또는 상수의 데이터 타입이 Any로 지정되어 있다면 그 변수 또는 상수에는 어떤 종류의 데이터 타입이든지 상관없이 할당할 수 있다. 
 
-AnyObject는 Any보다는 조금 한정된 의미로 클래스의 인스턴스만 할당할 수 있다. 
쉽게 말해 AnyObject는 클래스의 프로토콜이다. 
 
nil은 특정 타입이 아니라 '없음'을 나타내는 스위프트의 기워드 이다.  
즉, 변수 또는 상수에 값이 들어있지 않고 비어있음을 나타내는데 사용한다. 

1. Typealias 

스위프트에서 Typealias는 데이터 타입의 별칭이라고 할 수 있다.  
현재 제공되어 있는 기본 타입의 별명을 만들어 대신 사용하는 것이다. 

1.  Array 

 Array는 배열이다.  
배열을 사용할 때 Array라는 키워드와 타입 이름의 조합으로 사용한다. 
Array가 특별한 점은 C언어의 배열처럼 한 번 선언하면 크기가 고정되는 버퍼가 아니라, 필요에 따라 자동으로 버퍼의 크기를 조절해준다. 

1. 10. Dictionary 

딕셔너리는 요소들이 순서 없이 키와 값이 쌍으로 구성되는 컬렉션 타입이다.  

 10. Set와 NSSet 
세트는 같은 타입의 데이터를 순서 없이 하나의 묶음으로 저장하는 형태의 컬렉션 타입이다. 
세트 내의 값은 중복된 값이 존재하지 않는다.  
그렇기 때문에 순서가 상관없고 각 요소가 중복되지 않은 값이어야 하는 경우에 상용한다. 
또 , 세트의 요소로는 해시 가능한 값이 들어와야 한다. 
스위프트에서 기본 데이터 타입은 모두 해시 가능한 값이다. 
 

NSSet은 Objective-C에서 사용되었으며 현재 스위프트에서는 Set으로 대체되었다. 
NNset은 Set와 비슷한 동작을 하지만 차이점이 있다. Set는 값의 유일성을 보장하면서도 동시에 값의 순서도 보장하지만 NSSet는 값의 순서를 보장하지 않는다.

## Flow Control

스위프트의 흐름 제어 구문에서는 소괄호(())를 대부분 생략할 수 있다. 하지만 중괄호({})는 생략할 수 없다.

1. 조건문

조건문에서는 if와 switch구문이 있다. 스위프트의 조건문에는 guard구문도 있다.

1. if구문

if 구문은 대표적인 조건문으로 if, else등의 키워드를 사용하여 구현할 수 있다. 정수, 실수 등 0이 아닌 모든 값을 참으로 취급하여 조건 값이 될 수 있는 다른 언어와는 다르다. 스위프트의 if 구문은 조건의 값이 꼭 Bool 타입이어야함.

else if는 몇개가 이어져도 상관없고 else 블록은 없어도 상관없다. if 키워드 뒤에 따라오는 조건수식을 소괄호로 감싸주는 것은 선택 사항입니다.

1. switch 구문 

기본 문법이라 할 수 있는 switch 구문은 다른 언어와 비교했을 때 많이 달라진 문법 중 하나이다. break 키워드 사용은 선택 사항이다. 이 뜻은 case 내부의 코드를 모두 실행하면 break 없이도 switch 구문이 종료된다는 뜻.

switch 구문의 case를 연속 실행하려면 fallthrough 키워드를 사용한다. switch 구문은 조건에 다양한 값이 들어갈 수 있다. 하지만 각case에 들어갈 비교 값은 입력 값과 데이터 타입이 같아야한다.

1. 반복문

반복문은 같거나 비슷한 명령을 반복 실행할 때는 반복문이 중요하다

1. for-in 구문

for-in 반복 구문은 반복적인 데이터나 시퀀스를 다룰 때 많이 사용합니다.

for 임시상수 in 시퀀스 아이템 { 실행코드 }

스위프트에 좀 더 익숙해져서 옵셔널, 클로저 등을 배우고, 함수형 프로그래밍 패러다임을 이해하면 for-in 구문보다 map. filter, flatMap 등을 더 많이 사용하게 된다.

1. while 구문

while 반복 구문도 다른 프로그래밍 언어의 While 구문과 크게 다르지 않다. while은 Bool 타입으로 지정되어야 한다. while도 for-in구문과 만찬가지로 continue, break 등의 제어 키워드 사용이 가능하다.

1. repeat while

repeat-while 반복 구문은 다른 프로그래밍 언어의 do-while 구문과 크게 다르지 않다. repeat 블록의 코드를 최초 1회 실행한후, while 다음의 조건이 성립하면 블록 내부의 코드를 반복 실행한다.

## Function

1. 함수

함수 대부분은 작업의 가장 작은 단위이자 하나의 작은 프로그램이기도 하다.

스위프트에서 함수는 다른 언어보다 훨씬 다양한 모습으로 존재하고, 코딩스타일도 다양하다.

따라서 팀 프로젝트를 진행할 때에는 코딩 규칙을 만들어 함수를 사용하는게 좋다.

1. 함수와 메서드

함수와 메서드는 기본적으론 같다.

단지 상황이나 위치에 따라 다른 용어로 부르는 것.

특정 타입에 연간되어 사용하면 메서드 전체에서 다 사용할 수 있으면 그냥 함수이다.

1. 함수의 정의와 호출

함수와 메서드는 정의하는 위치와 호출되는 범위만 다를 뿐, 정의하는 키워드와 구현하는  방법은 같다. 조건문이나 반복문 같은 스위프트의 다른 문법과 달리 함수에서는 소괄호(())를 생략할 수 없다. 

함수는 재정의와 중복 정의를 모두 지원한다. 따라서 매개변수의 타입이 다르면 같은 이름의 함수를 여러 개 만들 수 있고, 매개변수의 개수가 달라도 같은 이름의 함수를 만들 수 있다. 따라서 이름이 같은 함수를 구현해도 오류가 발생하지 않는다.

1. 함수의 호출과 기본형태

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

1. 매개변수

스위프트의 함수는 매개변수를 어떻게 정의하냐에 따라서도 모습이 크게 달라질 수 있다.

1. 매개변수가 없는 함수와 매개변수가 여러 개인 함수

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
//매개변수가 여러 개인 함수의 정의와 사용 책 예제
func sayHello(myName: String, yourName: String) -> String{
return "Hello \(yourName)! I'm \(mmyName)"
}
print(sayHello(myName:"yagom", yourName:"Jenny"))
```

매개변수가 여러 개  필요한 함수를 정의할 때는 쉼표( , )로 매개변수를 구분한다. 

주의할 점은 함수를 호출할 때, 매개변수 이름을 붙여주고 콜론( : )을 적어준 후 전달인자를 보내준다는 점.

1. 매개변수 이름과 전달인자 레이블

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

8.매개변수 기본값

스위프트의 함수에서는 매개변수마다 기본값을 저장할 수 있습니다.

즉, 매개변수가 전달되지 않으면 기본값을 사용합니다. 

1. 기본 매개변수와 입출력 매개변수

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

1. 중첩 함수

스위프트는 데이터 타입의 중첩이 자유롭다.

열거형 안에 또 하나의 열거형이 들어갈 수 있고 클래스 안에 또 다른 ‘클래스’가 들어올 수 있다.

따라서 함수도 중첩하여 사용할 수 있다.