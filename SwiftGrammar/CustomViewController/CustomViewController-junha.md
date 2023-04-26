# Custom View Controller

---

customViewController란 무엇일까?

나도 모르는 엄청난 개념이라서 기대하는 마음으로 찾아 보았다.

엄청 열심히 찾아 보았다 계속 View를 커스텀하는 너무 뻔한 지식만 나와서 은호의 뜻 깊은 마음을 알지 못하는 줄 알고 엄청 열심히 찾아보았는데 swift에서 CustomViewController라는 viewcontroller는 없다.

그랬다 은호에 깃허브를 가서 나는 알게 되었다 위에서 View를 커스텀하는 뻔한 지식이 었다는 것을 난 진짜 몰랐다…….. 그래서 이렇게 정리해보게 되었다.

하나의 ViewController에 객채를 만드는 것보다는 다른 ViewController를 상속시키거나 UIView 같은 것을 상속 기켜서 하는 것이 더 좋다고 실제로도 생각하고 있다.

이제 자기가 직접 UICollectionViewController나 UITableViewController, UINavigationController를 사용하지 않고 직접만들면 무엇이 좋을까?

1. 유지보수가 편해진다.
2. 상속의 개념을 보통은 이럴 경우 많이 쓰기 때문에 코드의 중복을 줄여준다
3. 조금 더 깔끔한 코드를 작성할 수 있다.
