# async, await

---

## async, await는 무엇인가?

- 프로그래밍에서 비동기 작업을 처리하는 패턴
- 비동기 작업은 작업이 완료될 때까지 기다리지 않고 다른 작업을 동시에 실행
- 네트워크 요청, 파일 다운로드, 긴 계산을 할 때 좋습니다.

## async, await의 특징

- 동기적이고 유사한 코드를 만들 수 있음
- **비동기 작업의 완료를 기다림**
    - **`await`** 를 사용하여 비동기 작업의 완료를 기다리고, 작업이 완료되면 결과를 반환
- 오류처리
    - **`try`**/**`catch`**를 사용하여 처리할 수 있다.

## async, await 언제 왔는가?

- Swift 5.5

## async?

- 비동기 함수로 선언

```swift
func fetchData() async -> Data {
    let url = URL(string: "https://api.junha.com/data")!
    let (data, _) = try! await URLSession.shared.data(from: url)
    return data
}
```

```swift
async {
    do {
        let data = try await fetchData()
        // 비동기 작업 완료 후 데이터 처리
    } catch {
        // 에러 처리
    }
}
```

## await?

- 비동기 작업의 완료를 기다리고 결과를 반환
- 사용하면 비동기 작업이 완료될 때까지 코드의 실행이 일시 중단되고, 작업이 완료되면 해당 결과를 반환

```swift
func fetchData() async -> Data {
    let url = URL(string: "https://api.junha.com/data")!
    let (data, _) = try! await URLSession.shared.data(from: url)
    return data
}
```

```swift
async {
    do {
        let data = try await fetchData()
        // 비동기 작업이 완료된 후 데이터를 사용하여 처리
        print("데이터 넣기: \(data)")
    } catch {
        // 에러 처리
    }
}
```

## async, await의 핵심 원리

- 이벤트 루프와 코루틴
- **`await`** 를 만나면 현재 코루틴의 실행을 일시 중단하고 다른 코루틴으로 전환
- 작업이 완료되면 해당 코루틴에서 중단한 위치에서 실행을 재개합니다.

### 코루틴?

- 비동기적인 작업을 동기적으로 다룰 수 있도록 하는 프로그래밍 개념
- 실행 중인 함수의 실행을 중지하고 나중에 재개할 수 있는 작은 실행 단위
- 코루틴은 함수의 실행을 중지하고 다른 작업을 수행한 후에 다시 해당 위치에서 실행을 재개 가능
- 코루틴은 비동기 작업을 처리하는 데 매우 유용

### 이벤트 루프

- 프로그램이 이벤트와 작업을 관리하고 처리하는 무한 루프
- 비동기적인 이벤트 기반 프로그래밍에서 사용
- 이벤트를 감지하고 처리하는 역할
- 프로그램이 비동기 작업을 조율하고 응답성을 유지하는 데 중요한 역할