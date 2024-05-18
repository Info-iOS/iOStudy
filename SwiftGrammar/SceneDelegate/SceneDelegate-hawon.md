# SceneDelegate

## SceneDelegate란?

iOS 13 이후 도입된 씬 기반 생명주기 관리의 일부로, 각 ❣️씬(Scene)의 상태와 이벤트를 처리하는 역할

➡️ 간단하게 화면에 무엇을 보여줄지 관리하는 역할

❣️씬(Scene)은 앱의 UI와 상호작용하는 독립적인 인스턴스를 의미

## SceneDelegate의 역할은?

역할은 각각의 Scene들의 ❣️Life Cycle을 관리하고 Scene의 Active 및 Foreground, Background 상태에서의 공유동작처리를 관리하는 것

## ❣️생명주기(Life Cycle)

### 생명주기(Life Cycle)이란?

생명주기라는 것은 앱의 최초 실행부터 앱이 완전히 종료되기까지 앱이 가지는 상태와 그 상태들 사이의 전이

앱의 상태는 앱이 현재 어떠한 것을 할 수 있는가를 결정

### View Life Cycle이란?

이름에서 알 수 있듯 View가 생기고 사라지는 것에 대한 주기

![https://velog.velcdn.com/images%2Fdin0121%2Fpost%2F0d013262-c9c1-4d72-9436-97485c312b1f%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-21%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.18.41.png](https://velog.velcdn.com/images%2Fdin0121%2Fpost%2F0d013262-c9c1-4d72-9436-97485c312b1f%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-21%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.18.41.png)

### 1. loadView

- Controller가 관리하는 View를 만드는 역할
- View Controller의 View를 메모리에 로드
- 직접 호출 ❌ ➡️ View가 처음으로 접근될 때 시스템에 의해 호출됨

### 2. viewDidLoad

- ‘View가 Load 되었다’ 라는 뜻
- 사용자에게 화면이 보여지기 전 데이터를 뿌려주는 코드를 작성할 수 있음
- View의 초기 설정을 하는 곳으로, View 초기화나 데이터 로드를 주로 처리
- ViewController가 실행되면서 오로지 한 번만 호출됨

### 3. viewWillAppear

- ‘View가 나타날 것이다’ 라는 뜻
- View가 화면에 나타날 것이라는 신호를 알려주는 역할
    
    ➡️ View가 화면에 나타나기 직전에 호출됨
    

### 4. viewDidAppear

- ‘View가 나타났다’ 라는 뜻
- View가 나타났다는 것을 알리는 역할
    
    ➡️ View가 화면에 나타난 직후 호출됨
    

### 5. viewWillDisappear

- ‘View가 사라질 것이다’ 라는 뜻
- View가 사라지기 직전에 호출 됨

### 6. viewDidDisappear

- ‘View가 사라졌다’ 라는 뜻
- View가 사라지고 나서 호출됨

## SceneDelegate의 주요 메서드

1. **`scene(_: willConnectTo: options: )`**
    - Scene이 새로 연결될 때 호출됨 ➡️ 가장 먼저 불리는 메소드
    - 앱의 UI를 설정하고 초기화하는 데 사용됨

1. **`sceneDidDisconnect(_:)`**
    - Scene이 연결 해제될 때 호출됨
    - Scene이 더 이상 사용되지 않을 때 정리 작업을 수행

1. **`sceneDidBecomeActive(_:)`**
    - Scene이 활성 상태가 될 때 호출됨
    - Scene이 ❣️foreground에서 사용자와 상호작용을 시작할 때 사용
    
    ❣️foreground는 컴퓨팅과 모바일 애플리케이션에서 현재 사용자와 직접 상호작용하고 있는 상태
    
2. **`sceneWillResignActive(_:)`**
    - Scene이 비활성 상태로 전환될 때 호출됨
    - Scene이 일시적으로 사용자와 상호작용을 중단할 때 사용됨
        
        EX) 전화가 오거나 홈 버튼이 눌렸을 때 호출됨
        
3. **`sceneWillEnterForeground(_:)`**
    - Scene이 foreground로 진입할 때 호출됨
    - background서 foreground로 전환될 때 필요한 작업을 수행
    
4. **`sceneDidEnterBackground(_:)`**
    - Scene이 background로 진입할 때 호출됨
    - Scene이 background 전환될 때 필요한 작업을 수행
        
        EX) 데이터를 저장하거나 상태를 보존하는 작업을 넣을 수 있음