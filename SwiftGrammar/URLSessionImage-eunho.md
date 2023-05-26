# URLSession Image

---

- 앱을 개발할때 서버에서 프로필 이미지 광고등의 이미지의 URL을 받은 후 해당 URL을 통해 이미지를 다운 받는 개발을 해야 될 때가 많다
- 그럴 때 사용하는 것이 URL을 통한 Image Download!
- 어려울 것 없이 API 통신 하듯이 URLSession을 이용해서 다운로드 받으면 간단하게 이미지를 다운 받을 수 있다.

```swift
func imageDownload(url: URL) {
    var request = URLRequest(url: url)
    request.httpMethod = "GET"

    URLSession.shared.dataTask(with: request) { data, response, error in
        guard
            let httpURLResponse = response as? HTTPURLResponse, httpURLResponse.statusCode == 200,
            let mimeType = response?.mimeType, mimeType.hasPrefix("image"), // URLSession을 통해 이미지 데이터를 받아 오면 현재 받아온 데이터가 이미지 데이터가 맞는지 확인하기 위해 mimeType을 체크 해주는 것이다. 확인하여 이미지 데이터를 정상적으로 다운로드 받았는지 확인한다.
            let data = data, error == nil,
            let image = UIImage(data: data) //받아온 데이터를 이용하여 UIImage를 생성한다. 위의 과정들이 정상적으로 작동하지 않는다면 이미지 다운로드 실패로 판단하고 esle코드를 실행
            else {
                print("Download image fail : \(url)") // 이미지 다운로드 실패를 알려주는 코드
                return
        }

        DispatchQueue.main.async() {[weak self] in //왜 비동기 처리로 받느냐? 이미지 다운로드를 URLSession을 통해 비동기로 받았기 때문에 메인 스레드에서 imageView를 없데이트 해주라고 명시 해줘야 정상적으로 이미지를 띄울 수 있기 때문이다.
            print("Download image success \(url)")

            self?.imageView.image = image
        }
    }.resume()
}
```

하지만 위와 같은 방법을 사용한다면 필요한 ViewController마다 해당 함수를 구현 해주어야 하는 불편함이 있음.

불편함을 없애기 위해 UIImageView를 Extension하여 Image Download를 구현 할 수 있다.

# UIImage의 Extension을 활용하여 Image Download 구현

---

밑 코드는 UIImageView를 Extension으로 빼서 매번 ViewController에서 작성하지 않고 더 편리하게 사용한 것입니다.

```swift
extension UIImageView { //UIImageView를 Extension으로 뺀 것
    func imageDownload(url: URL, contentMode mode: UIView.ContentMode = .scaleAspectFit) {
        var request = URLRequest(url: url)
        request.httpMethod = "GET"

        URLSession.shared.dataTask(with: request) { data, response, error in
            guard
                let httpURLResponse = response as? HTTPURLResponse, httpURLResponse.statusCode == 200,
                let mimeType = response?.mimeType, mimeType.hasPrefix("image"),
                let data = data, error == nil,
                let image = UIImage(data: data)
                else {
                    print("Download image fail : \(url)")
                    return
            }

            DispatchQueue.main.async() { [weak self] in
                print("Download image success \(url)")

                self?.contentMode = mode
                self?.image = image
            }
        }.resume()
    }
}
```

아래 코드는 위에코드에서 파라메터로 URL을 받는 작업에서 반복 작업들을 줄이기 위해서 String으로 받아서 사용할 수 있는 메서드를 추가해서 더 깔끔한 코드를 만든 것 이다.

```swift
func imageDownload(link: String, contentMode mode: UIView.ContentMode = .scaleAspectFit) {
    guard let url = URL(string: link) else {
        return
    }

    imageDownload(url: url, contentMode: mode)
}
```