# UrlSession2

---

# HTTP

- GET
    - 서버로부터 리소스를 가져오는 데 사용됩니다.
    - 데이터를 요청 URL의 쿼리 매개변수에 포함 시켜 전달합니다.
    - 코드 예제
    
    ```swift
    func fetchMealData(date: String) {
        let url = URL(string: "https://api.junha.com/meals")!
        
        var components = URLComponents(url: url, resolvingAgainstBaseURL: true)!
        components.queryItems = [
            URLQueryItem(name: "date", value: date)
        ]
        
        guard let mealURL = components.url else {
            print("Invalid URL")
            return
        }
        
        let task = URLSession.shared.dataTask(with: mealURL) { (data, response, error) in
            if let error = error {
                print("Error: \(error.localizedDescription)")
                return
            }
            
            if let data = data {
                // 데이터 처리
                let jsonString = String(data: data, encoding: .utf8)
                print("Received meal data: \(jsonString ?? "")")
                
                do {
                    let decoder = JSONDecoder()
                    let meal = try decoder.decode(Meal.self, from: data)
                    print("Meal: \(meal)")
                    
                } catch {
                    print("Failed to parse meal data: \(error.localizedDescription)")
                }
            }
        }
        
        task.resume()
    }
    
    //사용 예제
    let date = "2023-05-30"
    
    fetchMealData(date: date)
    ```
    
- POST
    - 서버에 데이터를 제출하고, 새로운 리소스를 생성하거나 기존 리소스를 업데이트합니다.
    - 데이터는 HTTP 요청의 본문(body)에 포함시켜 전달합니다.
    - 코드 예제
    
    ```swift
    func performLogin(username: String, password: String) {
        let loginURL = URL(string: "https://api.junha.com/login")!
        
        var request = URLRequest(url: loginURL)
        request.httpMethod = "POST"
    	//	request.setValue("application/xxxxxxxx", forHTTPHeaderField: "Content-Type") 인증이 필요하다면
    	//	request.setValue("application/json", forHTTPHeaderField: "Accept") 인증이 필요하다면
        
        let bodyData = "username=\(username)&password=\(password)".data(using: .utf8)
        request.httpBody = bodyData
        
        let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
            if let error = error {
                print("Error: \(error.localizedDescription)")
                return
            }
            
            if let response = response as? HTTPURLResponse {
                if response.statusCode == 200 {
                    // 로그인 성공
                    print("Login successful.")
                    if let data = data {
                        // 응답 데이터 처리
                        let jsonString = String(data: data, encoding: .utf8)
                        print("Response data: \(jsonString ?? "")")
                    }
                } else {
                    // 로그인 실패
                    print("Login failed. Status code: \(response.statusCode)")
                }
            }
        }
        
        task.resume()
    }
    
    // 사용 예시
    performLogin(username: "john", password: "password123")
    ```
    
- PUT
    - 서버에 리소스를 업데이트하는 데 사용됩니다.
    - 데이터는 HTTP 요청의 본문에 포함시켜 전달합니다.
    - 예제 코드
    
    ```swift
    func updateResource(ID: String, newData: Data) {
        let url = URL(string: "https://api.junha.com/resources/\(ID)")!
        
        var request = URLRequest(url: url)
        request.httpMethod = "PUT"
        request.httpBody = newData
        
        let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
            if let error = error {
                print("Error: \(error.localizedDescription)")
                return
            }
            
            if let response = response as? HTTPURLResponse {
                if response.statusCode == 200 {
                    // 업데이트 성공
                    print("Resource updated successfully.")
                } else {
                    // 업데이트 실패
                    print("Failed to update resource. Status code: \(response.statusCode)")
                }
            }
        }
        
        task.resume()
    }
    
    // 사용 예시
    let resourceID = "123"
    let newData = "Updated data".data(using: .utf8)!
    updateResource(ID: resourceID, newData: newData)
    ```
    
- DELETE
    - 서버에서 리소스를 삭제하는 데 사용합니다.
    - 코드 예제
    
    ```swift
    func deleteResource(ID: String) {
        let url = URL(string: "https://api.junha.com/resources/\(ID)")!
        
        var request = URLRequest(url: url)
        request.httpMethod = "DELETE"
        
        let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
            if let error = error {
                print("Error: \(error.localizedDescription)")
                return
            }
            
            if let response = response as? HTTPURLResponse {
                if response.statusCode == 204 {
                    // 삭제 성공
                    print("Resource deleted successfully.")
                } else {
                    // 삭제 실패
                    print("Failed to delete resource. Status code: \(response.statusCode)")
                }
            }
        }
        
        task.resume()
    }
    
    // 사용 예시
    let id = "123"
    deleteResource(ID: id)
    ```
    

## utf8?

- 컴퓨터가 이해할 수 있는 유니 코드로 바꿔주는 것

## resume?

- 네트워크 요청을 시작하는 메소드입니다.
- URLSessionTask가 완료되거나 에러가 발생할 경우에는 completionHandler 클로저가 호출

## **resolvingAgainstBaseURL?**

- URLComponents의 속성 중 하나
- 상대적인 URL 문자열을 기준 URL에 상대적으로 해석할지 여부를 나타내는 Bool 값
- true
    - baseURL을 기준으로 상대적인 URL을 해석
- false
    - baseURL을 무시하고 입력된 URL 문자열을 그대로 사용