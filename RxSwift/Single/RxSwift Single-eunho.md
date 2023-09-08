# RxSwift Single

---

> Traits
> 

Traits는  모든 경계에서 사용할 수 있는 원시적인 Observable과 비교할때 인터페이스 경계에서 observable 프로퍼티를 전달하고 보장하며, 문법적으로 도 더 쉽고 구체적인 사용을 할 수 있다.

Traits는 struct 형태로 일기전용 Observable sequence property와 함께 랩필 되어있다.

```swift
struct Single<Element> {
	let source: Observable<Element>
}

struct Single<Element> {
	let source: Observable<Element>
}
```

> Single
> 

Single은 Observable의 변형으로 일련의 요소를 방출하는 대신 항상 단일 요소 또는 오류를 방출하도록 보장한다.

- 정확히 하나의 요소 또는 error를 방출한다.
- 부수작용을 공유하지 않는다.

Single의 사용 예시로는 응답, 오류만 반환할 수 있는 HTTP 요청을 수행하는데 사용되지만 단일요소를 사용하여 무한 스트림 요소가 아닌 단일 요소만 관리하는 경우에 사용할 수 있다.

![Untitled](RxSwift%20Single%205b35cba17a7f44f283f64afc942453fb/Untitled.png)

어떠한 데이터를 받을 때 성공 아니면 에러를 내보낸다.

Single 코드 예제

```swift
let single = Single<Int>.create { observer in
        observer(.success(1)) // 또는 observer(.error())
        return Disposables.create()
    }

override func viewDidLoad() {
        super.viewDidLoad()
        
        single
            .debug("debug1>")
            .subscribe()
            .disposed(by: disposeBag)
        // subscribed > next(1) > completed > isDisposed
        
    }
```

switch case를 사용하여 HTTP 요청 성공 시와 실패에 따른 처리를 사용할 수 있다.

```swift
getRepo("ReactiveX/RxSwift")
    .subscribe { event in
        switch event {
            case .success(let json):
                print("JSON: ", json)
            case .error(let error):
                print("Error: ", error)
        }
    }
    .disposed(by: disposeBag)
```

subscribe(onSuccess:onError:)을 통하여 아래처럴 사용할 수 있다.

```swift
getRepo("ReactiveX/RxSwift")
    .subscribe(onSuccess: { json in
                   print("JSON: ", json)
               },
               onError: { error in
                   print("Error: ", error)
               })
    .disposed(by: disposeBag)
```