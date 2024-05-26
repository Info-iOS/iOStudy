# 동기/비동기

## 동기(**Synchronous**)란?

synchronous : 동시 발생(존재)하는

무슨 뜻이냐면 ==  작업이 동시 발생 ❌ 요청 - 응답이 동시 발생 ⭕️

➡️ 요청에 대한 응답이 동시에 발생

➡️ 내 작업이 끝나기 전까진 다른 작업 수행 못함^^

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmMLcC%2FbtqOMo6Q9YS%2FvUxTiQ7nbtvC887gFLYio0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmMLcC%2FbtqOMo6Q9YS%2FvUxTiQ7nbtvC887gFLYio0%2Fimg.png)

1의 작업이 완료되야만 다음 작업이 실행됨 

(2작업이 완료되어야 3작업, 3작업이 완료되어야 4작업)

➡️ 전체 실행 시간 45초

너무 비효율적이라구?? 근데 평소에 별도의 작업없이 내가 하는 코딩이 이거임 ㅎ

## 비동기(**Asynchronous**)란?

asynchronous : 동시에 발생(존재)하지 않는

그냥 동기의 반대임

➡️ 요청에 대한 응답이 동시에 발생 ❌

➡️ 내 작업이 끝나기 전에 다음 작업을 실행

별다른 응답이 없는 작업이라도 Async면 **다음 작업과 동시에 실행**되기 때문에,

Async작업이 많아지면 **여러 가지 작업을 '동시에' 처리** 할 수 있어짐

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdx1a1X%2FbtqOFil2eIG%2FsBE5yfwUKr2ZN8WEXtFBE1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdx1a1X%2FbtqOFil2eIG%2FsBE5yfwUKr2ZN8WEXtFBE1%2Fimg.png)

1작업이 완료되지 않아도 

2작업, 3작업, 4작업을 실행할 수 있음!!

➡️ 전체 실행 시간 20초

요청에 대한 응답이 나중에 오기 때문에

보통 Callback 함수로 들어옴

## 동기와 비동기의 장단점

|  | 동기 | 비동기 |
| --- | --- | --- |
| 장점 | 설계가 매우 간단하고 직관적임 | 응답이 주어질 때까지 기다리지 않고
다른 작업을 하므로 자원을 효율적으로 사용할 수 있다 |
| 단점 | 응답이 주어질 때까지 아무 것도 못하고 대기해야 한다 | 동기보다 설계가 복잡하다 |