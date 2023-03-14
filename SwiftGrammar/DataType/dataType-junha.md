## Boolean

-   불이라고도 하고 불리언이라고도 부른다
-   true, false의 단일 값을 가진다.
-   if나 swiftch에서 주로 사용한다.
-   Sendable을 상속받고 있습니다.
    -   int.type과 같이 암시적으로 프로토콜을 준수합니다.

```
//근본(지정)
let a: Bool = true
let b: Bool = false

//근본(선언)
let a: Bool?
```

```
//이럴 경우 any 타입으로 인식후 값을 자동 저장
let a = 10 > 12 // a = false 저장
let b = 10 && 10 // b == true 저장
```

if문 사용 예제

```
let a = true 

if a == true {
    print("true")
} else {
    print("false")
}
```

## Int, UInt

Int는 +,- 정수를 담을 수 있습니다. 하지만 UInt는 -를 포함하지 않고 0 까지만을 허락하는 int 타입의 정수입니다.

int와 UInt는 각각 8비트, 16비트, 32비트, 64비트의 형태가 있습니다.

int8, int16, int32, int64 / uint8, uint16, uint32, uint64 등 데이터 타입에 따라서 분리돼있습니다.

보통 우리가 쓰는 Int는 Int64를 사용하고 있는 것과 같습니다. UInt도 UInt64를 사용하는 것과 같습니다.

## Float, Double

Float와 Double는 부동 소수점을 사용하여서 실수이며 부동소수 타입이라고 합니다.

swift 64Bit는 Double이 사용하고 Float는 32Bit의 부동 소수를 표현할 때 사용합니다. 근데 만약 자기가 Float를 사용할지 Double을 사용할지 모르겠다면 가급적으로 Double을 사용하는 것이 좋습니다.

```
var f: Float = 1.2345678910
var d: Double = 1.2345678910

print("\(f)") //1.23456789
print("\(d)) //1.2345678910
```

## Strings, Characters

strings 타입은 Character 타입의 집합입니다.

swift는 문자열과 문자 타입은 빠르면 유니코드에 호환됩니다.

자바와 같이 두 개의 문자열을 합칠 때는 +를 사용하여 연결할 수 있습니다.

swift의 String은 NSString 클래스에 연결돼있습니다.

Cocoa 또는 Cocoa Touch의 Foundation 프레임워크에 NSString API를 호출하며 String 값을 만드는 것이 가능합니다.

swift에서는 초기 문자열이 리터럴 값이 되기 때문에 string 타입의 영향을 받습니다.

```
//string 초기화 방법
var a: String = ""
var b: String = String()
//두개다 String을 초기화 한 것은 동일합니다.
```

그리고 isEmpty를 사용하면 문자가 비어있는지 들어있는지 알 수 있습니다.

문자열은 값 타입

swift에서 문자열 타입은 값 타입. 문자열 값은 함수나 메서드를 통해 문자열 값으로 전달됩니다. 때문에 전달된 문자열은 원본이 아닙니다.

## AnyObject

AnyObject를 알기 전 Any를 알아야 합니다.

-   Any? = 함수타입을 포함하여 모든 타입의 인스턴스를 나타낼 수 있습니다.

그럼 이제 AnyObject는 무엇일까요?

-   AnyObject? = 모든 클래스 타입의 인스턴스를 나타낼 수 있습니다.

쉽게 생각하면

```
var ar: [Any] = [1,2,"3",-1]
//이게 되는 것이 Any입니다.
```

그럼 AnyObject도 이렇게 시용해야구나!

```
var ar: [AnyObject] = [1,2,"3",-1]
//이렇게 하면 에러납니다.
```

에러를 볼까요?

> **error: value of type 'Int' does not conform to expected element type 'AnyObject'**

해석하면 배열에 있는 AnyObject가 준수하지 않았다는 뜻입니다.

```
var ar: [AnyObject] = [1 as AnyObject,2 as AnyObject,"3" as AnyObject,-1 as AnyObject]
```

이러면 에러가 해결될 것입니다.

AnyObject는 프로토콜입니다.

