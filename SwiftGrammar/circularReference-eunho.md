# 순환참조

순환 참조란 두 가지 이상의 객체가 서로에 대한 강한 참조 상태를 가지고 있을 때 발생하며, 순환 참조가 발생하게 되면 서로에 대한 참조가 해제되지 않기 때문에 메모리에서 유지되며 이로 인해 메모리 릭이 발생하게 된다.

메모리릭은 개발자가 의도하지 않은 메모리를 점유하고 있는 현상을 말한다.

## 순환참조 해결 방법

순환 참조를 해결하기 위해 weak, unowned reference가 사용된다.

약한 참조를 사용하여 해결할 수 있다.

```swift
class A {
    weak var b: B?
}

class B {
    var a: A?
}

// A와 B 인스턴스 생성
var instanceA: A? = A()
var instanceB: B? = B()

// 강한 참조 사이클 형성
instanceA?.b = instanceB
instanceB?.a = instanceA

// 참조 해제
instanceA = nil
instanceB = nil
```

클래스 A는 클래스 B를 약한참조로 참조 하도록 했고. 참조 대상이 메모리에서 해제되면 자동으로 nil값을 할당하므로, 강한 참조 사이클이 형성되어도 메모리 누수 문제를 방지할 수 있다.