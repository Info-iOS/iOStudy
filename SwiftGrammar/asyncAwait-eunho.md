# async await

---

# 비동기(async)

---

```swift
func asyncTest() async throws -> String {
	//code
}
```

이러식으로 함수명을 적어주고 옆에 async 키워드를 적어주면 비동기로 처리된다는 것을 의미. throws를 붙여야 할 때는 async throws를 사용하면 된다.

# await

---

```swift
let string: String = try await asyncTest()
```

이런식으로 작성하면 asyncTest( )가 완료될 때까지 해당 임무의 작업은 일시 정지 된다.

# Dispatch Queues

---

- Grand Central Dispatch (GCD) dispatch queues는 task 수행을 위한 강력한 도구

```swift
DispatchQueue.main.sync {
    //code
}
```

위 코드는 main dispatch queue 직렬 방식이라 하나의 임무가 끝나야지 다음 임무를 할 수 있다.

```swift
DispatchQueue.global.async {
    //code

}
```

위 코드는 동시 방식으로서 하나 이상의 임무를 실행하지만 임무는 순서대로 계속 시작한다.

# 예제코드

---

```swift
func asyncTest() async throws -> String { //3초를 기다리다가 sleep 끝을 반환하는 함수
    try await Task.sleep(nanoseconds: 3_000_000_000) //3초
    return "sleep 끝"
}

Task {
    let string: String = try await asyncTest()
    print(string)
}
//이렇게 짜면 3초뒤에 sleep 끝 메세지가 작성 될 것이다.
```

3초동안 프로그램이 멈추는 것은 큰 일 이기때문에 반드시 비동기적으로 처리해야함. 함수명 옆에 async를  붙여주고 에러를 대비해 throws도 붙여준다.

await코드에서 try를 붙여준 까닭은 throws 때문에 붙인 것

### Task 주의점

---

```swift
// Task 주의점
print("Before Task")
Task {
    let string: String = try await asyncTest()
    print(string)
}
print("After Task")
```

이 코드에서 순서는 Before Task → After Task → 3초 대기 → sleep 끝이다.