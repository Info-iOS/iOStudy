# 맵(Map)

---

swift에서의 Map은 특정 함수를 통해 변환하여 새로운 컬렉션을 반환하는 고차함수 입니다.

map은 배열, 딕셔너리, 세트 등의 타입으로 사용할 수 있습니다.

```swift
let array = [1, 2, 3, 4, 5]
let doubledArray = array.map { $0 * 2 }
print(doubledArray) // [2, 4, 6, 8, 10]
```

때문에 map을 사용하면 여러가지 if 문과 같은 것을 줄일 수 있고 더욱 예쁜 코드를 활용할 수 있습니다.
