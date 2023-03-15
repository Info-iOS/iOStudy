# 흐름 제어
---

## if

---

스위프트도 조건문이 있습니다

```
let first: Int = 3
let second: Int = 1

if(first > second){
    print("\\(first) > \\(second)")
}else if(first < second){
        print("\\(first) < \\(second)")
    }else{
        print("\\(first) == \\(second)")
    }
```

스위프트와 C언어의 차이점은 별거 없습니다. 스위프트에서는 if문에서 소괄호를 써도 되고 안 써도 상관없습니다.

```
//응용
let IntNumber1: Int = 2;
let IntNumber2: Int = 3;
let IntNumber3: Int = 0;
var Temp: Int = 0;
if(IntNumber1 > IntNumber2 ){
    Temp = (IntNumber2 > IntNumber3) ? IntNumber2 : IntNumber3
}
else if(IntNumber2 > IntNumber1){
    Temp = (IntNumber1 > IntNumber3) ? IntNumber1 : IntNumber3
}
else{
    Temp = (IntNumber1 > IntNumber2) ? IntNumber1 : IntNumber2
}
print(Temp)
```

-   실행 결과
-   2

위 코드는 중간 값을 구하는 코드입니다.

```
var isDoeMode = true

if(isDorkMode)
{
    print("다크모드 입니다.")
} else {
    print("다크모드가 아닙니다.")
}
```

이렇게 굳이 조건식을 쓰지 않아도 if문을 사용할 수 있습니다

```
let age = 10

if age > 20 {
    print("성인입니다")
}else{
    print("미성년입니다")
}

if age >= 10 && age < 20 {
    print("10대 입니다")
}else if age > 20 && age < 30 {
    print("20대 입니다")
}else if age > 20 && age < 30 {
    print("30대 입니다")
}else if age > 20 && age < 30 {
    print("40대 입니다")
}else {
    print("......")
}
```

## switch

---

switch문은 swift에서는 많이 달라진 언어입니다

c언어는 break를 써주지 않으면 무한루프가 실행됩니다

```
#include <stdio.h>

int main(void)
{
    int a;
    scanf("%d",&a);
    switch(a)
    {
        case 1:
            printf("hello");
        case 2:
            printf("hi");
        case 3:
            printf("good");
        default:
            printf("wow");
    }
    return 0;
}
```

-   실행 결과
-   hellohigoodwow

원하는 값은 1이었는데 1부터 default값까지 전부 다 출력한다 (braek를 쓰면 딱 끝난다)

하지만 우리 스위프트는 그런 거 없다 스위프트는 원하는 값을 받으면 break가 없어도 실행된다

```
let SwiftSwitch: Int = 1;

switch(SwiftSwitch){
case 1:
    print("hello")
case 2:
    print("hi")
case 3:
    print("good")
default:
    print("wow")
}
```

-   실행 결과
-   hello

원하는 값을 넣어주면 break가 없어도 잘 실행되는 것을 볼 수 있다

하지만 스위프트는 나름에 rule가 있습니다 switch문을 작성할 때는 무조건 default를 무조건 써주어야 합니다

아! 만약 난 c언어처럼 연속 구문을 쓰고 싶다~하시면 fallthrough를 사용하면 됩니다

```
let interValue: Int = 5

switch(interValue){
case 0:
    print("Value == zero")
case 1...10:
    print("Value == zero")
    fallthrough
case Int.min..<0, 101..<Int.max:
    print("Value < 0 or Value > 100")
    break
default:
    print("10 < Value <= 1~10")
}
```

-   실행 결과
-   Value == zero Value < 0 or Value > 100

참고 \= 1... 10은 1부터 10까지 라는 뜻|| Int.min.. <0 = interValue는 0보다 크다 ||

101.. < Int.max= interValue는 0보다 작다

위에서 fallthrough를 사용하였기 때문에 break를 사용하여야 한다

---

swift에서 switch에서는 부동소수까지 표현이 가능하다.

```
let doubleValue: Double = 3.0

switch(doubleValue) {
case 0:
    print("Value == zero")
case 1.5...10.5:
    print("1.5 <= Value <= 10.5")
default:
    print("Value == \\(doubleValue)")
}
```

---

swift에서는 꼭 case 뒤에 숫자가 아니어도 상관없습니다.

```
let stringValue: String = "Liam Neeson"

switch stringValue {
case "junha":
    print("He is junha")
case "Jay":
    print("He is Jay")
case "Jenny","Joker","Nova":
    print("He or She is \\(stringValue)")
    
default:
    print("\\(stringValue) said 'I don't know who you are'")
}
```

