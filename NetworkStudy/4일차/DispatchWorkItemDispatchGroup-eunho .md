# DispatchWorkItem DispatchGroup

---

# **DispatchWorkItem**

---

- **DispatchWorkItem  클래스는 task의 캡슐화를 하는데 이용한다.**
- task를 세분화하여 만들어 DispatchQueue로 실행을 시킨다.

```swift
//비동기 적인 사용방법 
let myQueue = DispatchQueue(label: "com.nil.queue")
let workItem = DispatchWorkItem {
	print("WorkItem task")
}

myQueue.async(excute: workItem)
print("========")
```

동기적으로 실행할 땐 perform()을 이용해서 더 간단히 실행도 가능하다.

```swift
func perform()
	// 동기적으로 실행할 것
```

```swift
let myQueue = DispatchQueue(label: "com.nil.queue")
let workItem = DispatchWorkItem {
	print("WorkItem task")
}

workItem.perform()
print("========")
```

# **DispatchGroup**

---

- 여러 작업을 그룹에 연결하고 동일한 큐나 다른 큐에서 비동기식을 실행할 수 있다.
- 모든 그룹의 작업이 실행을 종료할 때까지 동기적으로 wait할 수 잇다.

```swift
let myGroup = DispatchGroup()
let serialQueue = DispatchQueue(label: "serialQueue")

let workItem = DispatchWorkItem {
    print(Thread.current)
    for i in 1...10 {
        print("💙", i)
    }
}

serialQueue.async(group: myGroup) {
    print(Thread.current)
    for i in 1...10 {
        print("💚", i)
    }
}

myGroup.notify(queue: .main) {
    print("DONE - 1")
}

serialQueue.async(group: myGroup ,execute: workItem)
```

- 위와 같이 코드를 짜주면 초록색 하트가 번호가 하나씩 증가하면서 나오고 그 다음에 파란색 하트가 나오는 것을 볼 수 있다. 비동기적으로 처리한 것이 먼저 나오는 것을 확인할 수 잇음.
- 만약 파란하트를 출력하는 코드도 비동기적으로 처리해주면 파란색이 쭉 나오고 초록색이 순서대로 나올 것이다.
- 여기서 둘 중 하나를 concurrentQueue를 사용하게 된다면 Serial 큐와 관계없이 실행되서 하나의 색깔이 다 출려되고 나오는 것이 아니라 중간중간 순차없이 출력된다.