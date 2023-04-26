# Library

라이브러리는 일반적으로 최적화된 코드를 포함하므로, 스위프트에서 직접 구현하는 것보다 높은 성능을 제공할 수 있습니다.

### SnapKit

```swift
myView.snp.makeConstraints { make in
    make.top.equalToSuperview().offset(50)
    make.left.equalToSuperview().offset(50)
    make.right.equalToSuperview().offset(-50)
    make.bottom.equalToSuperview().offset(-50)
}
```

이와같이 표현해줄 수 있다. Auto Layout의 복잡성과 번거로움을 줄여주고, 코드를 간결하게 작성할 수 있게 도와준다. 또한 코드의 가독성도 좋아짐

### then

```swift
let label: UILabel = {

  let label = UILabel()
  
  label.textColor = .black
  
  label.text = "Hello, World!"
  
  return label
  
}()
```

이러한 초기화 코드가 있다면 then을 활용해서 밑과 같이 만들 수 있다.

```swift
let label = UILabel().then {

  $0.textColor = .black
  
  $0.text = "Hello, World!"
  
}
```

이렇게 만들면 훨씬 편리하고 가독성이 편해지며 오류를 감소 시킬 수 있다.