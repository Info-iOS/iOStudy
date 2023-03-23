# 클로저

---

클로저는 코드블럭으로 C와 Objective-C의 블럭과 다른 언어의 람다와 매우 많이 비슷합니다.

클로저는 어떤 상수나 변수의 참조를 캡쳐해 저장할 수 있습니다. swift는 이 캡쳐와 관련한 모든 메모리를 알아서 처리합니다.

- 전역 함수: 이름이 있고 어떤 값도 캡쳐하지 않는 클로저
- 중첩 함수: 이름이 있고 관련한 함수로 값을 캡쳐 할 수 있는 클로저
- 클로저 표현: 문맥으로 부터 값을 캡쳐할 수 있는 이름이 없는 클로저

클로저

- 문맥에서 표현은 인자 타입과 반환 타입의 추론
- 단일 표현 클로저에서의 암시적 반환
- 축약된 인자 이름
- 후위 클로저 문법

클로저 표현

- 클로저 표현은 코드의 명확성과 의도를 잃지 않으면서도 문법을 축향해 사용할 수 있는 다양한 문법의 최적화 방법을 제공합니다

클로저 표현 문법

- 클로저 표현 문법은 일반으로 아래의 형태를 가집니다.

```swift
{ (parameters) -> return type in
    statements
}
```

- 인자로 넣을 parameters, 인자 값으로 처리할 내용을 기술하는 statements 그리고 return type입니다.

```swift
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

- 위 코드를 인라인 클로저라고 부릅니다.
- 클로저의 몸통은 in 키워드를 사용합니다.

클로저는 2가지가 있다

named Closure 와 unnamed closure

```swift
func goodjunha(){
        print("junha")
}
```

이게 named closure임 하지만 우리는 이것을 함수라도 부른다

그리고 이름을 붙이지 않고 사용하는 함수

```swift
let closure = { print("Somaker")}
```

이게 unname closure임 

근데 보통 closure라고 하면 보통은 unnamed closure라고 한다

{(Parameters) → Return Type in

실행구문

}

이제 closure Head 와 closure Body 를 구분지어 주는 것이 바로 in이다

위구문에서 실제로 return Type를 사용하지 않는 것처럼 생략이 가능하가

그리고 Parameters까지 생략 할 수 있다

```swift
let closure = { () -> () in
    print("closure")
}
```

---

Parameter 와 Return Type이 있는 클로저

```swift
let closure = { (name: String) -> String in 
        return "Hello, \(name)"
}
```

이때 클로저를 호출할 때 

```swift
closure("closure") //good
closure("name: "Sodeul") //error
```

```swift
func doSomething() -> () -> () {

        return { () -> () in
                print("hello sodeul!")
                        }
} 
```

closure는 return 이 가능함

변수와 상수를 대입하지 않고 사용할려면

```swift
({ () -> () in
        print("hello sodeul!")
})()
```

---

closure를 사용할 때 나는 지금 bool을 많이 보아서 bool에 대한 설명을 한번 짚어보고 가자
