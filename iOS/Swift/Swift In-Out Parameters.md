# Swift In-Out Parameters

<aside>

<br>

📩 **in-out 매개변수**

---

**변경된 값이 함수 호출이 종료된 후에도 지속되는 파라미터**

- 함수 정의시 파라미터의 타입 전에 `inout` 키워드를 추가
- in-out 파라미터는 변수만을 취급 → 상수 **X**
- 함수의 인자로 전달할 때 `&`를 사용

*pointer 매개변수랑 비슷하다 하지만 차이점이 존재한다.*

</aside>

> **등장 배경**
> 
> 
> ---
> 
> Swift에서 파라미터는 상수 → 함수 내부에서 파라미터의 값을 변경할 수 없다
> 

<br>

### 사용 🔥

---

```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
	let temp = a
	a = b
	b = temp
}

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
// someInt = 107, anotherInt = 3
```

<br>

### 포인터와의 차이점 🧪

---

<aside>

🧠 **매모리 접근**

```swift
var stepSize = 1

func increment(_ number: inout Int) {
    number += stepSize
}

increment(&stepSize)
// Error: conflicting accesses to stepSize
```

위에서 `stepSize`와 `number`는 같은 메모리 주소를 참조하기 때문에

읽기, 쓰기가 동시에 이루어져 충돌이 발생할 수 있기 때문이다.

</aside>