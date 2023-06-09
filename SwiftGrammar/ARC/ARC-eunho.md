# ARC

## Auto ****Reference Counting****

쉽게 직역하면 자동 참조 카운팅이다. 참조를 카운팅하는 이유는 메모리를 관리하기 위함이다.

자동으로 메모리 관리를 하는 것은 편리하게 사용하기 위함이다.

컴파일러가 자동으로 메모리 관리 코드를 넣어주고 코드도 훨씬 짧아지고, 자연스럽게 프로그램의 안정성을 높일 수 있게 된다.

## 장점

컴파일 당시 이미 인스턴스의 해제 시점이 정해져 있어서 인스턴스가 언제 메모리에서 해제될지 예측 가능함

## 단점

작동 규칙을 모르고 사용하면 인스턴스가 메모리에서 영원히 해제되지 않을 가능성이 있다.

## 규칙

자동으로 메모리 관리를 받기 위해서는 몇 가지 규칙을 알아야 한다. 왜냐 ARC는 컴파일과 동시에 인스턴스를 메모리에서 해제하는 시점이 결정하기 때문. 원하는 용도로 사용하려면 ARC에 명확한 힌트를 주어야 한다.

클래스의 인스턴스를 생성할 때마다 ARC는 그 인스턴스에 대한 정보를 저장하기 위한 메모리 공간을 따로 또 할당한다.