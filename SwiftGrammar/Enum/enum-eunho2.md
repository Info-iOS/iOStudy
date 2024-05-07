# 열거형

---

<aside>
❕ Enum(Enumeration)

</aside>

- 보기 쉽고 깔끔한 코드
- 효율적인 코드

### Enum이란?

---

> *“컴퓨터 프로그래밍에서 열거형은 요소. 멤버라 불리는 명명된 값의 집합을 이루는 자료형이다. 열거자 이름들은 일반적으로 해당 언어의 상수 역할을 하는 식별자이다.”*
> 

뭐가 좋은데…??

- 코드가 보기 쉽고 간결해진다.
- 코드를 작성할때 실수를 줄여준다.
- 코드를 작성하기 편리해진다.

### 1. 코드가 보기 쉽고 간결해진다.

---

- Enum을 사용하면 미리 원하는 집합을 나열해놓을 수 있다.

```python
enum Asia {
    case korea,china,japan
}

enum America {
    case usa
    case canada
    case mexico
}

enum Africa {
    case libya, egypt, ethiopia
}

enum Europe {
    case france
    case italy
    case germay
}

enum Oceania {
    case australia
    case newzealand
    case solomon
}
```

```python
let myCountry = Asia.korea
```

```python
enum Asia:String {
case korea = "대한민국"
case japan = "ㄴㅇㄹㄴㅇㄹ"
case china = "ㄴㅇㄹㄴㅇㄹsdf"
}

let myCountry = Asia.korea

print(myCountry)

출력
korea
```

```python
enum Asia:String {
case korea = "대한민국"
case japan = "ㄴㅇㄹㄴㅇㄹ"
case china = "ㄴㅇㄹㄴㅇㄹsdf"
}

let myCountry = Asia.korea.rawValue

print(myCountry)

출력
대한민국
```

### 코드를 작성할때 실수를 줄여준다

---

```python
var countryDic:[String:[String]] = [:]

countryDic["Asia"] = ["korea","china","japan"]
countryDic["America"] = ["usa","canada","mexico"]
countryDic["Africa"] = ["egypt","lybia","ethiopia"]
countryDic["Europe"] = ["france","italy","germany"]
countryDic["Oceania"] = ["australia","newzealand","solomon"]

let korea = countryDic["Asia"]![0]
print(korea) //korea
```

- enum없이 코딩한다면?
    
    더럽다...
    
- enum을 사용하면 오타를 줄일 수 있음

### 코드를 작성하기 편리해진다.

---

- .(점)을 이용해서 값을 정할 수 있다.