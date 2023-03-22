# View life cycle

## view의 생명주기

앱들은 ‘View Controller’로 이루어져 있는데, 하나 이상의 화면이 있다면 이 각각의View Controller들은 생명주기를 가지고 있다. View Controller의 생명주기는 보여졌다 사라지는 주기이다.

  

## Will과  Did

Will은 미래를 나타내고 Did는 과거를 나타낸다.

1. viewDidLoad
2. viewWillAppear
3. viewDidAppear
4. viesWillDisappear
5. viewDidDisappear

### 1. viewDidLoad

Did : 과거

뜻 : “뷰가 로드 되었다”라는 뜻이다.

viewDidLoad 메소드는 뷰의 로딩이 완료 되었을 때 시스템에 의해 자동으로 호출되기 때문에 리소스를 초기화하거나 초기 화면을 구성하는 용도로 주로 사용한다. 화면이 처음 만들어질 때 한 번만 실행되므로, 처음 한 번만 실행해야 하는 초기화 코드가 있을 경우 이 메소드 내부에 작성하면 된다.(View Controller생에 딱 한번만 호출이 된다.)

### 2.viewWillAppear

Wiill : 미래

뜻 : “뷰가 나타날 것이다”라는 뜻 이다.

타이밍 : 뷰 컨트롤러의 화면이 올라오고 난후 뷰가 나타나기 직전에 호출이 된다.

view가 이제 나타날 거라는 신호를 컨트롤러에게 알리는 역할을 한다. 즉 뷰가 나타나기 직전에 호출이 된다.  

viewWillAppear와 viewDidLoad의 차이 다른 뷰에서 갔다가 다시 돌아오는 상황에도 띄우고 싶다면 viewWillAppear를 사용해야 한다.

### 3.viewDidAppear

Did : 과거

뜻 : “뷰가 나타났다”라는 뜻이다.

타이밍 : view가 데이터와 함께 완전히 화면에 나타난 후 호출되는 메소드

viewDidAppear는 뷰가 나타났다는 것을 컨트롤러에게 알리는 역할을 한다. 또한 화면에 적용될 애니메이션을 그려준다. viewDidAppear는 뷰가 화면에 나타난 직후에 실행된다.

### 4. viewWillDisappear

Will : 미래

뜻 : “뷰가 사라질 것이다”라는 뜻이다.

타이밍 : 다음 View Controller 화면이 전환하기 전이나 View Controller가 사라지기 직전에 호출된다.

viewWillDisappear는 뷰가 삭제 되려고하고있는 것을 뷰 컨트롤러에 통지한다.

### 5. viewDidDisappear

Did : 미래

뜻 : “뷰가 사라졌다.”라는 뜻이다.

타이밍 : View Controller들이 화면에서 사라지고 나서 호출됨

viewDidDisappear가 호출 되면, 뷰 컨트롤러가 뷰가 제거되었음을 알려준다.