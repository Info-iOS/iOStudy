# 세마포어(GCD)

---

Semaphore???

- 동시에 하나의 자원에 접근을 방지하게 할 수 있는 비동기 문제를 해결하기 위해 사용
- 여러 프로세스가 데이터를 공유하면서 작업을 수행할 때, 동시에 접근하면 안되는 자원을 동시에 접근할 수 없도록 막는 플래그
- ~~운체때 왜 배우나 했는데 사용할 줄은 몰랐다~~
- 요약: Semaphore는 공유자원에 진입할 수 있는 허용 개수

운영체제에서 Semaphore는 어떻게 썼을까?

- 음… 일단 확실하게 생각하는 것은 임계 구역을 들어갈 때 P!!!라고 소리치고 나올 떄 V!!!라고 소리치는 것은 생각난다.
- 사전적인 뜻으로는 정수값을 갖는 변수이고 자원의 개수를 의미합니다.

```swift
var semaphore = 3

semaphore = semaphore - 1 // 2
semaphore = semaphore - 1 // 1
semaphore = semaphore - 1 // 0

//0일 때는 대기 상태
```

Semaphore 연산자

- wait()
    - semaphore의 값이 현재 0보다 크면 -1
    - 카운팅 값이 0이되면 값이 증가할 때까지 대기
    - 프로세스가 자원을 사용할테니 기다리라는 의미로 사용
- signal()
    - semaphore의 값을 +1
    - 프로세스가 자원을 사용하고 나왔다는 신호를 의미로 사용
    
- 추가적으로
    - semaphore의 값이 0이되면 임계영역에 들어가지 못하고 대기한다
    - 만약 0 미만이 되면 임계영역으로 쓰고 있는 프로세스, 스레드가 반납하기 전까지 대기한다.

**DispatchSemaphore**

- swift에서는 **DispatchSemaphore라는 녀셕이 있다**

어떤 일들을 할까?

작업 개수 제한

- **DispatchSemaphore를 이용해서 작업 개수를 제한 할 수 있다.**

```swift
for i in 1...8 {
		semaphore.wait() // 감소
		DispatchQueue.global().async() {

				print("공유자원 접근")
				sleep(3)
				print("공유자원 접근 종료")
				sleep(3)
				semaphore.signal() //semaphore 증가
		}
}
```

- 실행

```swift
공유자원 접근
공유자원 접근
공유자원 접근 종료
공유자원 접근 종료
공유자원 접근
공유자원 접근
공유자원 접근 종료
공유자원 접근 종료
공유자원 접근
공유자원 접근
공유자원 접근 종료
공유자원 접근 종료
공유자원 접근
```

- 작업 수가 2개씩 나온 이유는 작업 수가 2개이기 때문입니다.

두 쓰레드의 특정 이벤트 완료 상태 동기화

- DispatchSemaphor는 두 가지 방식으로 사용가능합니다
    - 두 쓰레드가 특정 이벤트의 완료 상태를 동기화 하는 것이 유용하다.
        - 쓰레드 A는 작용 A 실행 중
        - 쓰레드 B는 작업 A가 끝난 후에 무언가를 수행
        - 위 방식을 원한다면 semaphore 초기값을 0으로 설정한다
    
    ```swift
    let semaphore = DispatchSemaphore(value: 0)
    
    print("task A가 기다름")
    
    // 다른 스레드에서 task A 실행
    DispatchQueue.global(qos: .background).async {
    
        print("task A 시작!")
        print("task A 진행중..")
        print("task A 끝!")
    
        semaphore.signal() // 끝이라고 알려줌
    }
    
    // 이때 task A는 0인 상태가 아니라 task A 종료까지 block
    semaphore.wait()        
    print("task A 완료됨")
    ```