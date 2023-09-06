# Observable

---

-Rx의 심장

- Observable = Observable Sequence = Sequence
- 비동기적
- Observable 들은 일정한 기간 동안 계속해서 이벤트를 생성(emiting(방출))
- marble diagram = 시간의 흐름에 따라 표시함

marble duagran = 

[RxMarbles: Interactive diagrams of Rx Observables](https://rxmarbles.com/)

## Observable 생명주기

1. 어떤 구성요소를 가진 `next` 이벤트를 가지는 `next` 이벤트를 계속 방출할 수 있다
2. `error` 이벤트를 방출해서 완정히 종류할 수 있다
3. `complete` 이벤트를 방출하여서 완전히 종료 시킬 수 있다

 

## Observable 사용법

```swift
Observable<타입>
```

선택적으로 `<>`를 이용해서 어떤 형태로 방출 할 것인지 타입을 정할 수 있습니다

## Observable.just()

```swift
Observable<Int>.just(1)
```

`just`는 하나의 요소를 포함하여 방출하는 단순한 observable

## Observable.Of()

```swift
Observable<Int>.of(1, 2, 3, 4, 5)
//순차적으로 볼 수 있는 observable Sequence
```

`Of`는 다양한 요소를 포함하여 방출하여 하나이상의 이벤트를 넣을 수 있다

```swift
Observable.of([1, 2, 3, 4, 5])
```

observable은 타입 추론을 통하기 떄문에 Array 전체를 넣으면 하나의 Array를 내뿜는 Observable Sequence가 완성된다 떄문에 하나의 Array를 내뿜어서 of가 아닌 just를 사용해도 코드이 문제가 발생하지 않는다

## Observable.From()

```swift
Observable.From([1, 2, 3, 4, 5])
```

`From`을 사용하면 `Array` 안에 있는 값을 순차적으로 하나씩 보여주기 때문에 `Array` 안에 있는 값을 하나 하나씩 보여줘야하는 상황이 있다면 `From`을 사용해야합니다

// 하지만 from 연산자는 오직 Array만 취할 수 있다

그래서 의문점! 그럼 observable은 이렇게만 하면 이벤트가 발생하는가? 아니다 그랬으면 내가 이걸 하나하나 풀지 않았을 것이다. 지금 우리가 한 Observable은 Sequence 정의만 했을 뿐 다른 행동을 취하지 않았다

때문에 여기서 알 수 있는 점은 Observable은 구독되기 전까지는 정의 만했을 뿐 구독이 되어야 이벤트를 발생 할 수 있다 지금 부터는 구독을 시켜주는 subscribe를 알아봐 보자

## subscribe(onNext: {})

```swift
Observable<Int>.just(1)
      .subscribe(onNext: {
       print($0)
})
```

`subscribe`를 통해 구독된 것은 `onNext`를 통해서 출력된다고 생각하면 편 할 것 같다 위 코드는 우리가 1을 넣어 주었기 때문에 출력 결과는 1이 나올 것이다

그러면 또 의문점 `onNext` 굳이 써주어야 할까?

## subscribe{}

```swift
Observable.of(1, 2, 3)
    .subscribe {
     print($0)
}

//next(1)
//next(2)
//next(3)
//completed
```

위와 같이 코드를 출력하면 밑에 주석에서 알 수 있 듯이 `next`, `completed` 가 나오는 것을 알 수 있다 지금까지는 `onNext`를 사용하여서 우리가 원하는 vlaue값만 딱! 확인을 했지만 `subscribe`만을 사용하면 코드의 작동 결과를 알 수 있다 `next`를 통해서 1, 2, 3이 출력됬고 `completed`를 통해서 끝났다라는 사실을 알 수 있다

```swift
Observable.of(1, 2, 3)
    .subscribe {
	if let element = $0.element {
       	    print(element)
	}
}
```

if let을 사용하면 어떻게 될까? 하는 궁금증에 사용해보았다 그랬더니 `onNext`를 사용한 값과 동일 결과가 나왔다 

## Observable.empty()

```swift
Observable.empty()
    .subscribe {
        print($0)
    }
```

`empty`는 무엇일까? `empty`는 아무런 값을 가지지 않는 요소를 만들떄 사용한다 떄문에 위 코드를 사용하면 아무런 결과 값이 없을 것이다

하지만

```swift
Observable<Void>.empty()
    .subscribe {
        print($0)
    }

//Observable<Void>.empty()
//    .subscribe(onNext: {
//
//}, 
//	onComplect: {
//		print("completed")
//})
```

만약에 타입을 명시해주면 어떻게 될까? 타입을 명시하게되면 “completed”라는 결과가 뜰 것이다 이유는

그전에는 `empty`는 타입을 추론 할 것이 없어서 그냥 종료됬지다 때문에 `empty`를 사용할 때는 타입을 명시를 해주어야 한다 그러면 이 쓸때 없어보이는 것을 언제 쓸까? 찾아보니까 주로 즉시 종료 할 수 있는 Observable을 return하고 싶을 때 또는 의도적으로 0개의 Observable을 return 하고 싶을 떄 사용한다고 하네요

## Observable.never()

```swift
Observable.never()
   .subscribe {
	onNext: {
       	   print($0)
	},
	onComplect: {
      	   print("Completed")
      }
}
```

`never`의 신기한 점은 아무것도 안떠 왜 안뜨지? 내가 타입 추론을 안해서 안뜨나? Completed도 안뜨네?

```swift
Observable<Void>.never()
   .subscribe {
	onNext: {
    	   print($0)
	},
	onComplect: {
	   print("Completed")
     }
}
```

그래도 안떠 이상하다 그러면 `never`는 정말 아무 것도 안뜨는 것인가? `never`를 띄우는 방법이 있다 

밑에 코드를 확인 해보자

```swift
Observable<Void>.never()
   .debug("never")
   .subscribe {
	onNext: {
	   print($0)
	},
	onComplect: {
	   print("Completed")
	}
}

//출력 결과 = never -> subscribed
```

`debug`를 적어주면 밑에 출력 결과 처럼 ‘구독은 됐어’ 라고 뜨는 것을 볼 수 있다 그렀다 바로 `naver`는 작동은 하지만 아무런 결과를 내뱉지 안는다

## Observable.range(start: _ , count: _)

```swift
Observable.range(start: 1, count: 9)
   .subscribe(onNext: {
	   print("2 * \($0) = \(2*$0)
	})
```

약간 for문 같은 느낌이 나는데 `range`는 start 값부터 시작해서 count를 하나씩 올려서 값을 하나씩 올리다가 count값이 되면 종료하는 식이다

//구구단 만들기 최적화된 ㅋㅋ

## dispose

지금까지 우리는 `subscribe`을 통해서 이벤트를 방출했지만 지금부터는 구독을 수동적으로 취소 하여서 수동적으로 Observable을 종료 시킬 수 있는 `dispose`를 알아보자

```swift
Observable.of(1, 2, 3)
   .subscribe {
    print($0)
}
.dispose()

//next(1)
//next(2)
//next(3)
//completed
```

 지금 우리가 쓰는 코드는 `dispose`를 하지 않아도 끝났다고 `completed`가 뜨지만 요소가 아무래도 3개다 보니까 `completed`가 뜬다 하지만 우리가 실무에서 ViewController가 띄어졌을 경우 1초씩 늘어나는 코드를 작성했으면 아무래도 자! 여기서 끈어 하는 명령을 해줘야 겠죠? 그럴떄 바로 `dispose`를 사용해서 구독을 해지해주면 `subscribe`를 끈어주는 것 입니다 대신 일일이 하나씩 추가해서 방출을 해야하는데 귀찮겠죠 그래서 밑을 확인 하시면 됩니다

## disposeBag

```swift
var disposeBag = DisposeBag()

Observable.of(1, 2, 3)
   .subscribe {
    print($0)
}
.disposed(by: disposeBag)

```

`Disposable`에는 `disposed(by:)` 라는 메소드가 존재 합니다. 파라미터에 `disposeBag` 객체가 들어가고 bag에 가신이 들어가는 형식이죠 모든 구독자(Observable) 안에 `disposeBag`에 등록되고 `disposeBag`가 해지되면 현재까지 등록된 모든 `disposeBag`는 모든 값을 `dispose` 시키는 형식이죠

// 근데 다른 글을 찾아보다가 본 꿀팁인데요 let이 아니라 var 인 것을 볼 수 있죠 이유는 disposeBag이 해제 되면 모든 disposable이 dispose가 되는 원리를 사용해서 subscribe 도중에 disposable를 초기화 시키고 싶다면 그냥 (disposeBag = DisposeBag() ) 으로 초가화 시킬 수 있다는 꿀팁 ㄷㄷ

그럼 `dispose`를 안하면 어떻게 될까요 보통은 swift에서 하세요 라고 경고를 주는 것이 보통이지만 만약 하지 않으면 메모리 누수가 발생 할 수 있다고 하네요

// 메모리 누수란 무엇일까?: 메모리 누수 현상은 프로그램이 필요하지 않은 메모리를 계속 점유하고 있는 현상을 말합니다.

## Observable.create

```swift
Observable.create { observer -> Disposable in
   observer.onNext(1) //observer.on(.next(1)) 동일 하다
   observer.onCompleted()
   observer.on(.next(2))
   return Disposables.create()
}
.subscribe {
   print($0)
}
.disposed(by: disposeBag)
```

`create`는 (AnyObserver) -> Disposable 타입의 클로저입니다.(observer → Disposable)부분

1. AnyObserver는 해당 Observable을 구독하게 될 Observer라고 생각하면 됩니다. Observer의 on 메소드를 통해 해당 Observer에 이벤트를 전달하게 됩니다.

2. Disposable은 해당 Observable과 연결될 Disposable입니다. 이 Observable은 명시적으로 `Dispose` 메시지를 받거나, `DisposeBag`에 담겨 있다 Bag이 해제될 때 메모리 해제가 일어나게 됩니다.

그리고 끝날때는 무조건 return Disposables.create() 를 만들어서 내보내주어야 합니다

그리고 속았을 분들은 없겠지만 onNext(1) 다음에 onCompleted를 해주면 onCompleted 뜻 자체가 끝낸다는 의미이기 때문에 onNext(2)는 실행되지 않는다는 것 누구나 다 알고 있었겠죠? 큼큼,,

떄문에 출력하면 1 출력하고 끝나는 것을 알 수 있습니다

```swift
enum MyError: Error {
    case anError
}

Observable<Int>.create { observer -> Disposable in
    observer.onNext(1)
    observer.onError(MyError.anError)
    observer.onCompleted()
    observer.onNext(2)
    return Disposables.create()
}
.subscribe(
    onNext: {
        print($0)
    },
    onError: {
        print($0.localizedDescription)
    },
    onCompleted: {
        print("Completed")
    },
    onDisposed: {
        print("Disposed")
    }
)
.disposed(by: disposeBag)
```

요번에는 `error`를 추가 해보았습니다 그리고 `create`에는 `onNext`, `onError`, `onCompleted`, `onDisposed` 라는 4가지 값을 가지고 있는데 설명해보겠습니다

- `onNext`: 우리가 선정한 값을 print 하는데 사용됨
- `onError`: error가 생길경우 사용됨
- `onCompleted`: 끝났음을 표시 할 때 사용됨
- `onDisposed`: `disposed` 할 때 사용됨

자! 그리고 요번에도 역시 미끼를 던졌는데 이제는 실수 하지 않겠죠 출력 결과를 보면 1 출력하고 에러 출력하고 onCompleted가 뜨겠지 그리고 onNext(2)는 실행 안되겠지 헤헤 맞췄다 ㅋㅋ 아뇨 틀렸습니다. onNext(1)까지는 잘 출력되지만 error를 우리가 만들었기 때문에 error가 발생하겠죠 error는 그자리에서 completed가 되기 전에 끝난다는 사실을 알면 좋을 것 같습니다.

그리고 또 궁금한 사실이 있었다 그러면 그냥 `onError`와 `onCompleted`와 `disposed`를 안하면 어떻게되지?

```swift
enum MyError: Error {
    case anError
}

Observable<Int>.create { observer -> Disposable in
    observer.onNext(1)
    observer.onNext(2)
    return Disposables.create()
}
.subscribe(
    onNext: {
        print($0)
    },
    onError: {
        print($0.localizedDescription)
    },
    onCompleted: {
        print("Completed")
    },
    onDisposed: {
        print("Disposed")
    }
)
```

이 경우는 어떻게 될까?

코드를 보시면 onNext 2개만 방출하고 종료하는 것도 없고 끝내겠다는 말도 없으니 계속 구독중이다 이떄 심하게 메모리 낭비가 된다는 사실 떄문에 우리는 `dispose`를 해주어야한다

## Observable.deffered

```swift
Observable.deferred {
    Observable.of(1,2,3)
}
.subscribe {
    print($0)
}
.disposed(by: disposeBag)
```

`deffered`를 사용하면 Observable 안에 Observable을 만들 수 있다

위 코드를 사용하면 observable 안에 있는 1 2 3 의 값들이 나올 것이다

```swift
var upend: Bool = false
let fatory: Observable<String> = Observable.deferred {
    upend = !upend
    
    if upend {
        return Observable.of("👊")
    } else {
        return Observable.of("✋")
    }
}

for _ in 0...3 {
    fatory.subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)
}
```

Observable.deferred는 observable fatory 통해서 할 수 있는 것은 Sequence들을 생성 할 수 있는 연산자다

그럼 `deferred`의 장단점은 무엇일까?

장점은  메모리 관점에서 구독할때 안에 구현부가 메모리에 로드되며 메모리 효율에 좋은 코드를 만들 수 있다

단점은 대부분은 `Deferred`를 사용하지 않으면서 메모리 효율을 내고 싶을때만 사용한다

단점 2번째는 `Deferred`는 구독이되는 시점에 메모리에 Observable을 생성하는 코드가 올라오기 때문에 빠르게 Observable을 구독하여 사용하고 싶은경우 성능에 안좋은 영향을 미칠 수 있음
