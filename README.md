# Swift_Design_Pattern
 Swift로 Design Pattern 구현 및 공부

공부 기간|
---|
22.05.01 ~ |

## 디자인 패턴이란?
객체지향 설계하다보면 이전과 비슷한 상황에서 사용했던 설계를 재사용하는 경우가 종종 발생한다.
이런 설계는 특정 상황에 맞는 해결책을 빠르게 찾을 수 있도록 도와주는데, 이렇게 반복해서 사용되는 설계는 클래스, 객체의 구성, 객체 간 메세지 흐름에서 일정 패턴을 갖는다.
결국 디자인 패턴은 소프트웨어 개발 시 발생하는 다양한 상황에 대한 재사용 가능한 해결방법이다.

## 디자인 패턴 구성 요소 4가지
1.패턴 이름
2.문제
3.해법
4.결과

## 디자인 패턴의 종류
1.생성 패턴 (추상 객체 인스턴스화)
객체 생성과 관련된 패턴
객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공한다.

2.구조 패턴 (객체 결합)
클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
예를 들어 서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스를 제공하거나 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

3.행동 패턴 (객체 간 커뮤니케이션)
객체나 클래스 사이의 알고리즘이나 책임 분배에 관련된 패턴
한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 그렇게 하면서도 객체 사이의 결합도를 최소하는 것에 중점을 둔다.

------------
* Creational Pattern (생성 패턴)
    * Abstract Factory
    * Builder
    * Factory Method
    * Prototype
    * Singleton

* Structual Pattern (구조 패턴)
    * Adapter
    * Bridge
    * Composite
    * Decorator
    * Facade
    * Flyweight
    * Proxy

* Behavioral Pattern (행동 패턴)
    * Chain Of Responsibilty
    * Command
    * Interpreter
    * Iterator
    * Mediator
    * Memento
    * Observer
    * State
    * Strategy
    * Template Method
    * Visitor
