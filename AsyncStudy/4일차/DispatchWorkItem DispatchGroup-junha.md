# DispatchWorkItem DispatchGroup

---

# **DispatchWorkItem**

- DispatchWorkItem은 GCD에서 작업을 캡술화하는 클래스입니다.
- 직접적인 상속 구조가 없습니다.
- **`DispatchWorkItem`**: 작업을 생성하는 초기화 메서드입니다.
- 클로저를 인자로 받아서 DispatchWorkItem 객체를 생성합니다.

```swift
let workItem = DispatchWorkItem {
    print("작업 실행")
}
```

- **`perform()`**: 작업을 실행합니다. 생성한 DispatchWorkItem 객체에 대해 **`perform()`** 메서드를 호출하여 작업을 실행할 수 있습니다.

```swift
workItem.perform()
```

- **`cancel()`**: 작업을 취소합니다. 작업을 취소하면 해당 작업은 실행되지 않습니다.

```swift
workItem.cancel()
```

- **`notify(queue:execute:)`**: 작업이 완료되면 지정된 큐에서 클로저를 실행합니다. 다른 작업을 기다리고 있는 동안에 사용할 수 있습니다.

```swift
workItem.notify(queue: DispatchQueue.main) {
    print("작업 완료")
}
```

# **DispatchGroup**

```swift
class DispatchGroup: DispatchObject
```

- 여러 테스크들을 그룹으로 묶어서 동시에 수행하고자할 때 사용
- 하나의 `task`를 `{ }` 를 이용해 block을 정의 하고 block을 그룹에 참가 시킨다.
- 테스크들의 세트/묶음을 `group` 이라고 한다.
- 그룹안데 work item들이 수행을 끝마치면 그룹은 completion handler를 수랭한다.
- task들이 수행을 끝마칠때까지 동기적으로 기다려줄 수 있다.
- 요약: DispatchGroup은 여러 작업을 그룹화한다.

## 코드 사용 방법

1. **`enter()`**: 작업 그룹에 진입한다.
- 그룹에 속하는 작업을 시작하기 전에 **`enter()`** 메서드를 호출하여 그룹에 작업이 추가될 것임을 알린다.
- 해당 그룹에 block이 들어갔다고 알립니다.
- 파라미터로 group을 받는데, dispatch group을 업데이트하기 위해 사용되고 nil이 올 수 업습니다.

```swift
group.enter()
```

1. **`leave()`**: 작업 그룹에서 빠져나온다.
- 작업이 완료되었을 때  **`enter()`**와 짝을 이루는 **`leave()`** 메서드를 호출하여 그룹에서 작업이 완료되었음을 알린다.
- 그룹 안에서 수행이 끝난 블록을 명시적으로 나타냅니다.
- enter와 똑같이 nil이 올 수 없습니다.

```swift
group.leave()
```

1. **`notify(queue:execute:)`**: 그룹 내의 모든 작업이 완료되면 지정된 큐에서 클로저를 실행한다
- 모든 작업이 완료된 후에 실행되어야 할 작업을 지정할 수 있다.
- Dispatch Group에 들어있는 task가 0이 되었을 때 실행되는 함수
    - qos: 해당 work가 수앻될 서비스의 퀄리티를 정한다.
    - flags: work가 어떻게 수행될 것인지에 대한 옵션을 지정
    - queue: 그룹의 수행이 모두 완료되었을 때 알림받는 큐
    - work: 그룹의 수행이 완료되었을 때 dispatch queue에 수행될 work

```swift
group.notify(queue: DispatchQueue.main) {
    print("모든 작업 완료")
}
```

아래는 DispatchWorkItem과 DispatchGroup를 같이 사용한 예제 입니다.

```swift
let group = DispatchGroup()
let queue = DispatchQueue.global()

let workItem1 = DispatchWorkItem {
    print("첫 번째 작업 실행")
}

let workItem2 = DispatchWorkItem {
    print("두 번째 작업 실행")
}

queue.async(group: group, execute: workItem1)
queue.async(group: group, execute: workItem2)

group.notify(queue: DispatchQueue.main) {
    print("모든 작업 완료")
}
```