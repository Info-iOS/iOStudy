# RxSwift Maybe

---

> Maybe
> 

Maybe는 Single과 Completable사이에 있는 Observable의 변형이다.

- 완료된 이벤트, 싱글 이벤트 또는 오류를 방출한다.
- 부수작용을 공유하지 않는다.

Maybe를 요소를 방출하는 연사자 모델을 위해 사용할 수 있다. 그러나 요소들을 방출하는 것이 꼭 필요해야하는 것은 아니다.

![Untitled](RxSwift%20Maybe%20f2ee7f43ea304eb4953a1a3a068441fc/Untitled.png)

Maybe 코드 예제

```swift
func generateString() -> Maybe<String> {
    return Maybe<String>.create { maybe in
        maybe(.success("RxSwift"))

        // OR

        maybe(.completed)

        // OR

        maybe(.error(error))

        return Disposables.create {}
    }
}
```

위와 같은 형태로 만들수 있고 사용하는 코드는 아래와 같다.

```swift
generateString()
    .subscribe { maybe in
        switch maybe {
            case .success(let element):
                print("Completed with element \(element)")
            case .completed:
                print("Completed with no element")
            case .error(let error):
                print("Completed with an error \(error.localizedDescription)")
        }
    }
    .disposed(by: disposeBag)
```

위는 switch case 를 사용하여 maybe를 사용하는 방법이고 아래는 subscribe(onSuccess:onError:onCompleted:)를 사용하여 하는 방법이다.

```swift
generateString()
    .subscribe(onSuccess: { element in
                   print("Completed with element \(element)")
               },
               onError: { error in
                   print("Completed with an error \(error.localizedDescription)")
               },
               onCompleted: {
                   print("Completed with no element")
               })
    .disposed(by: disposeBag)
```