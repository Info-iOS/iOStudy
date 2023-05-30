# Encoding & Decoding & Codable

---

## Encoding

- 인코딩은 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해서 다른 형태나 형식으로 변환하는 처리 혹은 그 처리 방식을 뜻한다.

## Decoding

- 인코딩의 반대 작업을 수행하는 것

## Codable

- 스위프트 4 버전에서는 스위프트의 인스턴스를 다른 데이터 형태로 변환하고 그 반대 역활을 수행한다.

```swift
typealias Codable = Decodable & Encodable
```

- json 형식으로 서버와 애플리케이션이 통신한다면 Codable 프로토콜을 이용해 편리하게 인코딩과 디코딩이 가능하다

## **CodingKey**

- json 형태를 변환하고자 할 때 사용한다. 기본적으로 인코딩/디코딩할 JSON 타입의 키와 애플리케이션의 사용자 정의 프로퍼티가 일치한다.

## **JSONEncoder**

- 스위프트 타입의 인스턴스를 JSON 데이터로 인코딩
- Codable 프로토콜을 준수하는 login 구조체의 인스턴스를 JSON로 인코딩 방법
- 

```swift
struct Login: Codable {
    var name: String
    var password: Int
}

let pear = Login(name: "junha", password: 12345678)

let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted

do {
	let data = try encoder.encode(pear)
	print(String(data: data, encoding: .utf8)!)
} catch {
	print(error)
}

//출력
{
   "name" : "junha",
   "password" : 123456789
 }
```