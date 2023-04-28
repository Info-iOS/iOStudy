# Codable, Encoding, Decoding

# Codable

- Codable은 Encodable과 Decodable이 합쳐진것이다.
    - Encodable은 data를 Encoder에서 변환해주려는 프로토콜로 바꿔주는 것. 모델을 json으로 인코드 해주는 것.
    - Decodable은 data를 원하는 모델로 Decode 해주는 것. json을 내가 원하는 모델로 디코드
    
    ```swift
    struct Person: Codable {
        var name: String
        var age: Int
    } // 이름과 나이
    
    let person = Person(name: "John", age: 30) 
    
    // JSON 인코딩 데이터를 다른형식으로 변환
    if let jsonData = try? JSONEncoder().encode(person),
       let jsonString = String(data: jsonData, encoding: .utf8) {
        print(jsonString)
    }
    
    // JSON 디코딩 다시 원래의 형태로 변환한다
    let jsonString = """
        {
            "name": "Jane",
            "age": 25
        }
    """
    
    if let jsonData = jsonString.data(using: .utf8), 
       let decodedPerson = try? JSONDecoder().decode(Person.self, from: jsonData) {
        print(decodedPerson)
    }
    ```
    

# Encoding

- 프로그래밍에서는 데이터를 다양한 형식으로 인코딩하고, 이를 다시 디코딩하여 원래의 데이터로 변환한다.
- 인코딩은 어떤 데이터를 다른 형식으로 변환하는 것을 말한다.
- 인코딩은 주로 데이터의 전송 및 저장에 사용된다.

# Decoding

- 디코딩은 인코딩된 데이터를 다시 원래의 형식으로 변환하는 것을 말한다.
- 데이터를 인코딩할 때는 해당 데이터를 다른 형식으로 변환하여 다른 시스템에서도 사용할 수 있도록 한다.
- 해당 데이터를 사용하려면 다시 원래의 형식으로 변환해야 하는데, 이 작업을 디코딩이라고 한다.