# Asnyc (비동기)

- 실행 시간이 다른 작업들과 독립적으로 실행될 수 있도록 하는 프로그래밍 기술이다.
- 즉, 코드가 실행되는 동안 다른 작업을 수행할 수 있도록 하여 앱의 반응성을 향상시키는 것을 의미한다.

---

# async, await

- 이 구문을 사용하면 쉽게 비동기 코드를 작성할 수 있고 가독성과 유지보수성을 높일 수 있다.

⬇️ 파일 다운로드를 비동기적으로 처리하는 코드

```swift
func downloadFileAsync(url: URL) async throws -> Data {
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}
```

위 코드는 파일 다운로드를 비동기적으로 처리하는 코드

이렇게 하면 다운로드가 완료될 때 까지 기다리지 않고도 코드의 실행을 계속할 수 있다.

---

# GCD (Grand Central Dispatch)

- GCD를 사용하면 백그라운드 스레드에서 작업을 수행하고, 결과를 메인 스레드에서 처리할 수 있다.
- 하지만 GCD대신 async/await 구문을 사용하면 더 간결하고 직관적인 코드를 작성할 수 있다.