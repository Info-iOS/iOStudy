# AppDelegate

## AppDelegate란?

 iOS 애플리케이션의 주요 진입점으로, 앱의 전체 생명주기와 중요한 상태 변화를 관리하는 객체

## AppDelegate의 역할은?

- 애플리케이션 초기화
- 애플리케이션 상태 전환 처리
- 원격 및 로컬 알림 처리
- URL 스킴 및 ❣️Universal Links 처리
- background 작업 지원
- SceneDelegate 관리

❣️Universal Links은 iOS 앱에서 웹 URL을 사용하여 앱의 특정 화면으로 직접 연결할 수 있는 기능

## AppDelegate의 주요 메서드

1. **`application(_:didFinishLaunchingWithOptions:)`**
- 앱이 실행되고 초기화 작업을 수행

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // 초기화 작업
    return true
}
```

1. **`applicationDidBecomeActive(_:)`**
- 앱이 활성화 상태가 되었을 때 호출됨
- 앱이 foreground로 돌아왔을 때 필요한 작업을 수행

1. **`applicationWillResignActive(_:)`**
- 앱이 비활성화 상태로 전환되기 직전에 호출됨
    
    EX) 전화가 오거나 앱이 일시 중지될 때
    

1. **`applicationDidEnterBackground(_:)`**
- 앱이 background 상태로 진입했을 때 호출됨

1. **`applicationWillEnterForeground(_:)`**
- 앱이 background에서 foreground로 전환되기 직전에 호출됨

1. **`applicationWillTerminate(_:)`**
- 앱이 종료될 때 호출됨