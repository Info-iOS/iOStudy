# 클래스와 구조체
---
클래스와 구조체는 프로그램의 코드를 조직화하기 위해서 일반적으로 사용합니다. OOP를 위한 요소이기도 합니다.
클래스와 구조체의 공통점

값을 저장하기 위한 프로퍼티 정의
기능을 제공하기 위한 메소드 정의
초기 상태를 설정할 수 있는 initializer 정의
기본 구현에서 기능 확장
특정한 종류의 프로토콜 순응
구조체로는 가능하지 않지만 클래스만 가능한 기능

상속
부모클래스가 자식 클래스에게 가지고 있는 값을 주는 것
타입 캐스팅
런타임에 클래스 인스턴스의 타입을 확인
소멸자
할당된 자원을 해제 시킴
참조 카운트
클래스 인스턴스에 하나 이상의 참조가 가능
구조체는 다른 코드로 전달될 때 항상 복사하고 참조 카운트를 사용하지 않습니다.
선언하는 방법

struct AStructure {
    var name: String = "박준하"
    var age: Int = 18
}

class AClass {
    var aStructure = AStructure()
    var aBool: Bool = false
    var aDouble: Double = 0.0
}
구조체는 타입추론을 해주지만 가능하면 자신이 사용할 변수에 데이터 타입을 입력하는 것이 베스트입니다.
클래스와 구조체를 인스턴스로 만드는 법

let aStructure = AStructure()
let aClass = AClass()
프로퍼티 접근 방법

점을 이용해서 접근할 수 있습니다
print("\\(AStructure.name)")
//구조체 접근을 위해서 점을 이용해서 안에 있는 값을 사용할 수 있습니다.
print("\\(AClass.aStructure.name)")
//클래스에 있는 구조체를 들어갈 때는 클래스 안에 있는 구조체를 가져오고 구조체의 값을 가져오면 됩니다.
구조체의 멤버 초기화하는 방법

let astructure = AStructure(name: "박준하", age: 18)
//초기화시 프로퍼티를 선언할 수 있는 초기자를 자동으로 생성해서 제공합니다.
구조체와 열거형은 값 타입

Swift에서 모든 구조체와 열거형 타입은 값 타입입니다.
let astructure = AStructure(name: "박준하", age: 18)
var a = astructure
아까 말했듯이 참조 카운트를 사용하지 않기 때문에 값을 나누었다고 한들 astructure와 a는 같지 않고 완전히 다른 인스턴스입니다.
a.name = "은호"
print(a.name) // 은호
print(astructure.name) //박준하
이것으로 두 인스턴스가 완전히 다른 개체로 다른 주소 공간에서 저장되어 사용된다는 것을 알 수 있습니다.
클래스의 참조 타입

값 타입과 달리 참조 타입은 변수나 상수에 값을 할당을 하거나 함수에 인자로 전달 한때 값을 복사하지 않고 그대로 참조합니다. 참조한다는 뜻은 같은 메모리를 보고 있다는 뜻입니다.
let aClass = AClass()
aClass.aBool = true
let bClass = aClass
bClass.aBool = false
print("\\(aClass.aBool)") // false
같은 메모리를 바라보기 때문에 값이 같이 변하는 것을 알 수 있습니다.
식별 연산자

=== : 두 상수나 변수가 같은 인스턴스를 참조하고 있는 경우에 참
!== : 두 상수나 변수가 다른 인스턴스를 참조하고 있으면 참
클래스와 구조체의 선택

클래스 인스턴스가 인자로 사용될 때는 참조가 넘어가고 구조체는 값이 넘어간다고 사전에 말했습니다. 아래는 클래스를 사용할 타임과 구조체를 사용할 타임을 나누어놨습니다.
구조체를 사용하는 경우

주목적이 관계된 간단한 값을 캡슐화하기 위한 것
인스턴스가 참조되기보다 복사하고 싶을 때
구조체에 의해 저장된 어떠한 프로퍼티가 참조되기 보다 복사하고 싶은 경우
프로퍼티나 메서드 등에 상속할 필요 없는 경우
위에 있는 경우가 아니면 전부 클래스 사용해도 됩니다.
String, Array, Dictionary의 할당과 복사 동작

swift에서 String, Array, Dictionary는 구조체로 구현할 수 있습니다. 하지만 Foundation의 NSString, NSArray, NSDictionary는 클래스로 구현돼 있습니다.
구조체에 대한 더 자세한 예

구조체는 인스턴스의 값을 저장하거나 기능을 제공하고 이것을 캡슐화할 수 있습니다.
struct Name {
    var name = "Pack"
    
    func myName() {
        print("my name is \\(name)")
    }
}

var pack : Name = Name()

print(pack.name)
pack.myName()

pack.name = "jun"
pack.myName()
구조체는 class와 코드가 매우 유사합니다 구조체 안에 있는 것을 속성이라고 부르고 구조체 안의 함수는 메소드라고 부릅니다
하지만 구조체는 class처럼 초기화를 꼭 init으로 할 필요 없이 자동으로 초기화해줍니다
struct Name {
    var name = String
        var age = Int
    
    func myName() {
        print("my name is \\(name) and \\(age)")
    }

        init(name: String) {
        self.name = name
                self.age = 17
    }
}

var pack : Name = Name()

print(pack.name)
pack.myName()
하지만 구조체를 직접 초기화하는 것도 알아야 합니다 위 코드는 구조체를 수동적으로 초기화 하는 코드입니다 하지만 수동 초기화의 경우 앞으로 자동 초기화를 제공받을 수 없습니다.
그리고 잘 보시면 인스턴스를 생성할 때 name 밖에 안 되는 것을 볼 수 있는데 그 이유는 자동초기화에서는 정의할 수 있는 age 변수를 직접 초기화를 쓴 여기는 사용할 수 없습니다 때문에 여기서 자동초기화의 혜택을 못 봤는다는 것을 알 수 있죠
그럼 마지막으로 클래스와 같이 구조체는 상속이 가능할까요? 아뇨 안돼요, 상속할 수 없습니다.

오늘도 수고 많으셨습니다.
