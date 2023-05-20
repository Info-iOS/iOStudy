# GCD(Grand Central Dispatch)

---

- GCD는 멀티 코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술이다.
- Task를 Dispatch Queue에 추가하기만 하면 GCD가 알아서 Task를 적절한 Thread에 배분하고 관리해준다.

# Dispatch Queue

---

- Task의 실행을 관리하는 객체로 앱의 Thread에서 Task를 동기적, 비동기적으로 실행하게 도와준다.
- GCD와 비슷한 이유는 GCD에서 사용하는 Queue이기 때문이다.

```swift
DispatchQueue.{Queue 종류}(.{qos 옵션}).{sync/async} {
    //순차적으로 진행되는 하나의 작업 단위
}
```

위 와 같이 DeispatchQueue의 종류와 처리 방식을 설정할 수 있다.

```swift
//예시
DispatchQueue.global().async {
	print("Eunho")
}
```

순서가 중요하지 않을 것들은 글로벌 큐로 보내면 된다

# Qos 종류

---

- ****userInteractive : 사용자와 직접 상호작용 하는 작업****
- ****userInitiated : 클릭할 때 작업을 수행하는 것과 같은 즉각적인 결과가 필요한 작업 (userInteractive 보다는 조금 오래걸림)****
- default : 일반적인 작업.
- background : 사용자가 직접적으로 인지하지 않는 시간이 덜 중요한 작업
- ****unspecified : 정보가 없음을 나타냄.****

# Custom Queue

---

- default 로 Serial 특성을 가진 Queue. 하지만 Concurrent 로 설정 가능하다.

```swift
//생성할때 label을 붙이면 커스텀이 된다.
let customSerialQueue = DispatchQueue(label: "Eunho")

//Concurrent 설정할 때 
let customSerialQueue = DispatchQueue(label: "Eunho", attributes: .concurrent)
//위와 같이 qos설정을 안해주면 알아서 추론함 

//qos 설정도 할 경우
let customSerialQueue = DispatchQueue(label: "Eunho", attributes: .concurrent, attributes: .concurrent)
```