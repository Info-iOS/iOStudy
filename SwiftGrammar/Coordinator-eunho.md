# Coordinator

---

- Coorinator는 View Controller가 단일 책임 원칙을 따르고 응집력을 유지할 수 있도록 돕는 데 사용된다.
- 앱 내에서 다양한 화면 간 전환 및 비즈니스 로직을 처리하는 데 사용된다.
- Coordinator를 통한 화면 전환시 View Controller에서 사용할 View Model을 함께 주입해줄수 있어 DI(**Dependency Injection**) 또한 쉽게 해결할 수 있다.

```swift
protocol ProductDetailCoordinator: AnyObject {
  func pushToDetail(_ navigationController: UINavigationController, productId: String)
}

extension ProductDetailCoordinator {

  func pushToDetail(_ navigationController: UINavigationController, productId: String) {
    let vc = DetailViewController()
    vc.setNavigationTitle("상세화면")
    vc.productId = productId
    navigationController.pushViewController(vc, animated: true)
  }

}
```

- delegate protocol로 상품 상세 화면으로 전환하는 coordinator를 만들고, extension하여 화면 전환에 필요한 작업을 구현한다.