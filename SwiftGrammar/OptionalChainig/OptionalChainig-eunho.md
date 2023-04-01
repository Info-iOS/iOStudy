# Optional Chainig

옵셔널 체이닝은 여러 값이 중첩된 형태를 띄어야 제 몫을 발휘한다. 옵셔널 체이닝을 사용하면 옵셔널을 더 편리하게 사용할 수 있다. 

옵셔널 체이닝은 옵셔널 값 뒤에 물음표(?)를 붙여서 표현 가능하다. 옵셔널을 사용할 수 있는 값에는 프로퍼티, 메소드등이 포함된다. 

물음표 대신에 느낌표( ! )를 사용할 수도 있는데 이는 옵셔널에서 값을 강제 추출하는 효과가 있다. 물음표와 가장 큰 차이점은 값을 강제 추출하기 때문에 옵셔널에 값이 없다면 런타임 오류가 발생한다.

## instance

```swift
let eunho: Person = Person(name: "eunho")
```

만약 eunho가 사는 호실 번호를 알고 싶다.옵셔널 체이닝과 강제 추출을 사용하여 프로퍼티에 접근하면 결과를 볼 수 있다. 

```swift
let eunhoRoomViaOptionalChainig: Int? = eunho.address?.building?.room?.room?.number
let eunhoRoomViaOptionalUnwraping: Int? = eunho.address?.building?.room?.room?.number
//오류
```