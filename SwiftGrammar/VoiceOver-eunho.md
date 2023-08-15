# VoiceOver

---

- VoiceOver 는 화면을 보지 않아도 기기의 인터페이스를 경험할 수 있게 해주는 스크린 리더이다.
- 시력이 좋지 않은 분들은 VoiceOver에 의존하여 iOS 를 사용하고 있다

### 탭 동작

---

- 탭을 하게 되면 한 항목을 선택할 수 있다. 선택된 항목에 대한 정보를 읽어줌
- 기존 탭 기능은 더블탭으로 사용할 수 있음.

### 슬라이드 동작

---

- 오른쪽으로 슬라이드 하면 다음 항목 선택
- 왼쪽으로 슬라이드 하면 이전 항목 선택
- 위/아래 슬라이드를 통해서는 VoiceOver 로터에 등록된 기능을 사용할 수 있음

### VoiceOver 적용

---

- iOS 에서 기본적으로 제공하는 뷰는 기본적인 VoiceOver를 지원하여 컨텐츠에 대한 사운드 피드백을 준다.
- 개발하는 앱들은 복잡한 뷰로 구성되어 있기 때문에 설정을 통해 VoiceOver를 적용해야함

### 기본 속성들

---

1. isAccessibilityElement : 값을 true로 설정하면 해당 요소에 커서를 이동할 수 있다. 불필요한 내용을 읽지 않게 하기 위해 사용함

```swift
let imageView = UIImageView()
imageView.isAccseeibilityElement = false //읽지 않는다.
```

1. accessibilityLabel : 요소를 선택할 때 읽어주는 텍스트

```swift
let addButton = UIButton()
button.setImage(UIImage(named: "add", for: .normal))
button.accessibilityLabel = "추가하기"
```

1. accessibilityHint : 요소에 대한 추가 설명이나 동작시키기 위한 방법 안내

```swift
let imageView = UIImageView()
imageView.accessibilityLabel = "사진"
imageView.accessibilityHint = "2020년 10울 10일 촬영된 사진"
```

1. accessibilityValue : 값이 달라지는 요소(textField)에 사용. 슬라이더의 경우 Label에 다운로드 진행도 Value “50%”처럼 설정 가능

```swift
let slider = UISlider()
slider.accessibilityLabel = "다운로드 진행도"
slider.accessibilityValue = "50%"
```

1. accessibilityTraits : 접근성 요소의 특징을 지정. 

```swift
let imageView = UIImageView()
imageView.accessibilityTraits = .image

let button = UIButton()
button.accessibilityTraits = .button

let view = UIView()
view.accessibilityTraits = .none3
```

1. UIAccessibility Notification : 앱 내의 변경사항이 있을 때 Notification을 통해 알림

```swift
let view = UIView()

// 레이아웃 변경 알림 코드
UIAccessibility.post (
	notification: UIAcessibility.Notification.layoutChanged,
	argument: view
)
```