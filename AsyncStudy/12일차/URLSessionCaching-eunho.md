# URLSession Caching

---

- URLSession은 네트워크 요청을 수행하는 데 사용되는 iOS의 기본 네트워킹 라이브러리이다.
- URLSession은 기본적으로 캐시를 지원하며, 서버에서 가져온 데이터를 캐시에 저장하고 이후에 동일한 요청이 발생할 때 캐시에서 데이터를 가져올 수 있다.
- URLSession의 기본 캐시 동작 :
    - 메모리 캐시 : 앱이 실행되는 동안 메모리에 데이터를 저장하는 것
    - 디스크 캐시 : 데이터를 디스크에 저장하여 앱이 다시 실행되거나 재부팅되어도 데이터를 보존한다.

```swift
// URLSessionConfiguration을 생성하고 캐시를 활성화 하는 코드
let config = URLSessionConfiguration.default
config.requestCachePolicy = .returnCacheDataElseLoad

// URLSession을 생성하고 캐시가 활성화된 configuration을 사용함
let session = URLSession(configuration: config)

//URL 생성
let url = URL(string: "http://www.mukgen.info/meal/today")!

//URLSessionDataTask를 사용하여 데이터 요청
let task = session.dataTask(with: url) { (data, response, error) in
	if let error = error {
			print("Error: \(error.localizedDescription)")
			return
	}

	//옳은 데이터일때 데이터 사용
	if let data = data {
			let responseData = String(data: data, encoding: .utf8)
			print("Response Data: \(responseData)") 
	}
}

//요청 시작
task.resume()
```

위 코드에서 데이터를 우선적으로 캐시에서 가져오고 캐시에 데이터가 없을 경우에만 네트워크 요청을 수행하는 코드이다. 

만약 항상 캐시를 우선적으로 사용하고 싶다면 .useProtocolCachePolicy로 설정 가능하다