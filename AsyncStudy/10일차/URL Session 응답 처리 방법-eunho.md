# URL Session 응답 처리 방법

---

<aside>
💡 URLSession 작업 순서 URLSession 인스턴스 생성 → 데이터 작업 생성 → 응답처리 → 작업 시작

</aside>

- 응답처리 : 데이터 작업의 completionHandler 클로저를 사용하여 서버의 응답을 처리한다. completionHandler 클로저는 세 개의 매개변수(data, reponse, error)를 받는다.
- data : 서버에서 수신한 데이터. 데이터는 Data 형식으로 제공된다.
- response : 서버의 응답. HTTPURLResponse의 인스턴스로 제공된다. 응답에는 상태 코드, 헤더 및 기타 정보가 포함된다.
- error : 발생한 오류가 있는 경우 오류 정보를 포함한다.

```swift
let task = session.dataTask(with: urlRequest) { (data, response, error) in
    if let error = error {
        // 오류 처리하는 코드
        return
    }
    
    guard let httpResponse = response as? HTTPURLResponse else {
        // 잘못된 응답 처리
        return
    }
    
    if httpResponse.statusCode == 200 {
        // 성공적인 응답 처리
        if let responseData = data {
            // 데이터 사용
        }
    } else {
        // 다른 상태 코드 처리
    }
}
```

# HTTP Status Code

---

- 1xx (Informational) : 요청을 받았고 처리 중인 상태
- 2xx (Success) : 요청이 성공적으로 처리 된 상태
- 3xx (Redirection) : 추가 동작이 필요함을 나타내는 상태
- 4xx (Client Error) : 클라이언트의 요청이 잘못되었거나 처리할 수 없음을 나타내는 상태
- 5xx (Server Error) : 서버에서 요청을 처리하는 동안 오류가 발생했음을 나타내는 상태