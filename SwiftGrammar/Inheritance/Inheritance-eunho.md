# Inheritance

클래스는 메서드나 프로퍼티 등을 다른 클래스로부터 상속받을 수 있다. 상속을 받으면 자식 클래스이고 자신의 특성을 물려주면 부모 클래스이다.

부모클래스로부터 물려받은 메서드를 호출할 수 있다. 또한 물려받은 메서드, 프로퍼티등을 자신만의 내용으로 재정의 할 수 있다.

다른 클래스로부터 상속을 받지 않은 클래스를 기반클래스 라고 부른다.

```swift
Class person {
var name: String = ""
var age: Int = 0

var introduction: String{
	return "이름 : \(name). 나이 : \(age)"
}

func speak() {
	print("가나다라")
}
let yagom: Person = Person()
yagom.name = "yagom"
yagom.age = 99
print(yagom.introduction)
yagom.speak()
```

위 코드는 상속 되어 있지 않은 기반 클래스이다.

## 클래스 상속

상속은 기반클래스를 다른 클래스에서 물려받는 것을 말한다.

클래스 이름 뒤에 콜론을 붙이고 다른 클래스 이름을 써주면 뒤에 오는 클래스의 기능을 앞의 클래스가 상속받을 것임을 뜻한다.

```swift
class 클래스 이름: 부모클래스 이름 {
	프로퍼티와 메서드들
}
```

## 재정의

자식클래스는 부모클래스로부터 물려받은 특성을 그대로 사용하지 않고 자신만의 기능으로 변경하여 사용할 수 있다. 이것을 재정의라고 부른다.

상속받은 특성들을 재정의하려면 새로운 정의 앞에 override라는 키워드를 사용한다. override 키워드는 컴파일러가 조상클래스에 해당 특성이 있는지 확인한 후에 재젖이 된다. 만약 특성이 없다면 오류가 발생한다.

## 프로퍼티 재정의

부모클래스로부터 상속받은 인스턴스 프로퍼티나 타입 프로퍼티를 자식 클래스에서 용도에 맞게 재정의 할 수 있다. 단 저장 프로퍼티로 재정의할 수 없다.

## 재정의 방지

재정의를 방지하고 싶은 특성 앞에 final 키워드를 명시하면 재정의가 되지 않는다.

## 이니셜라이즈 지정

```swift
init(매개변수들) {
	초기화 구문
}
```

```swift
convenience init(매개변수들) {
	초기화 구문
}
```

편의 이니셜라이저 지정

## 이니셜라이저의 상속 및 재정의

스위프트의 이니셜라이저는 부모클래스의 이니셜라이저를 상속받지 않는다.

하지만 안전하고 적절하다고 판단되는 특정한 상황에선 상속이 가능하다.

마찬가지로 override 수식어를 붙여야한다.
