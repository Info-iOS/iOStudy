# AlertView

### **UIAlertController**

---

- UIAlertController는 두 가지 형태로 메시지 창을 표현할 수 있다.
- 하나는 **알림창**, 다른 하나는 **액션시트이**다.

---

### Alert의 구성요소

```swift
var title: String?
	//제목

var message: String?
	//메세지

var preferredStyle: UIAlertController.Style
	// alert, action sheet 둘중 하나 고르는 스타일

let alert = UIAlertController(title: "타이틀입니다", message: "메세지입니다", preferredStyle: .alert)
```

이런 식으로 AlertView를 사용하면 애플이 제공해주는 기본 팝업창을 수월하게 사용할 수 있다.

toDoList에서 사용하려는 목적

Alert View를 띄워서 입력하고 Action 하려고 한다.