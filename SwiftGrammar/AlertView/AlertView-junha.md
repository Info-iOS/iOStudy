# AlertView

---

오늘은 AlertView에 대해서 설명해드리겠습니다.

참고로 iOS 8 이전까지는 AlertView를 사용했습니다……

하지만 이제는 AlertView를 공부하셔도 AlertView를 사용하지 못할 것 입니다.

왜냐하면 이름이 바뀌었거든요 

iOS 8 버전까지는 아래와 같이 선언했습니다

```swift
let alertView = UIAlertView(title: "제목", message: "메시지", delegate: self, cancelButtonTitle: "취소", otherButtonTitles: "확인")

alertView.show()
```

딱 보기만 해도 뭔가 많아서 어려워 보이죠 

그리고 지금과 다르게 그때는 alertView의 Delegate 선언은 필수 였습니다.

그래서 이제는 무엇으로 바뀌었냐? iOS 8 이후의 앱은 UIAlertController를 사용했습니다. 
UIAlertController 때 부터는 더욱 사용하기 편해졌으며 스타일 또한 재공해주는 것이 많아졌습니다.

그리고 iOS 8버전 이후 부터는 아래와 같이 사용하기 시작했습니다.

```swift
let alertController = UIAlertController(title: "제목", message: "메시지", preferredStyle: .alert)

let okAction = UIAlertAction(title: "확인", style: .default) { (action) in
    print("안녕")
}

alertController.addAction(okAction)

present(alertController, animated: true, completion: nil)
```

그러면 이와 같은 Alert 언제 사용하는지 알려드리겠습니다

- 예외 처리로 와이파이 또는 데이터가 꺼졌을 떄 경고 창
- 로그인 성공 및 인증번호 발송 창
- 사용자에게 다시 묻는 용도
- 중요한 파일을 삭제하는 용도

그리고 UIAlertController에는 preferredStyle 등 여러가지 스타일을 정의 해줄 수 있습니다.

> 하지만 그렇다고 UIAlertView를 사용하지 않는다는 것은 아니지만 애플 공식 문서에도 UIAlertController를 추천하는 것을 보면 다~ 이유가 있습니다.
>
