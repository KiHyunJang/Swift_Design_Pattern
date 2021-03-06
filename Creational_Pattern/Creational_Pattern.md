# Creational Pattern

## 생성 패턴 (Creational Pattern)
생성 패턴은 객체의 생성 과정을 인스턴스화를 추상화한다.   
객체를 생성 또는 합성하는 방법과 객체의 표현되는 방식을 시스템과 분리하여 독립적으로 만드는데 도움이 된다.   
생성 패턴을 통해 어떤 객체가 생성되는지, 누가 객체를 생성하는지, 객체가 어떤 과정으로 생성되는지, 객체를 언제 생성하는지를 자유롭게할 수 있다.   
   
## 생성 패턴의 분류
- 클래스 생성 패턴
    - 인스턴스로 만들 클래스를 다양하게 만들기 위한 용도로 상속을 사용
- 객체 생성 패턴
    - 객체생성의 일부를 다른 객체에게 넘김
    
## 생성 패턴의 특징
- 생성 패턴은 시스템이 어떤 클래스를 사용하는지에 대한 정보를 캡슐화
- 생성 패턴은 캡슐화한 클래스의 인스턴스가 생성되고 결합되는 방식을 숨김
   
## 생성 패턴의 종류
- 추상 팩토리 패턴(Abstract Factory Pattern)
    - 동일한 주제의 다른 팩토리를 묶어 준다.
   
- 빌더 패턴(Builder Pattern)
    - 생성(construction)과 표기(representation)를 분리해 복잡한 객체를 생성한다.
   
- 팩토리 메서드 패턴(Factory Method Pattern)
    - 생성할 객체의 클래스를 국한하지 않고 객체를 생성한다.
   
- 프로토타입 패턴(Prototype Pattern)
    - 기존 객체를 복제함으로써 객체를 생성한다.
   
- 싱글턴 패턴(Singleton pattern)
    - 한 클래스에 한 객체만 존재하도록 제한한다.
