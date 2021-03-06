# topic 10. 직교성

직교성은 기하학에서 빌려온 용어이다. <br />
두 벡터가 직교하면 한 벡터의 스칼라값이 변해도 다른 벡터가 가리키는 방향의 스칼라 값은 변하지 않는다. <br />
컴퓨터과학에서 이것은 독립성, 결합도 줄이기를 의미하다. <br />
직교성을 가지면 한 컴포넌트를 수정해도 다른 컴포넌트들을 수정할 필요가 없다.

## 계층 구조(layer structure)

계층 구조는 직교적 시스템을 설계하는 강력한 방법이다. <br />
각 계층은 자기 바로 밑에 있는 계층이 제공하는 추상화만을 사용하기 때문에, 다른 코드에 영향을 끼치지 않으면서 기반 구현들을 변경할 수 있게 되어 유연성이 높아진다.

## 전역 데이터를 피하라

코드가 전역 데이터를 참조할 때마다 코드는 해당 데이터를 공유하는 다른 컴포넌트와 묶이게 된다. <br />
전역 데이터를 읽기 전용으로 사용한다고 하더라도 문제가 생길 수 있다. <br />
예를 들어 코드를 갑자기 멀티 스레드로 바꿔야 하는 경우 문제가 생길 수 있다.

**싱글턴 객체를 일종의 전역 데이터로 남용하지도 말아야 한다.** <br />
싱글턴을 이렇게 사용하면 마찬가지로 불필요한 결합을 만들 수 있다.

전역 데이터가 필요하면 **컨텍스트**를 만들어 모듈에 명시적으로 넘겨주는 방법을 택하자

## 유사한 함수를 피하라

유사해 보이는 함수를 여럿 구현해야 할 떄, 중복 코드가 많아진다.
이 때에는 GoF의 디자인 패턴 중 **전략 패턴**을 사용하자.

## 리팩터링

기회가 있을 때마다 코드의 구조와 직교성으 개선하기 위해 노력하는 과정

## 객체지향 언어와 함수형 언어의 직교성 차이

어떤 언어로든 직교적이고 좋은 코드를 쓸 수 있다.

### 객체 지향 언어

객체 지향 언어는 불투명한 결합을 만들 가능성을 잔뜩 높이는 기능이 많다. <br />
다중 상속, 예외, 연산자 오버로딩, 상속을 이용한 부모 메서드 오버라이딩 같은 것들이다. <br />
클래스가 코드와 데이터를 묶기 때문에 생기는 결합도 있다. <br />
이런 결합은 보통은 좋은 것이지만(이런 좋은 결합을 응집성(cohesion)이라고 부른다.) <br />
클래스가 관심사에 잘 집중하지 않으면 인터페이스가 엉망으로 망가질 수 있다.

### 함수형 언어

작고 독립된 함수를 많이 만든 다음, 이를 여러가지로 조합하여 문제를 해결하도록 유도한다. <br />
이론적으로는 좋아보이고 실제로도 그런 경우가 많다. 하지만 여기서도 모종의 결합이 생길 수 있다. <br />
이런 함수는 일반적으로 데이터를 변환하는데, 한 함수의 결과가 다른 함수의 입력이 되는 식이다. <br />
이때 주의하지 않으면 함수가 생성하는 데이터 포맷을 바꾸는 바람에 그 이후로 이어지는 변환 어딘가를 망가트릴 수 있다. <br />
좋은 타입 체계를 갖춘 언어를 사용하면 이런 문제를 어느 정도 예방할 수 있다.
