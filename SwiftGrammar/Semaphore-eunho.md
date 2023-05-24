# Semaphore

---

- 동시에 하나의 자원에 접근을 방지하게 할 수 있는 비동기 문제를 해결하는데 사용
- 한번에 여러 데이터를 공유하면서 작업을할 때 동시에 접근하는 안되는 자원을 동시에 접근할 수 없도록 막는 플래그 기능이다.

### Semaphore 연산자

- wait()
    - Semaphore의 값이 0보다 크면 값이 -1
    - 0이 되면 값이 증가할 때까지 대기
    - 프로세서가 자원을 사용할테니 기다리라는 의미
- signal()
    - Semaphore의 값을 +1
    - 프로세서가 자원을 사용하고 나왔다는 신호를 의미

```swift
let semaphore = DispatchSemaphore(value: 1) // 공유자원 최대 1개
var updateSomeProperty = 0 // 사용될 프로퍼티

(0...3).forEach { _ in
  self.semaphore.wait()
  self.addCountAfterSeconds()
  self.semaphore.signal()
}

var count = 0
private func addCountAfterSeconds() {
  DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    self.count += 1
  }
}
```

스위프트 내부적으로 wait() 와 signal()의 동작 프로세스

semaphore값이 0인 상태에서 다른 작업이 들어오면 현재 진행중인 큐에다가 넣어놓고 큐를 대기시키는 것