q# URLSession 에러 처리

---

# URLSessionTaskDelegate

---

1. URLSessionTaskDelegate를 포함한 URLSessionDelegate 프로토콜을 채택합니다.
    
    ```swift
    class MyDelegate: NSObject, URLSessionTaskDelegate {
        // URLSessionTaskDelegate 메서드 구현
    }
    ```
    
2. delegate 설정 : URLSession 인스턴스의 delegate 속성을 설정하여 작업에 대한 응답 및 에러를 처리할 대리자(delegate)를 지정
    
    ```swift
    let session = URLSession(configuration: URLSessionConfiguration.default, delegate: myDelegate, delegateQueue: nil)
    ```
    
3. URLSessionTaskDelegate 메서드 구현 : URLSessionTaskDelegate 프로토콜의 메서드를 구현하여 에러를 처리한다.
    1. urlSessio함수 작업이 완료되었을 때 호출된다. 오류가 발생한 경우와 성공한 경우를 if let을 사용하여  둘다 한 메소드에서 처리할 수 있다.

```swift
func urlSession(_ session: URLSession, task: URLSessionTask, didCompleteWithError error: Error?) {
    if let error = error {
        // 에러 처리
    } else {
        // 성공적인 완료 처리
    }
}
```

1. NSError를 통한 에러 처리 : URLSession에서 발생한 에러는 NSError 형태로 제공될 수 있다. 에러를 처리할 때, NSError를 활용하여 오류 유형 및 관련 정보에 접근 가능

```swift
func urlSession(_ session: URLSession, task: URLSessionTask, didCompleteWithError error: Error?) {
    if let error = error as NSError? {
        // 에러 유형에 따라 처리
        if error.domain == NSURLErrorDomain {
            // 네트워크 에러 처리
            if error.code == NSURLErrorTimedOut {
                // 타임아웃 에러 처리
            } else if error.code == NSURLErrorNotConnectedToInternet {
                // 인터넷 연결 없음 에러 처리
            }
            // 추가적인 네트워크 에러 처리
        } else {
            // 기타 에러 처리
        }
    } else {
        // 성공적인 완료 처리
    }
}
```
