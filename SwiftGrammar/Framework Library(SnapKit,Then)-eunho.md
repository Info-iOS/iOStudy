# Framework, Library(SnapKit, Then)

---

## Framework

---

- Framework는 계층 구조를 갖는 디렉터리를 의미한다.
    - directory(디렉터리)는 컴퓨팅에서 파일을 분류하기 위해 사용하는 이름공간이다.
- Framework 은 Library 처럼 목적(같은 도메인)이 같은 코드의 모음이다.

## Framework가 Library와 다른점

---

- 리소스(resource)를 포함할수 있다. ex) image, asset, documentations, strings
- 오직 하나의 Framework 코드 및 리소스를 메모리에 올릴수 있다. (라이브러리는 여러 개 가능)
- 하나만 사용하기 때문에 메모리 풋프린트(foot print: 단위가 차지하고 있는 공간의 크기)를 줄이고, 시스템 성능을 향상 시킬수 있다.
- 여러 앱에서 해당 Framework이 필요한 경우, 공유되어 사용할 수 있다.

## XCFrameworks

---

- XCFrameworks 는 Framework 배포 방법이다.
- 여러번형들(디바이스, 시뮬레이터 등)을 포함해서 배포할 수 있다.
- Swift 와 C 기반 코드 바이너리(binary: 2진 형태로 저장되어 있는 이진 파일)를 지원한다.
- Static Library와 헤더들을 묶을 수 있다.

## Library

---

- 단순 활용가능한 도구들의 집합을 말한다. 쉽게 말해 프로그램을 개발하기 위해 쓰는 공구와 같은 도구들이다.
- 개발자가 만든 클래스에서 호출하여 사용하거나 클래스들의 나열로 필요한 클래스를 불러서 사용하는 방식이다.

## SnapKit

---

- Auto Layout 기능을 코드로 손쉽게 적용하도록 도와주는 기능을 제공하는 라이브러리이다.
- 가독성을 잃지 않으면서 최소한의 코드만으로 자동 레이아웃을 코드에 작성하는 것 을 단순화한 레이아웃 라이브러리이다.

## Then

---

- 이니셜 라이즈 코드를 간단하게 해주는 것이고 SnapKit은 레이아웃 코드를 간단하게 만들어 주는 것이다.
- 따라서 합쳐 사용했을 때 효율성이 증가한다.

```swift
//then을 사용하지 않았을 때
let nameLabel: UILabel = {
        let label = UILabel()
        label.textAlignment = .center
        label.textColor = .black
        label.font = .systemFont(ofSize: 30)
        label.backgroundColor = .red
        label.text = "나의 이름은 ***입니다."
        return label
    }()
```

```swift
//then을 사용했을 때
let secondNameLabel = UILabel().then {
        $0.textAlignment = .center
        $0.textColor = .black
        $0.font = .systemFont(ofSize: 30)
        $0.backgroundColor = .red
        $0.text = "나의 이름은 ***입니다. "
    }
```

상수 선언할 때 then을 같이 써줌으로써 label이 반복되는 곳을 더 $0.으로 단축하여 사용하여 편리하고 짧게 코딩할 수 있다.