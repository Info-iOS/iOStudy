# Swift 반복문

### For
---

```swift
for i in 1...100{ //1 ~ 100까지 
    print(i)
}

let name : [String] = ["song", "kim", "park", "chang" ]

for stat in name { //모든 항목 돌아가기
    print("name is \(stat)")
}

for i in stride(from: 0, to: 5, by: 1) { //form = start, to = end, by = step
    print("\(i)") // 0 ~ 4 출력
}
```

```swift
let range1 = 0...10 // 0부터 10까지
let range2 = 0..<10 // 0부터 9까지
```

for문은 python과 매우 흡사한 느낌
<br><br>

### For Where
---
```swift
for i in range1 where i%2 == 0 {
    print(i)
}//range1에 있는 수 중 i%2 == 0을 만족하는 수, 즉 짝수만 출력
```
<br>

### While
---

```swift
var i = 1

while i < 10 {

    if i == 5 {
    	break
    }
    
    print(i)
    i += 1 
}
```
while도 python과 같음
<br><br>

### Repeat While
---

```swift
var j = 10

repeat {

    print(j)
    j += 1
    
} while j < 10
```

다른 언어 do while과 같다