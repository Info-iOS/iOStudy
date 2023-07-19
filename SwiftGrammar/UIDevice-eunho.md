# UIDevice

---

<aside>
❗ UIDevice 클래스에 접근하면 해당 디바이스의 정보를 알 수 있다.

</aside>

- 디바이스 이름 / 모델 / 화면 방향 등등
- OS 이름 / 버전
- 인터페이스 형식 (phone, pad, tv 등)
- 배터리 정보
- 근접 센서 정보
- 멀티태스킹 지원 여부

### 접근방법

---

```swift
let device = UIDevice.current
```

### system 버전

---

<aside>
❗ 버전에 따라 Major, Minor(public), Minor(non-public)가 존재함

</aside>

- 개발을 할때 버전별로 API가 다를수 있기 때문에 분기처리를 위한 systemVersion을 알아야한다.

```swift
if #available(iOS 9.0, *) {
	print("9.0이상")
} else {
	print("9.0미만")
}
```

### 디바이스

---

<aside>
❗ UIDevice에 대한 extension을 설정하면 프로젝트 어디에서든 해당 화면에 대한 구분을 할 수 있음

</aside>

```swift
extension UIDevice {
	public var isPhone: Bool {
		if UIDevice.current.userInterfacelidom == UIUserInterfaceldiom.phone {
			return true
	}
return false
}
public var isIpad: Bool {
		if UIDevice.current.userInterfacelidom == UIUserInterfaceldiom.pad {
			return true
		}
		return false
}}		 
```

```swift
if UIDevice.current.isPhone {
		// 아이폰
} else if UIDevice.current**********************.isPad {
		// 아이패드
}**********************
```