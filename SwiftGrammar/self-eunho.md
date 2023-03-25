# self

```swift
self.프로퍼티명 // 클래스나 구조체 자신의 인스턴스에 속한 프로퍼티
```

self는 클래스나 구조체의 인스턴스 자신을 가리킨다. self와 프로퍼티명을 구분해주는 . 은 소속의 의미를 나타낸다. 인스턴스는 클래스 외부에서만 접근할 수 있기 때문에, 클래스 내부에서는 어느 인스턴스에 할당된 것인지 알기 힘들다.

```swift
class PersonA {
	var name: String
	init(name: String){
		self.name = name
 }
}
```

위와 같은 코드의 경우 인스턴스 프로퍼티로 지칭해주기 위해 self가 사용된다.
요약 : self는 인스턴스가 가지고 있는 프로퍼티이다.

Self 타입은 특정한 Type이 아니고 타입의 이름을 반복해서 쓰는 대신에 현재 타입을 쓸 수 있도록 도와주는 것이다. 클래스, 구조체 등등에서 Self를 사용하면 그 타입을 가리킨다는 뜻이다.

```swift
class SuperClass {
func f() -> Self{
	return self
 }
}
class SubClass: SuperClass {}

let x = SuperClass()
x.f()

let y = SubClass()
y.f()
```

위 코드에서 보면 대문자 Self타입은 SuperClass와 SubClass의 타입을 가리키고 있고 소문자 self 프로퍼티는 SuperClass와 SubClassdml의 인스턴스들을 가리키고 있다.

## Self와 self의 차이점

Self는 타입프로퍼티와 타입메서드를 가리킬 때 사용된다. (Type)

self는 인스턴스프로퍼티와 인스턴스 메서드를 가리킬 때 사용된다.(instance)

self: 타입 인스턴스를 의미(참조값)

Self: 타입 그 자체를 의미