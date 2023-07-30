# Tuist edit

---

```swift
tuist edit // 입력
```

```swift
tuist edit
Generating workspace Manifests.xcworkspace
Generating project Manifests
Generating project Plugins
Opening Xcode to edit the project. Press CTRL + C once you are done editing
```

위와 같이 나오면 정상

project 파일이 정상적으로 생기면 성공

프로젝트 파일에 프로젝트를 만든다

```swift
import ProjectDescription

let target = Target(
    name: "WebTest",
    platform: .iOS,
    product: .app,
    bundleId: "com.Kimbaechu.WebTest",
    infoPlist: .default,
    sources: ["WebTest/Sources/**"],
    resources: ["WebTest/Resources/**"],
    dependencies: []
)

let project = Project(
    name: "WebTest",
    organizationName: nil,
    options: [],
    packages: [],
    settings: nil,
    targets: [target],
    schemes: [],
    fileHeaderTemplate: nil,
    additionalFiles: [],
    resourceSynthesizers: []
)
```

창을 종료하고 터미널에 돌아와 CTRL + C 를 입력

Sources와 Resources를 구분해야함

swift 파일은 Soureces로 넣고 나머지는 Recources로 넣어줌

tuist generate하면 실행 완료