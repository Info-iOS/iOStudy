# View Change

---

### 방법

---

1. ViewController의 view 바꿔치기(overflow의 위험이 있어 좋은 방법은 아님.)
2. ViewController가 다른 ViewController를 호출(present)
3. NavigationViewController 사용하여 화면 전환(push)

### NavigationViewController 화면 전환(push)

---

- 애플에서 제공하는 대표적인 방법이다.
- 내비게이션 컨트롤러는 뷰 컨트롤러들의 계층적 구조를 관리하는 역할이기 때문에, 직접 콘텐츠를 담고 화면을 구성하지는 않는다.
- 내비게이션 컨트롤러는 화면에 현재 표시되고 있는 뷰 컨트롤러들을 내비게이션 스택을 이용하여 관리한다.(스택구조

```swift
@objc func tapCodePushButton (sender: UIButton) {
	let viewController = CodePushViewController ()
	self .navigationController?.pushViewController(viewController,animated:true)
}
```

이렇게 push해줄 수 있다.