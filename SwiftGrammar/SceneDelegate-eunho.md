# SceneDelegate

SceneDelegate은 화면에 무엇을 보여줄지 관리하는 역할을 한다.

## **scene(_: willConnectTo: options: )**

제일 처음 불리는 메소드로  첫 content view, 새로운 UIWindow를 생성하고 window의rootViewController를 설정한다.

## **sceneWillEnterForeground(_ :)**

scene이 foreground로 전환될 때 불린다. 두 가지 경우가 있는데 background → foreground로 바뀔때나 처음 active일때가 있다.

## **sceneDidBecomeActive(_ :)\**

scene이 setup 되고 화면에 보여지면서 사용 될 준비가 완료 된 상태이다. inactive → active로 전환 될 때도 불린다

## **sceneWillResignActive(_ :)**

active한 상태에서 inactive 상태로 들어갈 때 불리는데 핸드폰 사용 중 전화가 걸려오는 것 처럼 임시 interruption 때문에 발생할 수 있다.

## **sceneDidEnterBackground(_ :)**

scene이 다시 foreground에서 background로 전환 될 때 불리게 되므로 다음에 다시 foreground에 돌아 올 때 복원할 수 있도록 정보를 저장하거나, 데이터를 저장, 공유 자원 돌려주는 등의 일을 하도록 하면 된다.

## **sceneDidDisconnect(_ :)**

이 메소드 내에서 해야 할 중요한 작업은 필요 없는 자원은 돌려주는 것입니다.