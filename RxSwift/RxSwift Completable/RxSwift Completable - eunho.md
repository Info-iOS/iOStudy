# RxSwift Completable

---

> Completable
> 

Completable은 변화무쌍한 Observable이다. complete 하거나, error를 방출하고, 아무 요소도 방출하지 않는 것을 보장한다.

- 제로 요소 방출
- 완료 이벤트 또는 에러 방출
- 부수작용을 공유하지 않는다.

Completable은 완료에 따른 요소에 신경쓰지 않은 경우 사용하면 유용하다. 요소를 내보낼수 없는 경우 Observable을 사용하여 비교할 수 있다.

![Untitled](RxSwift%20Completable%205bd2ae57372648ae945bdfb020a55c91/Untitled.png)

completable 코드예제

```swift
let completable = Completable.create { observer in
        observer(.completed) // 또는 observer(.error())
        return Disposables.create()
    }

override func viewDidLoad() {
        super.viewDidLoad()
        
        completable
            .debug("debug2>")
            .subscribe()
            .disposed(by: disposeBag)
        // subscribed > completed > isDisposed
    }
```

## Observable과 Single, Completable 차이

- Single과 Completable은 한 번 subscribe하고 이벤트가 방출되면 바로 dispose되어 1회성으로 사용할 때 사용
    - 주로 API 통신 할 때 Single과 Completable을 활용한다.

observable을 subsricbe할 때 next 이벤트가 발생해도 dispose 되지 않는다.

## 요약

- 계속 observe하여 이벤트가 발생할 때마다 특정 작업을 처리해야하는 경우 (상태 바인딩 후 UI 변경하는 경우)
    - Observable 사용

- 필요할때마다 호출하여 특정 작업을 하고싶은 경우 (API 통신, 등등)
    - Single이나 Completable 사용

- Single ㄱ