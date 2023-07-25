# SuperView

---

- 다른 view들을 포함한 view. 이 view가 포함하고 있는 view들을 subview라고 한다.
- 부모view라고 불리기도 한다.
- superView와 subView의 관계에서는 superView가 우선해서 그려진다
- 동일한 superView 내부에 여러 siblingView가 겹쳐 있다면 먼저 drawiing된 View가 가려진다. addSubview가 된 순으로 drawing 된다.

### 특징

---

- superView를 제거하면 subView도 함께 제거된다
- superView의 투명도는 subView에도 적용된다
- superView의 size가 변하면 subView의 size도 함께 변한다
- superview는 subViews를 array(배열)로 관린한다