AnyObject는 모든 클래스가 암시적으로 준수하는 프로토콜이라고 애플 공식 사이트에서 쓰여있습니다. 때문에 AnyObejct는 일반 데이터의 타입에서 사용하는 것이 아니라 class를 사용할 때 사용하는 것이 에러가 나지 않습니다.

```
class a {}
class b {}

var abObject: [AnyObject] = [a(), b()]
//이러면 에러가 발생하지 않습니다.
```

## nil

-   nil은 값이 없을 뜻합니다

예시) 화장실에 갔는데 휴지는 없지만 휴지 심만 있으면 0 휴지와 관련된 모든 것이 없으면 nil입니다.

c언어나 java에서는 NULL을 사용하지만 swift나 Objective-C에서는 nil을 사용합니다.

하지만 Objective-C에서는 nil을 존재하지 않는 객체의 포인터라고 하지만 swift에서의 nil은 포인터가 아니라, 단지 특정 타입에 대한 값의 부재를 보여주는 것이다.

줄여서 nil은 swift에서 특정 타입에 대한 값의 부재를 표현한다.

## typealias

-   기존에 선언되어 있는 것을 코드에 읽기 쉽도록 내가 알기 쉬도록 하는 문법입니다.

3가지의 유형이 있는데

-   내장 유형 → String, Int, Float
-   사용자 정의 유형 → Class, Struct, Enum
-   복합 유형 → Closure
-   열거형

열거형은 연관된 값들의 그룹을 만들어 주는 것입니다.

swift에서는 enum을 사용하여 열거형을 만들 수 있습니다.

예시) 내장 유형

```
typealias User = String

let user1: User = "박준하"
let user2: String = "박준하"
//둘다 같은 데이터를 똑같이 보관하지만 String만 내가 원하는 것으로 하냐 않하냐의 차이입니다.
```

예시) 사용자 정의 유형

-   열거형

열거형은 연관된 값들의 그룹을 만들어 주는 것입니다.

```
Class Hello {}

typealias Hello = [Hello]
var hello: Hello = []
```

예시) 복합적이 유형 예시

```
func test(c: (Void) -> (Void) ) {

}

typealias voidHandler = (Void) -> (Void)

func test(c: voidHandler) {

}
```

## Array

Array(배열) - 멤버가 순서를 가진 리스트 형태의 컬렉션 타입

💡 참고로 배열의 값은 옵셔널이다

```
//정식 문법
let numbers: Array<Int> = [2, 4, 6, 8]

//축약형
let numbers: [Int] = [2, 4, 6, 8]
```

원래는 Array 이런 식으로 적는데 보통의 사람 들어 축약형을 더욱 선호합니다

그리고 우리의 Swift는 타입 명시를 하지 않아도 자동으로 타입 유추를 하기 때문에 굳이 타입을 안 정해줘도 됩니다(하지만 가능한이면 적어주는 버릇을 들이는 것이 좋습니다)

```
//배열을 추가 하고 싶다면?
numbers.append(10) //출력 = [2, 4, 6, 8, 10]

numbers += [12, 14, 16] //[2, 4, 6, 8, 10, 12, 14, 16]
```

배열을 추가하고 싶으면 `append`를 사용하여서 하나하나씩 추가해주는 방법이 있습니다, 그리고 추가 한 배열은 자동으로 뒤에 추가됩니다

또는 여러 가지 배열값을 추가해주고 싶으면`+=` 을 사용해지면 간결해집니다.

```
//만약 값을 알고 싶다면?
firstItme = numberItem[0] //첫 번째 아이템
print(firstItme)

numbers.contains(2) // true
```

자신이 정한 변수 뒤에 \[\]를 붙이고 찾고 싶은 값을 쓰면 인덱스 값을 출력할 수 있다

`contains`를 사용하여서 내용물을 확인할 수도 있다, 참고로 `contains`는 Bool이라서 `true`, `false`로 표현한다

```
//배열의 값을 삭제 및 수정하고 싶다면?
let firstItem = numbers.first // 초반에 옵셔널이 없을 수 있음 // 출력 = Optional(2)
let lastItem = numbers.last // 초반에 옵셔널이 없을 수 있음 // 출력 = Optional(16)

numbers.min() // Optional(2)
numbers.max() // Optional(16)

numbers.insert(0, at: 1) //0번째 인덱스가 2에서 1로 바뀜

numbers.removeAll() //모든 것을 없에 버림

numbers.remove(at: 0) //0번째 값이 사라지고 다시 재정렬됨
```

