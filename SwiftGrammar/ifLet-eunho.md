# if let

if let은 if문 안의 조건문의 값이 nil인지 아닌지 판단하는 문법이다.

조건문이 nill이 아니라면 해당 블럭이 실행되는 구조이다.

```swift
	if let constant name = optional {
			statements
}
```

위 코드는 if let 문법의 기본적인 형태이다.

## if let 예제 코드

```swift
let data: String? = nil
// 결과 : data is nil

let data: String? = "eunho"
// 결과 : data :: eunho

if let str = data {
	print("data :: /(str)")
} else {
	print("data is nil")
}
```

```swift
var name: String? 
var = "eunho"
print(name) //옵셔널 은호

if let myName = name { // name이 nil이 아니라면 참 nil이면 거짓
	print(myName) // name이 nil이 아니라면 
} else {
	print("nil") // name이 nil이라면
}
// 이 코드의 결과 : eunho
```

if let 구문 안에 있는 my name 변수는 지역변수로서 if let 구문 안에서만 사용할 수 있다. 

```swift
var name: String? 
var = nil
print(name) // nil

if let myName = name { // name이 nil이 아니라면 참 nil이면 거짓
	print(myName) // name이 nil이 아니라면 
} else {
	print("nil") // name이 nil이라면
}
// 이 코드의 결과 : nil
```

이와 같이 myName이 name과 다른 즉 nil일 때 라면 거짓이 실행되어 nil을 출력하게 된다.