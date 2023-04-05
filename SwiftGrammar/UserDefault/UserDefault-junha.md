# UserDefault
---

## UserDefault란?

- 데이터 저장소
- 앱의 어느 곳에서나 데이터를 쉽게 읽고 저장할 수 있습니다.
- swift에서 사용하는 로컬 저장소

## UserDefault 어떤 경우에 사용할까?

- 사용자 기본 설정과 같은 데이터 값에 넣는 것이 적합
- 대량의 데이터 저장에는 추천하지 않음(그런 곳에는 CoreData, sqlite)
- 예를 들어서 스위치를 눌르고 다른 controller에 와도 스위치가 눌러져있는 상태에 있고 싶을 경우

## UserDefault 어떻게 사용할까?

- UserDefaults.standard.set(데이터, “키”)
- 여기서 키는 나중에 불러올때 키값을 적으면 데이터를 불러옵니다.
- UserDefaults를 통해 plist에 데이터를 저장한다.
- UserDefaults는 사용자의 정보를 저장하는 싱글톤 인스턴스이다.
- 간단한 정보를 저장 및 불러올 수 있다.
- 내부적으로 plist파일에 저장되기 때문에 보안이 약하다.

## UserDefault 뜯어보기

```swift
open class var standard: UserDefaults { get }
    
// 데이터 가져오기
open func object(forKey defaultName: String) -> Any?
open func string(forKey defaultName: String) -> String?
open func array(forKey defaultName: String) -> [Any]?
    
// 데이터 저장하기
open func set(_ value: Any?, forKey defaultName: String)
    
// 데이터 지우기 
// 키 값을 입력하면 삭제 가능
open func removeObject(forKey defaultName: String)
```

## UserDefault 사용 예제

```swift
let myUserDefaults = UserDefaults.standard

let aUserSave = myUserDefaults.set("aUsers", forKey: "userID")
let aUserLoad = myUserDefaults.string(forKey: "userID)!
```
