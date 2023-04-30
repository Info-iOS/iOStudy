# tableView와 collectionView의 차이점

# tableView

---

- 단일 열에 배열된 행을 사용해 데이터를 표시하는 뷰이다.
- cell을 재사용할 수 있어, cell을 초기화하는 부담을 줄일 수 있다.

# collectionView

---

- collectionView는 tableView와 다르게 수직과 수평 스크롤을 모두 할 수 있다.
- collectionView는 레이아웃 객체가 있다.
- 기존에 제공하는 레이아웃을 사용해도 되지만 커스텀 해서도 사용할 수 있다.

# 차이점

---

- tableView는 단순한 자료들을 표현하기엔 쉽지만 자료들이 많아지면 메모리도 커지고 관리하기가 어려워 진다.
- 디자인의 수정 가능성이 높다면 collectionView를 사용해야 한다.