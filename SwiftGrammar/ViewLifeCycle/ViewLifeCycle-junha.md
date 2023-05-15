### init
​
-   viewController 객체가 생성됩니다.
​
### loadView
​
-   View를 메모리에 로드합니다.
​
### viewDidLoad
​
-   뷰가 로드되었다!
-   뷰가 컨트롤러가 메모리에 로드되고 난 후 호출
-   (리소스 초기화 또는 화면이 처음 만들어질 때, 처음 한 번만 실행해야 하는 초기화코드의 경우 사용)
​
### viewWillAppear
​
-   뷰가 나타날 것이다.
-   뷰가 나타나기 직전 호출
-   (다른 뷰를 갔다가 다시 돌아오는 상황에 사용)
-   (viewController가 화면에 나타날 때마다 반복 실행)
​
### viewDidAppear
​
-   뷰가 나타났다.
-   view가 화면에 나타난 직후에 실행
-   (뷰가 화면에 나타난 직후를 빼면 viewDidAppear와 viewWillAppear는 거의 같다)
-   (뷰가 화면에 나타난 즉시 발생하는 이벤트를 작업할 때 사용)
​
### viewWillDisappear
​
-   뷰가 사라질 것이다.
-   뷰가 사라지기 직전에 호출
-   (뷰가 삭제되려고 하는 것을 통제합니다.)
​
### viewDidDidDisappear
​
-   뷰가 사라졌다.
-   뷰 컨트롤러가 뷰가 제거되었음을 알려줌
-   (view가 메모리에서 해제된 후 호출됩니다.)
​
### viewDidLoad와 viewWillAppear의 차이점
​
처음 A --> B --> C를 가게 되면 viewDidLoad와 viewWillAppear가 모두 실행됩니다.
​
하지만 C --> B --> A로 돌아오게 되면 viewWillAppear만 발생합니다.
​
그리고 A --> B --> C로 갈 때도 viewWillAppear만 발생합니다.
​
글이 도움 됐으면 좋겠습니다.