-   실행 결과
-   Liam Neeson said 'I don't know who you are'

이처럼 스위프트에서는 swift에서의 switch에서는 문자열 및 다양한 기호를 이렇게 넣을 수 있습니다.

하지만 c언어에서는 case를 사용하고 모든 것을 연속 출력허기 위해서

```
#include <stdio.h>

int main(void)
{
    int a;
    scanf("%d",&a);
    switch(a)
    {
        case 1:
        case 2:
        case 3:
            printf("hello");
        default:
            printf("hi");
            break;
    }
    return 0;
}
```

이런 식에 코드를 사용하여서 1,2,3의 값을 똑같이 받을 수 있다.

하지만 위에서 말했듯 swift에는 1... 3 있기 때문에 case에 빈 공간을 둘 필요가 없다 swift에는 빈공간을 두면 오류가 발생한다

```
let stringValue: String = "Android"

switch stringValue {
case "Junha":
    print("he is junha")
case "ios":
    print("He is ios");
case "js":
    fallthrough
case "html":
    fallthrough
case "C":
    print("He or She is \\(stringValue)")
default:
    print("\\(stringValue) said 'I don't know who you are.'")
}
```

-   실행 결과
-   Android said 'I don't know who you are.'

이렇게 응용도 가능합니다 ^^

```
typealias NameAge = (name: String, age: Int)

let tupleValue: NameAge = ("junha",99)

switch(tupleValue){
case ("junha",99):
    print("정확히 맞췄습니다!")
default:
    print("누굴 찾나요?")
}
```

-   실행 결과
-   정확히 맞췄습니다!
-   해석
-   NameAge값에 튜플 값을 입력해 주면 tupleValue를 입력해주면 자동으로 입력됩니다. 값이 맞지 않으면 default 값으로 넘어가서 실행됩니다.

튜플을 사용하여서 switch를 사용할 수 있습니다

```
typealias NameAge = (name: String, age: Int)

let tupleValue: NameAge = ("junha",18)
switch tupleValue {
case ("junha",17):
    print("정확히 맞췄습니다!")
case ("junha",let age):
    print("이름만 맞았습니다. 나이는 \\(age)가 아닙니다")
case(let name, 17):
    print("나이는 맞았습니다. 이름은 \\(name)님이 아닙니다")
default:
    print("누굴 찾나요?")
}
```

나중에 switch를 사용하면 회원가입 어플을 만들 수 있을까.. 합니다.

참고로 스위프트에서 default를 사용할 필요가 없어도 무조건 default는 꼭 사용해야 합니다.

열거형을 쓰는 방법도 있습니다.

주로 주어진 이름 중에 선택합니다.

```
enum Menu {
    case chicken
    case pizza
}

let lunchMenu: Menu = .chicken

switch lunchMenu {
case .chicken:
    print("반반으로 주세요.")
case .pizza:
    print("핫소스 많이 주세요")
case _:      //case default와 같은 의미 입니다
    print("오늘 메뉴가 뭐죠?")
}
```

## for-in

---

for in은 반복문이다 c언어와 다른 점은 for문만 쓰는 것이 아니라 조건식이 필요하기 때문에 where를 사용한다

```
var myArray : [Int] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for item in myArray {
    print("item: \\(item)")
}
```

-   실행 결과
-   item: 0 item: 1 item: 2 item: 3 item: 4 item: 5 item: 6 item: 7 item: 8 item: 9 item: 10

이렇게 배열에 있는 값을 출력할 수 있다

```
var myArray : [Int] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for item in myArray where item > 5{
    print("5 보다 큰 수: \\(item)")
}
```

-   실행결과
-   5 보다 큰 수: 6 5 보다 큰 수: 7 5 보다 큰 수: 8 5 보다 큰 수: 9 5 보다 큰 수: 10

where를 사용하여서 조건을 써주는 방법도 있다.

예)

```
for item in myArray where item % 2 == 0{
    print("짝수: \\(item)")
}
```

-   실행 결과
-   짝수: 0 짝수: 2 짝수: 4 짝수: 6 짝수: 8 짝수: 10

예)

```
for item in myArray where item % 2 == 1{
    print("홀수: \\(item)")
}
```

-   실행 결과
-   홀수: 1 홀수: 3 홀수: 5 홀수: 7 홀수: 9
