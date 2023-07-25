# URLSession 네트워크 통신

---

- 앱에서 서버와 통신하기 위해 애플이 제공하는 API
- HTTP를 포함한 몇 가지 프로토콜(특정 역할을 하기 위한 메소드, 프로퍼티 등)을 지원하고 인증, 쿠키 관리, 캐시 관리 등을 지원
- 기본적으로 request, response 구조를 가지고 있음

### URLSession 사용 순서

---

1. Configuration(앱의 실행 환경, 설정, 변수를 관리하는 프로세스(실행되는 프로그램?))을 결정
2. Session(객체가 생성되고 설정될 때 시작되는 작업들의 그룹) 생성
3. Request(네트워크 연결을 통해 웹 서비스에 데이터를 요청하거나 전송하기 위한 객체)에 사용할 url(웹 서비스의 위치를 가리키는 URL) 설정
4. Task(네트워크 작업을 수행하는 기본 단위) 결정 및 작성

### URLSession Configuration(구성)

---

- URLSession을 생성하기 위해서 필요한 요소
- Configuration을 생성할 때는 URLSession 정책에 따라 default, ephemeral(일시적인), background 세 가지 형태로 생성
    - Default : 기본 통신으로 디스크 기반 캐싱을 지원
    - Ephemeral : 쿠키나 캐시를 저장하지 않는 정책을 가져갈 때 사용 (ex. Safari의 개인 정보보호 모드)
    - Background : 앱이 백그라운드에 있는 상황에서 컨텐츠 다운로드, 업로드를 할 때 사용, 앱이 종료돼도 통신이 이뤄지는 것을 지원하는 세션

### URLSession Delegate

---

- 네트워크 중간 과정을 확인할 수 있다. 필요에 따라서 사용

### URLSession Task

---

- 작업에 따라 (DataTask, UploadTask, DownloadTask) 3가지로 나뉨
    - UploadTask : 파일을 업로드할 때 사용
    - DownloadTask : 파일을 다운로드 받아서 디스크에 쓸 때 사용

### DataTask

---

- Data를 받는 작업, Response 데이터를 메모리 상에서 처리하게 됨
- Background 세션에 대한 지원이 되지 않는다.
- URL 요청을 실시하고 완료 시 핸들러를 호출하는 Task 형식
- Task가 실행된 후 핸들러가 실행되기 때문에 탈출 Closure 형태로 받아와야 함

### Configuration 결정 및 Session 생성

---

- Configuration은 기본 통신인 Default 설정값을 이용하였고 이를 통해서 Session을 생성할 수 있음

```swift
let config = URLSessionConfiguration.default
let session = URLSession(configuration: config)
```

### Request에 사용할 url 설정

---

- Component로 접근해도 되고 한 번에 url을 작성하는 방식도 있음
- 예제코드로는 urlComponents를 사용해서 URL을 설정하려고 함

```swift
// itunesSearchAPI를 이용해서 가수에 대한 검색과 정보를 받아오는 코드
var urlComponents = URLComponents(string: "https://itunes.apple.com/search?")!

var mediaQuery = URLQueryItem(name: "media", value: "music")
var entityQuery = URLQueryItem(name: "entity", value: "song")
var termQuery = URLQueryItem(name: "term", value: "Wondergirls")

urlComponents.queryItems?.append(mediaQuery)
urlComponents.queryItems?.append(entityQuery)
urlComponents.queryItems?.append(termQuery)

var requestURL = urlComponents.url!
```

- 코드 설명
    - media, entity, term은 itunesSearchAPI를 이용하기 위한 파라미터
    - term 부분에 본인이 찾고 싶은 가수의 이름을 작성
    - 파라미터(매개 변수 : 시스템이나 함수의 특정한 성질을 나타내는 변수) 정보는 각각의 API마다 다르게 설정되어 있음
    

### Task 작성

---

- URL을 이용해서 request했을 때 응답(response) 값을 받아오기 때문에 DataTask를 이용해야함
- 실제 네트워킹할 url을 인자로 받고 네트워킹 요청을 하고 나서 완료가 되면 수행 작업은 Completion Handler에서 작업을 진행함

```swift
let dataTask = session.dataTask(with: requestURL) { data, response, error in
    let successRange = 200..<300
    guard error == nil, let statusCode = (response as? HTTPURLResponse)?.statusCode, successRange.contains(statusCode) else {
        return
    }
    
    guard let resultData = data else {
        return
    }
    
    
    do {
        let decoder = JSONDecoder()
        let response = try decoder.decode(Response.self, from: resultData)
        let tracks = response.tracks
        print(tracks.count)
        for track in tracks {
            print("title: \(track.title)")
            print("artistName: \(track.artistName)")
            print("")
        }
    } catch let error {
        print("--> error: \(error.localizedDescription)")
    }
}

dataTask.resume()
```

### Closure 부분

---

- Completion Handler : 네트워크를 통해서 데이터를 받아오면 데이터로 하는 행동을 Closure가 수행
- 위 코드에서 resultData를 print 해보면 몇 byte가 들어왔는지만 나오고 실제로 원하는 데이터가 나오지 않음
- 간단한 확인을 위해서 encodig을 .utf8로 진행해도 되지만, 네트워킹 이후의 JSON 형식의 데이터를 받아와서 가공하고 사용함
- Closure 부분에는 Data를 원하는 형식으로 가공하는 코드가 do{} 코드 부분에 작성되어 있음
- 원하는 정보를 JSON 형식으로 받아오기 위해서 받는 상자(object)가 필요함
- 위의 Closure 코드 부분에서는 Response와 tracks를 받기 위한 상자가 더 필요함
- 그렇기 때문에 상자 역할을 해줄 오브젝트를 생성해야 함

### Object 생성

---

```swift
struct Response: Codable {
	let resultCount: Int
	let tracks: [Track]

	enum CodingKeys: String, CodingKey {
			case resultCount
			case tracks = "results"
	}
}

struct Track: Codable {
	let title: String
	let artistName: String
	let thumbnailPath: String

	enum CodingKeys: String, CodingKey {
			case title = "trackName"
			case artistName
			case thumbnailPath = "artsorUrl30"
	}
}
```

- 코드 설명
    - Codable : JSON 데이터를 원하는 오브젝트로 파싱 할 때 유용하게 사용하는 프로토콜
    - CodingKey : 임의로 입력한 변숫값과 받아온 데이터의 키 값을 맞춰주는 기능
    - 
- request에 대한 응답으로 받아온 JSON 데이터는 Key, Value의 형식으로 되어 있음. 해당 Value에 접근하기 위해서는 해당 Key의 값을 알아야함
- 가수 이름은 artistName이라는 생각으로 변수명을 작성한다면 받아온 JSON 데이터와 매칭 할 수 없음
- 이런 이유 때문에 사용하는 것이 CodingKey는 JSON 데이터 안에 이미 정해진 변수명을 사용하는 것이 아니라 내가 원하는 변수명을 사용할 수 있도록 도와주는 기능