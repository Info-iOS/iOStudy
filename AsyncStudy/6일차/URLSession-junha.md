# URLSession

---

```swift
https://api.junha.com/photos?client_id=xxxxxxxxxxx&conut=10&page=1
```

- https
    - scheme
- api.junha.com
    - host
- photos
    - path
- client_id=xxxxxxxxxxx&conut=10&page=1
    - query

```swift
struct NetworkAPI {
    static let schema = "https"
    static let host = "api.junha.com"
    static let path = "/photos"

    func getImageAPI(page: Int) -> URLComponents {

        var c = URLComponents()
        c.scheme = NetworkAPI.schema
        c.host = NetworkAPI.host
        c.path = NetworkAPI.path

        c.queryItems = [
            URLQueryItem(name: "client_id", value: "xxxxxxxxx"),
            URLQueryItem(name: "count", value: "10"),
            URLQueryItem(name: "page", value: String(page))
        ]
        return c
    }
}

//사용 예제
let url = api.getImageAPI(page: page).url
```

그래서 URLSession이 뭔데?

- 앱과 서버 간의 데이터를 주고받기 위해서는 HTTP 프로토콜을 이용해서 데이터를 주고 받음
- 앱에서 서버와 통신하기 위해 애플이 제공하는 API
- HTTP를 포함한 몇 가지를 지원하며 인증, 쿠키 관리, 캐시 관리 등을 지원한다.
- request, response 구조를 가지고 있다

URLSessionConfiguration

- URLSession을 생성하기 위해서 필요한 요소
- Configuration을 생성할 때는 URLSession 정책에 따라 default, ephemeral, background 3가지가 존재한다.
    - Default
        - 기본 통신으로 디스크 기반 캐싱을 지원
        - 싱클턴과 비슷하게 작동하지만 delegate를 이용하여 데이터를 점진적으로 얻음
        
        ```swift
        class URLSessionManager {
            static let shared = URLSessionManager()
            private let session = URLSession(configuration: .default)
            private let api = NetworkAPI()
        
            private init() { }
        }
        ```
        
    - Ephemeral
        - 쿠키나 캐시를 저장하지 않는 정책을 가져갈 때 사용합니다.
        - 임시 세션
        - ex) 개인정보모드
        
        ```swift
        class URLSessionManager {
            static let shared = URLSessionManager()
            private let session = URLSession(configuration: .Ephemeral)
            private let api = NetworkAPI()
        
            private init() { }
        }
        ```
        
    - Background
        - 앱이 백그라운드에 있는 상황에서 컨텐츠 다운로드, 업로드를 할 때 사용합니다.
        - 앱이 실행되지 않고 백그라운드에서 콘텐츠를 업로드 및 다운로드 할 때 사용
        
        ```swift
        class URLSessionManager {
            static let shared = URLSessionManager()
            private let session = URLSession(configuration: .Background)
            private let api = NetworkAPI()
        
            private init() { }
        }
        ```
        

URLSession Delegate

- 네트워크 중간 과정을 확인할 수 있습니다.

URLSession Task

- 4가지로 나눠집니다.
    - Data Task
        - NSData 객체를 이용해서 통신
        - ex) 짧은 대화형 요청(GET)
    - UploadTask
        - 파일을 업로드할 때 사용합니다.
        - Data task랑 비슷하지만 파일형태의 데이터를 보냄
        - 백그라운드 통신 지원
        - ex) POST, PUT
    - DownloadTask
        - 파일을 다운로드 받아서 디스크에 쓸 때 사용합니다.
        - 데이터를 다운로드를 한다.
        - 백그라운드 통신 지원
    - WebSocket Task
        - RFC 6455에 정의된 WebSocket 프로토콜을 사용하여 TCP 및 TLS를 통해 메세지를 교환

URLSessionConfiguration

- URLSession의 동작을 구성하는 데 사용되는 객체
- 네트워크 연결의 속성을 구성할 수 있음
- timeoutIntervalForRequest를 설정하여 요청에 대한 타임 아웃 시간을 지정하거나 allowsCellularAccess를 사용하여 셀룰러 데이터 연경을 허용할지 여부를 설정할 수 있습니다.

URLSessionDelegate

- URLSession에서 발생하는 이벤트를 처리하는 프로토콜
- URLSessionDelegate을 사용하게 되면 URLSession의 동작을 제어하고, 네트워크 작업의 상태를 추적하고, 인증, 리다이렉트 등의 이벤트에 대한 처리를함
    - 리다이렉트란?
        - 다시 요청하다

Configuration 결정 및 Session 생성

- Configuration은 Default 설정값을 이용하고 Session을 생성가능

```swift
let config = URLSessionConfiguration.default

let session = URLSession(configuration: config)
```