`min`를 사용해서 최솟값을 찾을 수 있고

`max`를 사용해서 최댓값을 찾을 수 있고

`insert`를 사용해서 (`인덱스`, at: `원하는 값`)을 넣어서 값을 바꿀 수 있다

`removeAll을` 사용하여서 전부 초기화시켜줄 수도 있고

`remove를` 사용하여서 원하는 `index` 값만 삭제할 수 있다

```
//비어있는지 확인하고 싶으면?
let isEmpty = numbers.isEmpty
```

`isEmpty를` 사용하여서 값이 있는지 없는지를 확인할 수 있다 `isEmpty`는 bool 형태라서 `true`, `false`로 표현한다

```
//몇개인지 확인하고 싶다면?
numbers.count // 출력 = 8
```

`count`를 사용하여서 개수를 확인할 수 있다.

```
//값의 순서를 바꾸고 싶다면?
numbers.swapAt(0, 15)
```

`swapAt`을 사용하면 원하는 `index`의 값을 두 개의 `index를` 바꿀 수 있다

```
//값을 순간 다르게 하고 싶다면?
numbers.dropFist(3)
numbers.prefix(4)
```

`dropFist를` 사용하면 앞에 3개를 없애지만 실제로는 제거하지 않음

`prefix를` 사용하면 앞에 3개만 가져오고 실제로는 제거되지 않음

## Dictionary

딕셔너리란 바구니라는 예시를 사용할 수 있습니다. 하나의 변수에 여러 개의 값을 넣을 수 있기 때문입니다

```
var scores: [String: Int] = ["a":100, "b": 20, "c": 50]
//var scores: Dictionary<String, Int> = ["a":100, "b": 20, "c": 50]
```

딕셔너리의 기본 형태는 Dictionary <String, Int>이지만 주로 \[String: Int\]를 사용합니다

```
print(scores["a"])
// Optional(100)
```

하지만 Dictionary는 Array와 비슷하게 값이 없을 수도 있기 때문에 옵셔널 형태입니다

```
if let score = scores["a"] {
        print(score)
} else {
        print("스코어 없음")
}
```

때문에 코드를 불러오고 싶으면 옵셔널 바인딩을 하는 것을 추천합니다

```
scores["d"] = 0
print(scores)
//["a":100, "b": 20, "c": 50, "d": 0]
```

값을 추가하고 싶으면 딕셔너리 값에 이름을 써주고 원하는 값을 `=` 키워드 뒤에 적어주면 됩니다

```
scores["a"] = 200
print(scores)
//["a":200, "b": 20, "c": 50, "d": 0]
```

값을 수정하고 싶으면 이름을 배열에 적어주고 값을 `=` 키워드 뒤에 수정값을 적으면 됩니다

값제거 또는 크고 작은 값 찾기 개수 알기 등등은 Array의 값과 동일합니다.

## Set, NSSet

> 주의!! set은 배열과 동일하게 \[\]로 생성하기 때문에, 타입을 추론할 수 없습니다.  
> (타입 추론 시 배열로 추론됨)

Set은 Any로 생성 불가하지만 타입에 민감하지 않은 우리 obj-c는 NSSet을 사용해서 여러 Set을 가질 수 있습니다.

```
var set1: Set<Int> = [1,2,3]

//개수가 궁금하다면?
let count: Int = set1.conunt // 3

//비어 있는지 궁금하다면
let empty: Boll = set1.isEmpty // false

//요소 확인
set1.contains(1) // true
set1.contains(10) // false

//set의 값 추가하기
set1.insert(1) //false 중복이면 false
set1.insert(10) //true

//값이 존재하지 않으면 nil 존재하면 덮어쓰기
set1.update(with: 1) // 한가지 요서 삭제 할경우 사용합니다. 삭제 후 삭제한 값 return 없는 요소 삭제시 nil 리턴
set1.update(with: 10) // nil

// 요소 삭제 (요소가 있으면 삭제 없으면 nil)
set1.remove(1) // Optional(1)
set1.remove(10) // nil

//전체 요소 삭제
set1.removeAll()
```
