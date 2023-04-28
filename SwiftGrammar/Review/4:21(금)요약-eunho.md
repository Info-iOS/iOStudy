# 4/21 (금) 요약

# AlertView

### **UIAlertController**

---

- UIAlertController는 두 가지 형태로 메시지 창을 표현할 수 있다.
- 하나는 **알림창**, 다른 하나는 **액션시트이**다.

---

### Alert의 구성요소

```swift
var title: String?
	//제목

var message: String?
	//메세지

var preferredStyle: UIAlertController.Style
	// alert, action sheet 둘중 하나 고르는 스타일

let alert = UIAlertController(title: "타이틀입니다", message: "메세지입니다", preferredStyle: .alert)
```

- 이런 식으로 AlertView를 사용하면 애플이 제공해주는 기본 팝업창을 수월하게 사용할 수 있다.
- toDoList에서 사용하려는 목적
- Alert View를 띄워서 입력하고 Action 하려고 한다.

# Custom View Controller

---

## 사용 이유

---

- 앱의 특정 부분을 다른 개발자와 공유하기 위해 사용한다.
- 재사용성을 높이기 위해 사용합니다.
- 유지 보수성을 높이기 위해 사용합니다.
- 코드를 구성하여 구조를 개선할 수 있다.
- 재사용성을 높이기 위해 사용합니다.
    
    Custom View Controller를 사용하면 동일한 UI 요소를 여러 곳에서 사용할 수 있다. 이는 코드 중복을 방지하고 앱의 유지 보수성을 높이는 데 도움이 된다.
    
- 유지 보수성을 높이기 위해 사용한다.
    
    Custom View Controller를 사용하면 코드의 가독성을 높일 수 있다. 비슷한 기능을 하는 코드가 한 곳에 모이기 때문이다. 또한, Custom View Controller는 다른 View Controller와 분리되어 있으므로 코드 수정을필요한 View Controleler에서만 수정하면 된다.
    

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

# Library

라이브러리는 일반적으로 최적화된 코드를 포함하므로, 스위프트에서 직접 구현하는 것보다 높은 성능을 제공할 수 있습니다.

### SnapKit

```swift
myView.snp.makeConstraints { make in
    make.top.equalToSuperview().offset(50)
    make.left.equalToSuperview().offset(50)
    make.right.equalToSuperview().offset(-50)
    make.bottom.equalToSuperview().offset(-50)
}
```

이와같이 표현해줄 수 있다. Auto Layout의 복잡성과 번거로움을 줄여주고, 코드를 간결하게 작성할 수 있게 도와준다. 또한 코드의 가독성도 좋아짐

### then

```swift
let label: UILabel = {

  let label = UILabel()
  
  label.textColor = .black
  
  label.text = "Hello, World!"
  
  return label
  
}()
```

이러한 초기화 코드가 있다면 then을 활용해서 밑과 같이 만들 수 있다.

```swift
let label = UILabel().then {

  $0.textColor = .black
  
  $0.text = "Hello, World!"
  
}
```

이렇게 만들면 훨씬 편리하고 가독성이 편해지며 오류를 감소 시킬 수 있다.

# Map

맵은 자신을 호출할 때 매개변수로 전달된 함수를 실행하여 그 결과를 다시 반환해주는 함수이다.
Map 함수를 사용하면 기존의 컬렉션을 변경하지 않고도 각 요소에 대해 일괄적으로 작업할 수 있으므로, 작업의 효율성과 코드의 안정성을 높일 수 있다.

```swift
let numbers = [1, 2, 3, 4, 5]
```

```swift
let doubledNumbers = numbers.map { $0 * 2 }
print(doubledNumbers) // [2, 4, 6, 8, 10]
```

map 함수는 클로저(함수)를 전달받아, 해당 클로저를 컬렉션의 모든 요소에 대해 적용하고, 그 결과를 새로운 컬렉션으로 반환한다. 이를 통해 기존 컬렉션을 변경하지 않고도 새로운 컬렉션을 생성할 수 있다.

# Filter

---

- 필터는 스위프트에서 특정 조건을 만족하는 요소들만 추출하여 새로운 배열을 생성하는 고차함수이다.

---

ex) [1, 2, 3, 4, 5] 배열에서 짝수만 뽑아 내고 싶다면 밑 코드와 같이 filter를 사용할 수 있다.

```swift
let numbers = [1, 2, 3, 4, 5] // numbers라는 배열에 1,2,3,4,5를 넣어줬다
let evenNumbers = numbers.filter { $0 % 2 == 0 } // evenNumbers 라는 배열에 필터를 사용해서 짝수만 뽑아 내는 조건을 만들었다.
// 그러면 뽑아낸 결과값이 evenNumbers 배열 속으로 들어감
print(evenNumbers) // 출력 결과: [2, 4]
```

위의 코드에서 2번 째 줄에 있는 {$0 % 2 == 0} 은 클로저로, 배열의 각 요소에 대해 실행되며 해당 요소마다 조건을 확인한다. 조건에 해당한다면(짝수라면) filter함수는 그 요소를 새로운 배열에 추가하게 된다.

---

ex) 이번엔 배열안에 숫자가 아닌 문자를 넣어 조건에 맞게 요소를 뽑아내는 코드를 만들었다.

```swift
let strings = ["apple", "banana", "kiwi", "orange", "pear"] //총 5개의 단어를 strings배열 안에 집어넣음.
let shortStrings = strings.filter { $0.count <= 5 } // 조건에 맞는 요소는 새로운 shortStrings라는 배열에 들어가게 된다.
print(shortStrings) // 출력 결과: ["apple", "kiwi", "pear"]
```

위의 코드는 문자의 길이가 5이하일 때 추출하여 출력하는 프로그램이다. 2번째 줄 클로저 개념은 글자수를 카운트 했을때 5이하인가>? 라는 뜻 따라서 글자수가 5이하인  apple, kiwi, pear 가 새로운 배열에 들어가 출력했을 때 위와 같이 나온다.

---