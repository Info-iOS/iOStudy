# URLSession

---

- 앱과 서버 간의 데이터를 주고받기 위해서는 HTTP 프로토콜을 이용해서 데이터를 주고받음
- 앱에서 서버와 통신하기 위해 애플이 제공하는 API이다
- HTTP를 포함한 몇 가지 프로토콜을 지원하고 인증, 쿠키 관리, 캐시 관리 등을 지원
- iOS 앱에서 네트워킹을 하기 위해 필요한 API

# URLSession 구현순서

---

1. URL 만들기
2. URLSession 구성하기
3. dataTask 만들기
4. 네트워크 요청완료 핸들러 처리하기

## URLSession 용어

---

- URLSessionConfiguration : URLSession을 생성하기 위해서 필요한 요소
- URLSession Delegate : 네트워크 중간 과정을 확인할 수 있다.
- UILSession Task : 작업에 따라 3가지로 나뉨
    - DataTask : Data를 받는 작업.
    - UploadTask : 파일틀 업로드할 때 사용한다.
    - DownloadTask : 파일을 다운로드 받아서 디스크에 쓸 때 사용
    
    ```swift
    //Create a URL
    let urlString = "https://openapi.naver.com/v1/search/movie.json?query=lego"
    
    //Create a URLSession
    if let url = URL(string: urlString) {
    let session = URLSession(configuration: .default)
    
    // Give URLSession a task
    let dataTask = session.dataTask(with: requestURL) { (data, reponse, error) in
    	if error != nil {
    			print(error!)
    			return
    	}
    
    if let safeData = data {
    	do {
    			let decodeData = try JSONDecoder().decode(MoviewModel.self, from: safeData)
    			completion(.success(dsecodeData))
    	} catch {
    			print(error.localizedDescription)
    	}
    }
    
    // Start a task
    
    dataTask.resume()
    ```