# Optional

## 옵셔널

Swift는 안정성을 높이기 위해서 오류를 별로 좋아하지 않는다 때문에 nil을 사용하여 “값이 없음"을 알린다

//nil은 null과 같은 뜻이지만 Swift에서는 nil을 사용한다

```swift
var Name: String? // 옵셔널 
```

옵셔널은 값이 존재하지 않을 상황에서 사용한다

옵셔널을 사용할때는 타입 뒤에 `?` 를 붙여서 사용한다 만약 옵셔널인데 옵셔널 처리를 안해주면 nil의 값이 들어가면 error가 뜬다(앱에서는 뜅기기도 한다)

자료형에 `?` 를 붙인 상황이라도 값을 할당하지 않는다면 자동으로 nil로 초기화된다

옵셔널 타입은 2가지 형태로 받을 수 있다

- nil: 실행과정에서 오류가 발생했을때
- nil이 아닌 값: 오류가 발생하지 않았는데 반환하려는 값이 옵셔널로 둘러싸인 형태(옵셔널 언래핑된 상태)

// 옵셔널 언래핑된 상태란 (optional(”junha”))이러한 상태를 말한다

```swift
//기능 4가지

//Forced unwrapping == 억지로 내용을 까보기 //강제 해제

//Optional binding (if let) == 부드럽게 내용을 까보기1 // 옵셔널 바인딩

//Optional binding (guard) == 부드럽게 내용을 까보기2 // 옵셔널 바인딩

//Nil coalescing == 내용을 까봤더니, 값이 없으면 디폴트 값을 주자 // 
```

```swift
//Forced unwrapping // 강제 해제
var Name: String?
Name = "준하"
print(Name) // 결과 = Optional("준하")
print(Name!) // 결과 = 준하
Name = nil
print(Name!) // 에러
```

위 코드의 경우 Optional("준하") 값이디 때문에 강제(`!`) 해도 된다.

//강제 해제 해도 될 경우는 값이 무조건 들어가는 경우다

```swift
//Optional binding (if let)
var Name: String?
Name = "준하"

if let unwrappedName = Name {
    print(Name)
} else {
    print("이름이 없다")
}

func printParsedInt(from: String) {
    if let parsedInt = Int(from) {
        print(parsedInt)
    } else {
            print("Int로 컨버팅 안됩니다")
}

printParsedInt(from: "10") // 10
printParsedInt(from: "안녕") // Int로 컨버팅 안됩니다
```

//개인적으로 언제 언래핑하는지 잘몰랐지만 밑에 글을 읽으면 완벽이해가 가능하다

보통 옵셔널바인딩은 조건문 내에서 옵셔널 값을 일반 변수나 상수에 할당하는 구문을 사용하는 방식이다.

무조건 조건문이 필요하고 값이 증명됬기 때문에 안전하게 결과물을 볼 수 있으며 `!`를 통해서 강제해제 하지 않아야 된다

```swift
//Optional binding (guard)
var Name: String?
Name = "준하"

func printParsedInt(from: String) {
        guard let parsedInt = Int(from) else {
                print("Int로 컨버팅 안됩니다")
                return
        }
        print(parsedInt)
}
```

guard let 또한 if let 처럼 옵셔널 바인딩이다 하지만 둘은 차이점이 있다

|  | 공통점 | 차이점 | 차이점 | 차이점 | 차이점 |
| --- | --- | --- | --- | --- | --- |
| guard let | Optional binding | 전역변수 | else 생략 불가 | 코드가 간결해진다 | return, break,continue,throw등의 ‘제어문 전환 명령을 사용해야함 |
| if let | Optional binding | 지역변수 | else 생략 가능 | 코드가 복잡해진다 |  |

```swift
//Nil coalescing

var Name: String?
Name = "준하"
let myName: String = carName ?? "이름"
```

초기 값을 정해주거나 nil일 경우를 대비하는 것이다 현재는 Name에 값이 들었지만 만약 네트워크 통신에서 데이터를 받지 못하거나 초기 테스트에 사용하면 유용하다
