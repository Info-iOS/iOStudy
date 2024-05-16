# 접근 제어자

## 접근 제어자(Access Control)란?

코드끼리 상호작용을 할 때 파일 간 또는 모듈 간에 접근을 제한할 수 있는 기능

접근 제어를 통해 코드의 상세 구현은 숨기고 허용된 기능만 사용하는 ❣️인터페이스를 제공할 수 있음.

❣️인터페이스는 프로그램의 다양한 요소 간의 상호 작용을 정의하고 조직하는데 중요한 역할을 함

## 접근 제어자(Access Control)의 종류

접근 제어는 접근수준(Access Level) 키워드를 통해 구현

각 타입에 특정 접근수준을 지정 ⭕️, 타입 내부의 프로퍼티, 메서드, 이니셜라이저, 서브스크립트 각각에도 접근구준을 지정할 수 있음

### 1. open - 개방 접근수준

open 접근 제어자는  개방 접근수준 공개 접근수준 이상으로 높은 수준의 접근 제어자로, 다른 모듈에서도 해당 클래스나 메서드를 ❣️서브클래싱(subclassing)하거나 ❣️오버라이딩(overriding)할 수 있음

open으로 선언된 클래스나 메서드를 상속하거나 재정의해서 사용

➡️ 보통 외부 라이브러리를 만들고 사용할 때 유용

‼️ 클래스와 클래스의 멤버에서만 사용 가능

❣️서브클래싱(subclassing)은 기존 클래스를 기반으로 새로운 클래스를 정의하는 과정

❣️오버라이딩(overriding)은 부모 클래스에서 이미 정의된 메서드를 자식 클래스에서 다시 정의하여 사용하는 것

```swift
open class Animal {
	open func bark() {
		print("으르렁")
	}
}

class Dog: Animal {
	override open func bark() {
		print("멍멍")
	}
}
```

### 2. public - 공개 접근수준

접근수준이 지정된 요소는 어디서든 쓰일 수 있음

공개 접근수준은 주로 ❣️프레임워크에서 외부와 연결된 인터페이스를 구현하는데 많이 쓰임

‼️ 다른 모듈에서 서브클래싱하거나 오버라이딩 ❌

❣️프레임워크(Framework)는 애플리케이션 개발을 위해 재사용 가능한 코드와 라이브러리의 집합을 의미

```swift
 public class Animal {
	public func bark() {
		print("으르렁")
	}
}

// 다른 모듈에서 작성한 코드라면 재저의 불가능
public class Dog: Animal {
	override public func bark() { // 오류
		print("멍멍")
	}
}
```

### 3. internal - 내부 접근수준

기본적으로 모든 요소에 암묵적으로 지정하는 기본 접근수준

같은 모듈 내에서 어디서든지 해당 요소들을 사용 ⭕️ (‼️ 모듈 외부에서는 사용❌)

```swift
internal class Cat: Animal {
	override internal func bark() {
		print("야옹")
	}
}

// 외부 모듈이라면
let cat: Cat = Cat() // 오류
```

### 4. fileprivate - 파일외부비공개 접근수준

지정된 요소는 그 요소가 구현된 소스파일 내부에서만 사용 ⭕️

```swift
fileprivate class Dog {
	fileprivate func bark() {
		print("멍멍")
	}
}

fileprivate let dog = Dog() // 다른 소스 파일이라면 오류
dog.bark()
```

### 5. private

가정 한정적인 범위

지정된 요소는 기능을 정의하고 구현한 범위 내에서만 사용 ⭕️

‼️ 지정한 기능은 심지어 같은 소스파일 안에 구현한 다른 타입 or 기능에서도 사용 ❌

```swift
class Company {
	private let developer = Developer()
	
	func writeCode() {
		developer.writeCode()
	}
}

let company: Company = Company()
company.developer.? // 접근 불가능 오류
```

접근 제어자는 모듈,  소스 파일,  클래스, 구조체, 열거형, 속성, 함수, 메서드 등 다양한 요소에 적용됨.

‼️ 상위 요소보다 하위 요소가 더 높은 접근수준을 가질 수 없다.

‼️ 열거형의 접근수준을 구현할 때 열거형 내부의 각 case별로 따로 접근수준을 부여 ❌