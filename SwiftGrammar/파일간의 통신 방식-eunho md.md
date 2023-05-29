# 파일간의 통신 방식

---

- URLSession을 이용해 downloadTask()를 사용하면 지정한 URL의 내용을 가져와서 로컬 파일에 저장한 다음 완료 처리기를 호출하여 파일을 모두 조작할 수 있다.

```swift
let url = URL(string: "https://www.apple.com")!

let task = URLSession.shared.downloadTask(with: url) { localURL, urlResponse, error in
    if let localURL = localURL {
        if let string = try? String(contentsOf: localURL) {
            print(string)
        }
    }
}

task.resume()
```

- 주의사항
    1. 완료 처리기는 데이터가 로컬로 저장된 로컬 URL을 사용하여 호출된다.
    2. 문제가 발생한 경우 무슨 일이 일어났는지 설명하는 오류가 전달딘다.
    3. 다운로드 작업을 만들었을 때 resume( )을 호출하여 작업을 수행해야 한다.
    4. 다운로드 작업이 발생하는 동안 어디에 저장하는 것에 대해 걱정할 필요는 없다. 사용자를 대신하여 공유 URLSession에 의해 추적되기 때문