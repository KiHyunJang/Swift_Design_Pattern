# Factory Method Pattern

## 팩토리 메서드 패턴 (Factory Method Pattern)
 팩토리 메서드는 부모 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며, 자식클래스가 어떤 객체를 생성할지 결정하도록 하는 패턴이기도 하다.   
부모 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로 사용한다.   
   
쉽게 말하면, 객체 생성을 서브 클래스가 하도록 처리하는 패턴이다.   
이로 인해서 객체 생성을 캡슐화할 수 있고, 부모 클래스는 자식 클래스가 어떤 객체를 생성하는지 몰라도 상관없다.   
   
**Product** : Concrete Product가 해야할 동작들을 선언하는 객체   
**Concreate** Product : Product를 채택하며 그에 맞게 만든 실제 객체   
**Creator** : Product 인터페이스를 준수하는 새 객체를 반환하는 팩토리 메스드를 선언하며, Factory의 기본 역할을 정의하는 객체   
**Concrete Creator(Factory)** : Creator를 채택하고 있으며 product에 맞는 구체적 기능을 구현   
   
## 팩토리 매서드 패턴의 장점
- 프로토콜로 기본 기능을 정의해주었기 때문에 기존 코드를 변경하지 않고, 새로운 하위클래스 추가가 가능하기 때문에 유연하고 확장성이 좋다.
- 코드에 수정 사항이 생기더라도 팩토리 메소드만 수정하기 때문에 수정에 용이하다.
   
## 팩토리 메서드 패턴의 단점
- product가 추가될 때마다 새롭게 하위 클래스를 정의해주어야 하기 때문에 불필요하게 많은 클래스가 정의되어질 수 있고 그러다보면 복잡해지는 문제가 발생할 수 있다.
- 중첩되어 사용되면 매우 복잡해질 우려가 있다.
   
## 팩토리 메서드 패턴 예제
총을 예제로 팩토리 메서드 패턴을 구현해보았다.
   
Product Interface
``` swift
protocol Gun {
    var ownerName : String { get set }
    init (ownerName : String)
    func shoot()
    func Load()
}
```
   
Concrete Product
``` swift
class AK47 : Gun {
    var ownerName: String
    
    required init(ownerName : String) {
        self.ownerName = ownerName
    }
    
    func shoot() {
        print("AK47 shoot")
    }
    
    func Load() {
        print("AK47 load")
    }
    
}

class K2 : Gun {
    var ownerName: String
    
    required init(ownerName: String) {
        self.ownerName = ownerName
    }
    
    func shoot() {
        print("K2 shoot")
    }
    
    func Load() {
        print("K2 load")
    }
    
}
```
   
Creator
``` swift
protocol GunCreator {
     func createGun(ownerName: String, gunType: GunType) -> Gun
}
enum GunType {
    case AK47
    case K2
}
```

Factory(Concrete Creator)
``` swift
class GunFactory: GunCreator {
    
    func createGun(ownerName: String, gunType: GunType) -> Gun {
        switch gunType {
        case .AK47 :
            return AK47(ownerName: ownerName)
        case .K2 :
            return K2(ownerName: ownerName)
        }
    }
    
}
```

실행
``` swift
let factory = GunFactory()
let ak47 = factory.createGun(ownerName: "MinSu", gunType: .AK47)
let k2 = factory.createGun(ownerName: "Minji", gunType: .K2)

ak47.shoot() //AK47 shoot
k2.Load() //K2 load
```
