# Prototype Pattern

## 프로토타입 패턴 (Prototype Pattern)
프로토 타입패턴은 코드를 class에 종속시키지 않고 기존의 객체를 복제하기 위한 패턴이다.   
클라이언트 응용 프로그램 코드 내에서 객체 창조자를 서브클래스하는 것을 피할 수 있게 해준다.   
프로토 타입 패턴은 새로운 객체는 일반적인 방법으로 객체를 생성하는 고유의 비용이 주어진 응용 프로그램 상황에 있어서 불가피하게 매우 클 때, 이 비용을 감내하지 않을 수 있게 해준다.   
class는 참조 타입인데, 참조 타입의 복사 방법엔 깊은 복사와 얕은 복사가 있다.   
얕은 복사란 해당 객체만 복사하여 새 객체를 생성하는데, 원본 객체의 인스턴스 변수와 같은 메모리 주소를 참조한다.   
깊은 복사란 해당 객체의 인스턴스 변수까지 복사하며, 전부 복사하여 새 주소에 담기 때문에 참조를 공유하지 않음. 
따라서 해당 객체의 모든 정보를 완전히 복사해 새로운 객체를 만드려면 깊은 복사가 필요하다.   
이러한 작업을 쉽게 해주는 패턴이 프로토 타입 패턴이다.   
코드 구조를 패턴화하기 위해서 인터페이스를 정의하곤 한다.   
사실 인터페이스를 굳이 사용하지 않고 자기 자신을 반환하는 메서드를 만드는 경우도 많다.   

Prototype : 객체를 복제할 방법을 선언
Concrete Prototype : 객체 복제 방법을 구현
      
## 프로토타입 패턴을 사용하면 좋을 때
기존의 객체를 복제하려는데 원본 객체의 모든 값을 가지고 직접 새로운 객체를 만들 때, 만약 접근제어가 private인 프로퍼티는 접근할 수 없기때문에 복사가 불가능하다.   
또한 원본 객체의 클래스를 알야아 하기 때문에 코드가 해당 클래스에 종속되어 의존성이 생긴다.
이 때, 프로포타입 패턴을 사용하면 된다.
    
## 프로토타입 패턴의 장점
- 간단하게 새로운 객체를 복제할 수 있으며, 런타임에서 처리하기 때문에 유연하다.   
- 다양한 구조로 객체를 자식 클래스에서 만들 수 있음.
   
## 프로토타입 패턴 예제
피자는 맛있기때문에 피자로 예제를 만들어보겠다.
   
Prototype 생성
``` swift
protocol Prototype : AnyObject {
    func clone() -> Self
}
```
   
Concrete Prototype 생성
``` swift
class Pizza : Prototype {
    
    var price : Int
    
    init( price : Int) {
        self.price = price
    }
    
    func clone() -> Self {
        return Pizza(price: self.price) as! Self
    }
}
```
   
실행
``` swift
let aPizza = Pizza(price: 10000)
aPizza.price += 10000
print(aPizza.price) //20000

let bPizza = aPizza.clone()
print(bPizza.price) //20000

bPizza.price += 555
print(aPizza.price) //20000
print(bPizza.price) //20555
```
