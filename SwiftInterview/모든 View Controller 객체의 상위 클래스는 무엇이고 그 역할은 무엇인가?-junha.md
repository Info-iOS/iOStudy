# 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?
---

모든 ViewController의 상위 클래스는 UIViewController입니다.
UIViewController는 뷰를 업데이트하거나 이벤트 처리, 다른 ViewController를 포함한 다른 객체 조정(화면 이동)을 수행하기도 합니다.
UIViewController의 상위 클래스가 하나 더 있는데 UIResponder입니다.
UIResponder는 이벤트에 응답하고 이벤트를 처리하는 역할을 하는 인터페이스입니다.
이벤트가 발생하면 UIKit은 이벤트를 Responder에게 전달하고 Responder는 이벤트를 처리합니다.
반대로 UIViewController를 상속 받는 Container View Controller
UINavigationController
UISplitViewController
UITabBarViewController
UIIPageViewController
