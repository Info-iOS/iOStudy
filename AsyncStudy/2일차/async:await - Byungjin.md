# async / await

- 기존의 비동기 처리 방식은 DispatchQueue나 completionHandler를 사용하는 것이였다
- 하지만 async/await를 사용하여 더욱 편하게 비동기 처리를 할 수 있다.

```swift
//DispatchQueue
DispatchQueue.global.async {
	//code..
}

//completionHandler
let task = URLSession.shared.dataTask(with: url, completionHandler: { data, response, error in

}).resume()
```

## 왜 Async / await을 사용하나?

- 기존의 completionBlock 문법은 보기 불편하고 deep한 코드를 발생시킨다.

```swift
func processImageData1(completionBlock: (_ result: Image) -> Void) {
    loadWebResource("dataprofile.txt") { dataResource in
        loadWebResource("imagedata.dat") { imageResource in
            decodeImage(dataResource, imageResource) { imageTmp in
                dewarpAndCleanupImage(imageTmp) { imageResult in
                    completionBlock(imageResult)
                }
            }
        }
    }
}

processImageData1 { image in
    display(image)
}
```

- 또한 에러처리도 굉장히 더러운 코드가 나온다

```swift
func processImageData2c(completionBlock: (Result<Image, Error>) -> Void) {
    loadWebResource("dataprofile.txt") { dataResourceResult in
        switch dataResourceResult {
        case .success(let dataResource):
            loadWebResource("imagedata.dat") { imageResourceResult in
                switch imageResourceResult {
                case .success(let imageResource):
                    decodeImage(dataResource, imageResource) { imageTmpResult in
                        switch imageTmpResult {
                        case .success(let imageTmp):
                            dewarpAndCleanupImage(imageTmp) { imageResult in
                                completionBlock(imageResult)
                            }
                        case .failure(let error):
                            completionBlock(.failure(error))
                        }
                    }
                case .failure(let error):
                    completionBlock(.failure(error))
                }
            }
        case .failure(let error):
            completionBlock(.failure(error))
        }
    }
}

processImageData2c { result in
    switch result {
    case .success(let image):
        display(image)
    case .failure(let error):
        display("No image today", error)
    }
}
```

- 이러한 문제들을 해결하기 위해 async / await 가 등장하였다.

## async / await?

- 위 문제들을 해결하기 위해 도입된 문법이다
- 비동기 코드를 마치 동기 코드인것 처럼 작성할 수 있다.

```swift
func processImageData1(completionBlock: (_ result: Image) -> Void) {
    loadWebResource("dataprofile.txt") { dataResource in
        loadWebResource("imagedata.dat") { imageResource in
            decodeImage(dataResource, imageResource) { imageTmp in
                dewarpAndCleanupImage(imageTmp) { imageResult in
                    completionBlock(imageResult)
                }
            }
        }
    }
}

processImageData1 { image in
    display(image)
}
```

- 이런 코드를

```swift
func loadWebResource(_ path: String) async throws -> Resource
func decodeImage(_ r1: Resource, _ r2: Resource) async throws -> Image
func dewarpAndCleanupImage(_ i : Image) async throws -> Image

func processImageData() async throws -> Image {
  let dataResource  = try await loadWebResource("dataprofile.txt")
  let imageResource = try await loadWebResource("imagedata.dat")
  let imageTmp      = try await decodeImage(dataResource, imageResource)
  let imageResult   = try await dewarpAndCleanupImage(imageTmp)
  return imageResult
}
```

- 이렇게 리팩토링 할 수 있다고 한다.

### async

- 함수를 비동기 함수로 만듬

```swift
func someFunc() async -> String {
	// code..
}
// throws와 사용 가능
func someFunc() async throws -> String {
	// code..
}
```

- 반드시 async 키워드가 throws키워드 보다 먼저 선언

```swift
protocol SomeDelegate {
    func process() async
}
```

- 프로토콜에서도 요구 가능하다

### await

- 비동기 함수 호출시 **potential suspension point(잠재적인 일시 중단 지점)** 지정
- **잠재적인 일시 중단 지점**이 필요한 이유는 어떤 작업이 끝난후에만 다음 작업을 할 수 있는때가 있기 때문이다.

```swift
func process() async {
   let data = await self.getData()
   let contents = await self.decode(data: data)
   print(contents)
}
```

- 위 코드는 getData(), decode()를 호출하는 동안 작입 이 일시 중단된다.
- 만약 비동기 함수가 에러를 던질 수 있다면

```swift
func getData() async ✅ throws ✅ -> Data {
   let url = URL(string: "<https://zeddios.tistory.com>")!
   let data = try Data(contentsOf: url)
   return data
}

func decode(data: Data) async ✅ throws ✅ -> String {
   let contents = String(data: data, encoding: .utf8)!
   return contents
}

func process() async {
   do {
       let data = ✅ try ✅ await self.getData()
       let contents = ✅ try ✅ await self.decode(data: data)
       print(contents)
   } catch {
       
   }
}
```

- 위와같이 await에 `try`를 써줘야 한다.

### Task

- async 메서드를 호출하여면 async 메서드 내에서 호출되야 하는데, async 메서드에서 호출하는 것이 아니라면 Task 안에서 호출해야 한다.

```swift
Task {
    let string: String = await someStringFunc()
    print(string)
}
```

- Task는 각자 병렬적으로 수행된다.

```swift
print("Before Task")
Task {
    let string: String = await someStringFunc() //3초 대기
    print(string)
}
print("After Task")
```

- Before Task → After Task → 3초 대기 → sleep