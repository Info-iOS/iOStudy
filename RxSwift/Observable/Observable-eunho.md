# Observable

---

- Rx의 심장
- observable = observable sequence = squence 이 단어들은 모두 같은말. (모두 asynchrous비동기 이다.)
- Observable 들은 일정 기간 동안 계속해서 이벤트를 생성하며, 이러한 과정을 emitting(방출)이라고 표현한다.
- 각각의 이벤트들은 숫자나 커스텀한 인스턴스 등과 같은 값을 가질 수 있으며, 탭과 같은 제스처를 인식할 수도 있다.

## Observable의 생명주기

---

- next, completed, error로 구성되어 있다.
- next 이벤트를 통해 각각의 요소들을 방출함.
- ex) tap 이벤트를 방출한 뒤 이벤트들이 다 방출되면 완전 종료
- completed 이벤트 발생
- 에러를 발생시켜 error를 통해 종료 시킨다.
- on disappeat, dispose 메모리 누수

```swift
// 이러한 이벤트들은 enum 케이스로 표현한다.
public enum Event<Element> {
	case next(Element)
// next 이벤트는 어떠한 Element 인스턴스를 가지고 있는 것을 확인할 수 있다.
	
	case error(Swift.Error)
// error 이벤트는 Swift.Error 인스턴스를 가진다.

	case completed
// completed 이벤트는 아무런 인스턴스를 가지지 않고 단순히 이벤트를 종료시킨다.
}
		
```

## Observable 생성

---

```swift
example(of: "just, of, from") {
     // 1
     let one = 1
     let two = 2
     let three = 3
     
     // 2
     let observable:Observable<Int> = Observable<Int>.just(one)
 }
```

## Observable 구독

---

```swift
let observer = NotificationCenter.default.addObserver(
	  forName: .UIKeyboardDidChangeFrame,
	 	object: nil,
	  queue: nil
	 ) { notification in
	 	// Handle receiving notification
	}
```

- RxSwift Observabl을 구독하는 것은 상기 방식과 비슷하다.
- subsribe()를 사용함

```swift
observable.subscribe { event in
 	if let element = event.element {
 		print(element)
 	}
 }
```

```swift
observable.subscribe(onNext: { (element) in
 	print(element)
 })
```

- 상기의 코드를 위와 같이 변경할 수 있음

## .empty()

---

- empty 연산자를 통해 .completed 이벤트만 방출함
- 즉시 종료할 수 있는 Observable을 리턴하고 싶을 때
- 의도적으로 0개의 값을 가지는 Observable을 리턴하고 싶을 때

## .never()

---

- empty와 반대로 never 연산자가 있음

```swift
example(of: "never") {
     let observable = Observable<Any>.never()
     
     observable
         .subscribe(
             onNext: { (element) in
                 print(element)
         },
             onCompleted: {
                 print("Completed")
         }
     )
 }
```

- 위와 같이 코딩하면 Completed 조차 프린트 되지 않는다.

## .range()

---

```swift
example(of: "range") {
     
     //1
     let observable = Observable<Int>.range(start: 1, count: 10)
     
     observable
         .subscribe(onNext: { (i) in
             
             //2
             let n = Double(i)
             let fibonacci = Int(((pow(1.61803, n) - pow(0.61803, n)) / 2.23606).rounded())
             print(fibonacci)
         })
 }
```

1. range 연산자를 이용해서 start 부터 count 크기 만큼의 값을 갖는 Observable을 생성한다.
2. 각각 방출된 요소에 대한 n번째 피보나치 숫자를 계산하고 출력한다.

## .dispose()

---

```swift
example(of: "dispose") {
     
     // 1
     let observable = Observable.of("A", "B", "C")
     
     // 2
     let subscription = observable.subscribe({ (event) in
         
         // 3
         print(event)
     })
     
     subscription.dispose()
 }
```

1. Observable 생성
2. 구독과 Disposable을 리턴하도록 만듬
3. 출력
4. dispose는 구독을 취소하거나 dispose 한뒤에는 이벤트 방출이 정지된다

## .disposeBag

---

```swift
example(of: "DisposeBag") {
     
     // 1
     let disposeBag = DisposeBag()
     
     // 2
     Observable.of("A", "B", "C")
         .subscribe{ // 3
             print($0)
         }
         .disposed(by: disposeBag) // 4
 }
```

- 각각의 구독에 대해서 일일히 관리하는 것이 효율적이지 못하여 사용한다.
1. subscribe로 부터 방출된 리턴 값을 disposeBag에 추가한다.