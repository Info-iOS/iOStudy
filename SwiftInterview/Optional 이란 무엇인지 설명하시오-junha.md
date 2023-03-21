# Optional 이란 무엇인지 설명하시오.
---

### Optional 이란?
​
swift 코드에 안전성을 높여주는 것이 Optional입니다.
​
?를 사용해서 변수의 값이 nil일 수 있다고 알려주는 것입니다.
​
### 언제 사용할까?
​
주로 swift에서는 nil 값인 경우 강제 실행(!)을 하게 되면 앱이 멈춰 버립니다. 때문에 nil값이 들은 경우를 예외처리하거나 안전하게  
처리할 때 많이 사용합니다.
​
### Optional을 사용하면 뭐가 좋을까?
​
위에서 말했듯이 nil이 발견되면 터지기 때문에 Optional을 사용해서 nil로 인한 문제를 해결할 수 있습니다.
​
### Optional Unwrapping은 무엇일까?
​
Optional Unwrapping은 옵셔널 해제라는 뜻을 가지고 있습니다. 
​
즉 Optional Unwrappingsm는 Optional 변수의 Optional을 벗기는 작업입니다. 주로 nil이 절대 없으면 ! 를 사용해서 optional을 벗깁니다. 주로 Optional Unwrapping는 !를 사용해서 벗겨냅니다.
​
### Optional Binding은 무엇일까?
​
Optional Binding은 Optional 타입 변수 안에 값이 있는지 없는지를 확인 할 수 있도록 해주는 기능입니다.
​
Optional Unwrapping에서는 강제적으로 벗겨냈다면 Optional Binding는 좀더 안전하게 !를 사용하지 않고 Optional를 벗길 수 있습니다.
​
### Optional Chaining은 무엇일까?
​
Optional Chaining는 Optional끼리의 연산이 필요할 셩우 사용하는 것인데 이때 모든 변수에 옵셔널 바인딩을 하면 if문이 더러워지기 때문에 Optional Chaining를 사용하면 Optional 예외처리를 간단하게 할 수 있습니다.
​
### Optional 왜 사용하는 걸까?
​
objc에는 아직 nil타입이 존재하기 때문에 objc와 swift를 혼용해서 우리가 앱을 만들기 때문에 상호운용성 때문에 사용합니다
​
참고로 !는 강제 언래핑입니다.
