# 모나드

모나드는 여러 영역에서 다양한 뜻을 가지기도 하고 한 문장으로 설명하기 어려운 개념이다. 프로그래밍에서의 모나드를 모나딕이라고 표현한다. 그래서 모나드의 성질을 갖는 타입이나 함수를 모나딕 타입 혹은 모나딕 함수등으로 표현한다.

## 모나드가 갖춰야 하는 조건

- 타입을 인자로 받는 타입
- 특정 타입의 값을 포장한 것을 반환하는 함수가 존재
- 포장한 값을 변환하여 같은 형태로 포장하는 함수가 존재

## 컨텍스트

이번 파트에서 컨텍스트는 콘텐츠를 담은 그 무엇인가를 뜻한다. 물컵에 물이 담겨있는 예시를 들어보면 물이 담겨있는 물은 콘텐츠고 물컵은 컨텍스트라고 볼 수 있다.

```swift
let optionalString: String? = "Hello, world!"

let transformedOptionalString = optionalString.flatMap { string in
    return Optional("\(string.count)")
}

print(transformedOptionalString) // Optional("13")
```

문자열의 길이를 Int형으로 바꿔주는 코드.