# SceneDelegate

---

**SceneDelegate란?**

- **화면에 표시되는 내용 즉 Windows나 Scnes들을 처리하고 앱에 표시하는 방식을 제공합니다.**

**SceneDelegate는 어떤 역활을 하는 것들이 있을까?**

- willConnectTo
- scene이 앱에 추가될 때 호출

```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions)
```

- sceneDidDisconnect
- scene의 연결이 해제될 때 호출

```swift
func sceneDidDisconnect(_ scene: UIScene)
```

- sceneDidBecomeActive
- app *switcher*에서 선택되면 inActive 상태에서 active 상태로 전환

```swift
func sceneDidBecomeActive(_ scene: UIScene)
```

- sceneWillResignActive
- active 상태에서 inactive로 전환시

```swift
func sceneWillResignActive(_ scene: UIScene)
```

- sceneWillEnterForeground
- background에서 foreground로 전환시

```swift
func sceneWillEnterForeground(_ scene: UIScene)
```

- sceneDidEnterBackground
- foreground에서 backgRound로 전환시

```swift
func sceneDidEnterBackground(_ scene: UIScene)
```

Scene

- 하나의 앱에도 여러개의 UI 인스턴스가 존재할 수 있음
- Scenes
    - 각 인스턴스는 UIWindowScene가 관리함
    - 앱 인스턴스는 UI를 표현하기 위한 window, viewController를 포함하는 UIWindowSceneDelegate 객체를 가진다.
    - 여러가지 Scene 들은 동시에 실행하고 하나의 앱에 같은 메모리와 프로세스 공간을 공유한다
    
    > 같은 메모리를 공유함
    두 scene에 각각 숫자를 표시하는 UILabel이 있을 때 두 변수가 동일한 메모리 공간을 차지하는 것을 의미하는 것이 아니라 SceneDelegate 객체들이 App 단위의 하나의 메모리에서 나타나고 사라지는 scene에 따라 관리된다는 것을 뜻하는 것 같다.
    > 
    

**UIWindowScene**

- 앱의 scene 인스턴스 하나를 관리하는 타입으로 인스턴스의 UI를 표현하기 위해 window를 갖는다
- scene의 상태가 변하면 scene 객체는 UIWindowSceneDelegate 프로토콜을 adopt하는 delegate 객체를 노티피한다.
