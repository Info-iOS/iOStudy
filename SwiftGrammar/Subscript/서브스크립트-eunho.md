# 서브스크립트

---

클래스, 구조체, 열거형에는 컬렉션, 리스트, 시퀀스 등 타입의 요소에 접근하는 단축 문법인 서브스크립트를 정의할 수 있다.

### 서브스크립트 정의 문법

```swift
subscript(index: Int) -> Int {
get {
// 적절한 서브스크립트 결괏값 반환
	}

set(newValue) {
	// 적절한 설정자 역할 수행
	}
}
```

위 코드에서 get 메서드 없이 단순히 값만 반환하도록 구현한다면 읽기 전용이 된다.

### 서브스크립트 구현

```swift
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
print("six times three is \(threeTimesTable[6])")
// "six times three is 18" 출력
```

이런식으로 문법을 단축해서 편리하게 사용 가능하다.