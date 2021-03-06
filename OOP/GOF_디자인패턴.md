# GoF의 디자인 패턴

# 참고
* [개발자가 반드시 정복해야할 객체지향과 디자인 패턴 정리](https://github.com/cheese10yun/TIL/blob/master/OOP/%EA%B0%9C%EB%B0%9C%EC%9E%90%EA%B0%80-%EB%B0%98%EB%93%9C%EC%8B%9C-%EC%A0%95%EB%B3%B5%ED%95%B4%EC%95%BC%ED%95%A0-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EA%B3%BC-%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4.md)
* [객체지향 프로그래밍 입문](https://github.com/cheese10yun/TIL/blob/master/OOP/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8.md)


# 서론
> 디자인 패턴이란?
> 
> 특정한 전후 관계에서 일반적 설계 문제를 해결하기 위해 상호교류하는 수정 가능한 객체와 클래스들에 대한 설명입니다.

## 적당한 객체 찾기

![](https://i.imgur.com/HOKQ2GT.png)

* 객체는 데이터와 이 데이터에 연산을 가하는 프로시저를 함께 묶은 단위 입니다.
* 프로시저를 일반적으로 **메서드** 라고 합니다.
* 객체는 **요청, 메시지**를 사용자에게 받으면 연산을 수행합니다.
* **메시지**는 객체가 연산을 실행하는 **유일한** 방법이고, 연산은 객체의 내부 데이터의 상태를 변경하는 유일한 방법입니다.
* 접근의 제약 사항으로 객체의 내부 상태는 **캡슐화** 된다고 말합니다.
* 객체지향 설계의 가장 어려운 부분은 시스템을 구성할 객체의 분할을 결정하는 것입니다.
* **고려해야하는 요인에는 캡슐화, 크기 정하기, 종속성, 유연성, 성능, 진화, 재사용성등이 있습니다.**
* **시스템의 협력 관계나 책임을 중심으로 설계하는 방법도있고**, 실세계를 모델로 만들고 이를 분석해 설계로 전이하는 과정에서 객체로 바꾸는 방법을 사용할 수도 있습니다. 어느 방법이 가장 좋은 방법이라고 말할 수는 없습니다.
* 객체지향 설계는 실세계의 대응 관계를 갖지 못할 때가 많습니다. (객체지향은 현실 세상을 모방하는 것이 아니라 재창조하는 것이다.)


## 객체 인터페이스의 명세

```java
int(return) add(name) (int x, int y) parameter
```
return + name + parameter = **signature**

* 객체가 선언하는 모든 연산은 연산의 이름, 매개변수로 받아들이는 객체들, 연산의 반환 값을 명세합니다. 이를 연산의 **시그너처라**고 합니다.
* 인터페이스는 객체가 정의하는 연산의 모든 시그너처를 일컫는 말로 객체의 **인터페이스는 객체가 받아서 처리할 수 있는 연산의 집합입니다.**
* **타입은 인터페이스를 나타날때 사용하는 이름입니다. 객체가 Wiondow  타입을 갖는다는 것은 Window 인터페이스에 정의한 연산을 모두 처리할 수 있다는 것을 의미합니다.**
* 객체는 여러 타입을 가질수 있고, 서로 다른 객체가 하나의 타입을 공유할 수도 있습니다. 객체의 인터페이스에 정의된 연산들 중 일부는 A타입이 정의하는 연산이고, 일부 B 타입이 정의한 연산일 수 도 있습니다. 같은 타입의 두 객체는 인터페이스를 일부를 공유 해야합니다.
* 외부에서 객체를 할 수 있는 방법은 인터페이스 밖게 없기 때문에 인터페이스를 통해서만 처리를 요청할 수 있습니다.
* 객체에 요청이 전달되면 요청과 이를 받는 객체에 따라 수행되는 처리 과정이 달라질 수 있습니다. 어떤 요청과 그 요청을 처리할 객체를 프로그램 실행 중, **즉 런타임에 연결 짓는 것을 동적 바인딩 이라고 합니다. 이것을 대체성을 다형성이라고 합니다.** 


## 객체 구현 명세하기
* 클래스와 타입 사이의 차이점
  * 클래스 : 객체의 클래스는 그 객체가 어떻게 구현되느냐를 정의합니다. 클래스는 객체의 내부 상태와 그 객체의 연산에 대한 구현 방법을 정의합니다.
  * 타입 : 객체의 타입은 그 객체의 인터페이스, 즉 그 객체가 응답할 수 있는 요청의 집합을 정의합니다. 하나의 객체는 여러 타입을 가질 수 있고 서로 다른 클래스의 객체들이 동일한 타입을 가질 수 있습니다.
  * **객체의 구현은 다를지라도 인터페이스는 같을 수 있다는 의미**
* **객체의 구현은 클래스에서 정의합니다.** 클래스는 객체의 내부 데이터와 표현 방법을 명세하고, 그 객체가 수행할 연산을 정의합니다.
* 추상 클래스는 모든 서브클래스 사이의 공통되는 인터페이스를 정의 합니다. 정의만 하고 구현하지 않은 연산을 추상 연산이라 하고, 추상 클래스가 아닌 클래스를 구체 클래스라고 합니다.
* 서브 클래스는 부모 클래스가 정의한 행동을 재정의하거나 강제할 수 있습니다. 서브 클래스는 부모 클래스에 정의한 연산의 구현을 오버라이드할 수 있습니다.



## 클래스 상속 대 인터페이스 상속
* 객체의 클래스는 그 객체가 어떻게 구현되느냐를 정의합니다. 클래스는 객체의 내부 상태와 그 객체의 연산에 대한 구현 방법을 정의합니다.
* 어떤 메시지를 보내려면 수신 객체의 클래스가 이 메시지를 구현하거 있는 지를 확인해야 하지만 꼭 수신측 객체가 어떤 특정 클래스의 인스턴스일 필요는 없습니다. **단지 메시지를 처리할 수 있는지의 여부만을 확인하는 것입니다.**

## 구현에 따르지 않고, 인터페이스에 따르는 프로그래밍
* 클래스 상속은 기본적으로 부모 클래스의 정의한 구현을 재사용하여 기능을 확장하는 메커니즘입니다. **그러나 구현의 재사용이 전부는 아닙니다.** 상속이 다른 가진 다른 기능을 중에 **동일한 인터페이스를 갖는 객체군을 정의하는 것이 있는데 이것으로 다형성을 끌어낼 수 있습니다.**


추상 클래스를 정의하고 인터페이스 개념으러 객체를 다룰 때 얻을 수 있는 두 가지 이점은 다음과 같습니다. (자바에서는 추상 클래스와 인터페이스가 다르니 인터페이스를 사용했을대 이점으로 이해 했다.)

1. 사용자가 원하는 인터페이스를 그 객체가 만족하고 있는 한, 사용자는 그들이 사용하는 특정 객체 타입에 대해 알아야 할 필요는 없습니다. 
2. 사용자는 이 객체들을 구현하는 클래스를 알 필요가 없고, 단지 인터페이스를 정의하는 추상 클래스가 무엇인지 알면 됩니다.

**규현이 아닌 인터페이스에 따라 프로그래밍 합니다.**

## 재사용을 실형 가능한 것으로

* 클래스 상속에 단점 
  * 런타임에 상속을 받아 부모 클래스의 구현을 변경할 수 없습니다.
  * 부모 클래스는 서브클래스의 물리적 표현을 최소한 부분을 정의하기 때문에 서블클래스는 부모 클래스가 정의한 물리적 표현을 전부 또는 일부 상속받는 점입니다. 상속은 캡슐화를 파괴할 수 도 있습니다. **서브클래스는 부모 클래스의 구현에 종속될 수밖에 없음으로 부모 클래스 구현에 변경이 생기면 서브클래스도 변경해야합니다.**
  * 서브클래스를 재사용하려고 할 때 문제가 밸생, 상속한 구현이 새로운 문제에 맞지 않을 때, 부모 클래스를 재작성해야 하거나 다른 것으러 대체하는 일이 생기게됩니다. 이런 종석성은 유연성과 재사용성을 떨어뜨립니다.
* **클래스 상속보다 객체합성(조립)을 더 손호하는 이유는 각 클래스의 캡슐화를 유지할 수 있고, 각 클래스의 한 가지 작업에 집중할 수 있기 때문입니다.**


## 프레임워크
* 프레임워크는 응용프로그램에 대한 뼈대를 제공합니다. **클래스와 객체의 분활, 전체 구조, 크래스와 객체들 간의 상호작용, 객체와 클래스 조합 방법, 제어 흐름에 대해 미리 정의합니다.**
* 프레임워크는 응용프로그램 영역에 걸쳐 공통의 클래스들을 정의하여 일반적 설계 결정을 미리 내려둡니다. **이를 통해서 프레임워크는 코드의 재사용성보다는 설계의 재사용을 강조합니다.**
* 라이브러리를 사용하여 응용프로그램을 작성할 때는, 응용프로그램은 main 본문을 작성하고 라이브러리 코드를 호출합니다. **그러나 프레임워크를 재사용할 때는 프레임워크가 제공하는 main을 재사용하고 이 부분에서 호출하는 코드를 작성하는 것입니다.**


# 사례 연구: 문서 편집기 설계

# 결론

## 공통적인 설계자들의 어히로 쓰는 패턴
* 이 책의 디자인 패턴에 집중하게 되면 그들의 설계 어휘는 분명히 변할것입니다. **사용자는 디자인 패턴의 이름을 사용해서 자신의 의도를 표현할  수 있습니다.**

## 시스템 문서화와 학습 보조도구로 쓰는 패턴
* 디자인 패턴을 알면 기존 시스템을 이해하기가 더욱 쉬워집니다. 기존 객체지향 시스템을 이해하는데 많은 도움이 됩니다.
* 시스템이 사용하는 디자인 패턴 개념으로 시스템을 기술하면,시스템을 이해하기가 더울 쉽습니다. 공통의 어휘를 알면 패턴 자체를 설명할 필요가 업어져서 사용자는 단지 그것의 이름을 부르고 다른 사람들이 패턴을 알기를 기대하게 됩니다.


## 기존 방법에 대한 보조 역할로 쓰는 패턴
* 객체지향 설계 방법은 휼륭한 설계를 지원하고, 초보 설계자에게 설계를 잘하는 방법을 가르치며, 설계가 개발되어 가는 과정을 표준화 합니다.
