# 필터(Filter)

---

- 필터는 스위프트에서 특정 조건을 만족하는 요소들만 추출하여 새로운 배열을 생성하는 고차함수이다.

---

ex) [1, 2, 3, 4, 5] 배열에서 짝수만 뽑아 내고 싶다면 밑 코드와 같이 filter를 사용할 수 있다.

```swift
let numbers = [1, 2, 3, 4, 5] // numbers라는 배열에 1,2,3,4,5를 넣어줬다
let evenNumbers = numbers.filter { $0 % 2 == 0 } // evenNumbers 라는 배열에 필터를 사용해서 짝수만 뽑아 내는 조건을 만들었다.
// 그러면 뽑아낸 결과값이 evenNumbers 배열 속으로 들어감
print(evenNumbers) // 출력 결과: [2, 4]
```

위의 코드에서 2번 째 줄에 있는 {$0 % 2 == 0} 은 클로저로, 배열의 각 요소에 대해 실행되며 해당 요소마다 조건을 확인한다. 조건에 해당한다면(짝수라면) filter함수는 그 요소를 새로운 배열에 추가하게 된다.

---

ex) 이번엔 배열안에 숫자가 아닌 문자를 넣어 조건에 맞게 요소를 뽑아내는 코드를 만들었다.

```swift
let strings = ["apple", "banana", "kiwi", "orange", "pear"] //총 5개의 단어를 strings배열 안에 집어넣음.
let shortStrings = strings.filter { $0.count <= 5 } // 조건에 맞는 요소는 새로운 shortStrings라는 배열에 들어가게 된다.
print(shortStrings) // 출력 결과: ["apple", "kiwi", "pear"]
```

위의 코드는 문자의 길이가 5이하일 때 추출하여 출력하는 프로그램이다. 2번째 줄 클로저 개념은 글자수를 카운트 했을때 5이하인가>? 라는 뜻 따라서 글자수가 5이하인  apple, kiwi, pear 가 새로운 배열에 들어가 출력했을 때 위와 같이 나온다.

---