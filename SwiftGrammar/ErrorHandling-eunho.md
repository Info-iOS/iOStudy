# ErrorHandling

Error Handling은 프로그램에서 에러 조건들에 대해 대응하고 회복하는 프로세스이다.

Swift는 런타임에서 에러가 발생한 경우 해당 에러를 처리하기 위해 throwing, catching 등이 있다.

## Throw

Swift에서 에러는 Error 프로토콜을 준수하는 타입의 값으로 표현된다.

```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}

throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```

자판기 오류 예시 코드 

에러를 던지는 것(throwing)은 예기치 못한 무언가가 발생했고 일반적인 실행 흐름을 계속할 수 없다는 것을 가리킨다. throw**문**을 사용하여 에러를 발생시킬 수 있다. 위 코드처럼 코인이 다섯 개 부족하다는 코드도 만들 수 있다.

## Catch

do-catch문을 사용하여 에러를 처리하는 코드 블록을 작성할 수 있다. 만약 에러가 do절 안에서 코드에 의해 발생한다면, catch절 중에서 일치하는 것을 결정해 에러를 처리할 수 있습니다.