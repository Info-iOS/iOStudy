# URLSession 인증 처리

---

- HTTP Basic Authentication은 가장 간단한 URLSession 인증 방법 중 하나이다.
- 서버에 요청을 보낼 때, 인증 정보를 헤더에 추가해서 요청을 보낸다.

```swift
// URLSession을 셍성한다.
let session = URLSession.shared
```

```swift
// URL을 생성한다.
let url = URL(string: "http://www.mukgen.info/meal/today")!
```

```swift
// URLRequest를 생성하고 인증 정보를 추가하는 코드
var request = URLRequest(url: url)
request.httpMethod = "GET" // HTTP 요청 메소드 "GET"
let username = "username" // 이름
let password = "password" // 비밀번호
let loginString = "\(username):\(password)" // 이름:비밀번호
let loginData = loginString.data(using: .utf8)
let base64LoginString = loginData?.base64EncodedString()
request.setValue("Basic \(base64LoginString)", forHTTPHeaderField: "Authorization")
```

```swift
// URLSessionDataTask를 사용하여 데이터를 요청
let task = session.dataTask(with: request) { (data, response, error) in
    if let error = error { // 오류처리 코드
        print("Error: \(error.localizedDescription)")
        return
    }

    // 데이터가 옳은 데이터일 경우 사용한다
    if let data = data {
        let responseData = String(data: data, encoding: .utf8)
        print("Response Data: \(responseData)")
    }
}

// 요청을 시작
task.resume()
```

```swift
//HTTP Basic Authentication을 사용한 인증 전체 코드
let url = URL(string: "https://example.com/api/data")!

var request = URLRequest(url: url)
request.httpMethod = "GET"
let username = "username"
let password = "password"
let loginString = "\(username):\(password)"
let loginData = loginString.data(using: .utf8)
let base64LoginString = loginData?.base64EncodedString()
request.setValue("Basic \(base64LoginString)", forHTTPHeaderField: "Authorization")

let task = session.dataTask(with: request) { (data, response, error) in
    if let error = error {
        print("Error: \(error.localizedDescription)")
        return
    }

    if let data = data {
        let responseData = String(data: data, encoding: .utf8)
        print("Response Data: \(responseData)")
    }
}

task.resume()ㄷ
```

- 위 코드보다 더 비밀번호를 암호화하여 보안 수준을 높이고 싶다면 HTTP Digest Authentication을 사용하면 된다. 하지만 기본적으로 Digset Autentication을 지원하지 않아 직접 구현해야 할 수도 있다.