# Delegate pattern

---

- 델리게이트 패턴은 객채가 자신의 책임을 다른 객체에게 위임(delegate)하는 디자인 패턴이다.
- ex) 테이블뷰는 셀을 탭했을 때 어떤 행동을 할지에 대한 책임을 뷰컨트롤러에게 UITableViewDelegate를 사용해 위임한다.
- 테이블뷰가 탭 이벤트를 받으면 delegate의 didSelectRowAt 메소드를 실행시킨다. 이벤트를 받았을 때 어떤 행동을 할 것인지 delegate에게 위임하는 것이다.