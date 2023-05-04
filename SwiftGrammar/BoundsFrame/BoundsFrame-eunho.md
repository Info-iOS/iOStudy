# Bounds, Frame

- bounds 와 frame은 UIView 의 instance property 이다.

# Frame

- frame은 Super View 좌표계에서 View의 위치와 크기를 나타낸다.
- 간단하게 말해서 Super View의 좌표계이다.
- superView의 원점으로부터 x, y축으로 얼마나 떨어져 있는지를 나타낸다.
- superView 좌표계 안에서 현재 view가 사각형 영역으로 차지하고 있는 크기를 나타내기 때문에, view를 회전 시킨다면 frame의 크기는 달라질 수 있다.

# Bounds

- 자기 자신의 좌표계 안에서 원점을 결정하므로 별도의 값을 할당하기 전까지는 항상 0으로 초기화 된다.
- 자기 자신의 크기를 나타내서 view가 회전해도 frame과 달리 크기는 항상 같다

```swift
//bounds origin
bounds x = 0.0, y = 0.0
```