# 접근제어자

---

접근 제어자란?

- 접근 제어자는 접근 수준 키워드를 통해 구현 할 수 있습니다.

- open
    - 개방 접근 수준, 모듈외부까지, 클래스만 사용가능
    - 그 클래스 밖의 다른 클래스도 상속가능하다.
    - 다른 모듈에서도 부모클래스로 사용하겠다는 목적으로 사용

- public
    - 공개 접근 수준, 모듈외부까지

- internal
    - 내부 접근 수준, 모듈 외부까지
    - 내부 접슨 수준은 기본적으로 모든 요소에 암묵적으로 지정하는 기본 접근 수준
    - 보통 외부에서 사용할 클래스나 구조체가 아니며, 모듈 내부에서 광역적으로 사용할 경우 내부 접근수준을 지정합니다.

- fileprivate
    - 파일외부 비공개, 파일 내부

- private
    - 비공개 접근 수준,. 기능 정의 내부
    - 비공개 접근 수준으로 지정된 요소는 그 기능을 정의하고 구현한 범위 내에서만 사용할 수 있습니다.

open과 public 어떤 경우 다르게 사용할까요?

라이브러리 혹은 프레임워크를 설계할 때 사용자가 상속을 받아서 재정의 하면 좋겠다 싶으면 open 그게 아니라 클래스를 상속받거나 재정의 할 수 없도록 막고 싶다면 public을 사용하면 됩니다.
하지만 open 및 public은 접근 수준이 아닌 다를 클래스 및 타입은 모듈 외부에서 접근할 수 없으므로 라이브러리 혹은 프레임워크를 사용하는 프로그래머가 사용할 수 없습니다.

private 접근 수준과 fileprivate 접근 수준의 차이점

fileprivate은 그 파일 자체의 모든 코드에 접근 할 수 있습니다. 하지만 private 접근 수준으로 같은 파일 내부에 다른 타입의 코드가 있더라도 접근이 불가합니다. 하지만 자신을 확장하는 extension을 사용하면 사용가능합니다.