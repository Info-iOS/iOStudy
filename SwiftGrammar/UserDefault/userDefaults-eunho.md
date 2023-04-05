# User Defaults

간단하게 말해서 데이터 저장소라고 생각할 수 있다.

UserDefaults를 사용하면 앱의 어느 곳에서나 데이터를 쉽게 읽고 저장할 수 있게된다.

클래스는 float, double, integer 및 boolean과 같은 공통 유형에 액세스하기위한 메소드를 제공할 뿐만아니라,

NSData, NSString, NSNumber, NSDate, NSArray 또는 NSDictionary 유형의 객체를 저장할 수도 있다.

## 사용

UserDefaults를 통해 plist에 데이터를 저장한다.

UserDefaults는 사용자의 정보를 저장하는 싱글톤 인스턴스이다.

간단한 사용자 정보를 저장 및 불러오는게 가능하지만,

내부적으로 plist 파일에 저장되기 때문에 보안상 강력하지는 않다.

```swift
// 데이터 저장
UserDefaults.standard.set("hohyeon", forKey: "userID")
    
// 데이터 불러오기
let aUser:String = UserDefaults.standard.object(forKey: "UserID") as! String 
let bUser:String = UserDefaults.standard.string(forKey: "UserID")!
```