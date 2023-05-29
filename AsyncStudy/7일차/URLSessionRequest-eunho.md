# URLSession 요청 작업

---

- 서버와 통신하기 위한 방법으론 라이브러리 형식인 Alamofire가 있고 URLSession의 URLRequest를 이용하는 방법이 있다.

```swift
//
import UIKit

struct Response: Codable {
	let succesee: Bool
	let result: String
	let message: String
}

//body 가 없는 요청
func requestGet(url: String, completionHandler: @escaping (Bool, Any) -> Void) {

}

//body가 있는 요청
func requestGet(url: String, method: String, param: [String: Any], completionHandler: @escaping (Bool, Any) -> Void) {

}

func request(_ url: String, _ method: String, _ param: [String: Any]? = nil, completionHandler: @escaping (Bool, Any) -> Void) {
    if method == "GET" {
        requestGet(url: url) { (success, data) in
            completionHandler(success, data)
        }
    }
    else {
        requestPost(url: url, method: method, param: param!) { (success, data) in
            completionHandler(success, data)
        }
    }
}

request("http://localhost:5000/test/get", "GET") { (success, data) in
  print(data)
}

// 또는 아래와 같이도 쓸 수 있다.

request("http://localhost:5000/test/post", "POST", ["key": "hello!"]) { (success, data) in
  print(data)
}

//첫 번째 인자로는 URL을, 두 번째 인자는 METHOD를, 세 번째 인자로는 Optional로 Body에 들어갈 Dictoinary 타입의 데이터를 넣어준다.
```

request 함수를 요청하면 서버로부터 받은 데이터를 Escaping Closure를 통해서 View 파일에서 사용할 수 있게 된다.